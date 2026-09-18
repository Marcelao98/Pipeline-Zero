# SQL na prática: subqueries

Repara no caminho que a gente percorreu até aqui. Os capítulos 3, 4 e 5 foram todos sobre ler dado que já existe: `SELECT`, `WHERE`, `ORDER BY`, `LIMIT`, depois `COUNT`, `SUM`, `GROUP BY`, `HAVING`, depois `JOIN`. O capítulo 6 virou a moeda e foi sobre escrever dado: `CREATE TABLE`, `INSERT`, `UPDATE`, `DELETE`. Esse capítulo volta pro lado de ler, porque ainda sobrou um tipo de pergunta que nenhum dos comandos anteriores, sozinho, consegue responder direito. É a vez da subquery.

## O que é uma subquery

Uma **subquery** é, no fim das contas, uma consulta SQL dentro de outra consulta SQL. Em vez de escrever um valor fixo numa condição (tipo `WHERE valor_total > 100`), você escreve um `SELECT` inteiro naquele lugar, e o banco executa esse `SELECT` de dentro primeiro, pega o resultado dele, e usa esse resultado como se fosse o valor que você tinha digitado na mão.

O nome "subquery" vem exatamente disso: é uma query subordinada a outra, que existe pra alimentar a consulta principal com um resultado que, de outro jeito, você não teria como escrever direto.

## Que problema isso resolve

Até aqui, toda condição que a gente escreveu num `WHERE` ou `HAVING` usava um valor que a gente já sabia de antemão: `estado = 'SP'`, `valor_total > 100`, `SUM(valor_total) > 300`. Mas existe um tipo de pergunta onde o valor de comparação não é algo que você já sabe, é algo que precisa ser calculado primeiro, a partir do próprio banco.

Um exemplo bem comum: "quais pedidos tiveram valor acima da média?" Pra responder isso, primeiro alguém precisa calcular a média de todos os pedidos, e só depois comparar cada pedido individual contra esse número. O problema é que esse número (a média) não existe antes da consulta rodar, ele é resultado de uma consulta. É exatamente esse tipo de pergunta, que depende de um resultado intermediário calculado dentro do próprio banco, que subquery resolve.

## Como seria resolver isso sem subquery

Sem subquery, sobram duas saídas, e nenhuma das duas é boa. A primeira é rodar duas consultas separadas: uma pra calcular a média, olhar o número que voltou, e depois copiar esse número na mão pra dentro de uma segunda consulta, tipo `WHERE valor_total > 160.82`. Funciona, mas é manual, lento, e quebra na hora que o dado mudar, porque ninguém vai lembrar de recalcular aquele número toda vez.

A segunda saída é puxar o dado bruto inteiro pro banco de fora (uma planilha, um script), e fazer a conta de média e a comparação lá fora, sem envolver o banco nisso. Isso funciona pra pouco dado, mas desperdiça exatamente a vantagem que um banco de dado relacional tem: ele é feito pra processar dado em volume, ali mesmo onde o dado já está, sem precisar mover tudo pra outro lugar antes.

Subquery resolve os dois problemas de uma vez: o cálculo intermediário e a comparação final acontecem dentro da mesma consulta, no mesmo banco, sem etapa manual no meio.

## Os dois formatos mais comuns de subquery

Subquery pode aparecer em vários lugares diferentes de uma consulta, mas os dois formatos mais comuns, e os que resolvem a maior parte do que você vai precisar no começo, são esses:

**Subquery escalar** é uma subquery que devolve um valor só (uma linha, uma coluna). Ela entra numa comparação simples, no lugar onde você usaria um número fixo:

```sql
SELECT coluna
FROM tabela
WHERE coluna operador (SELECT algo FROM outra_tabela);
```

**Subquery de lista** é uma subquery que devolve vários valores (várias linhas, uma coluna). Ela não entra numa comparação simples, porque não tem como comparar uma coluna contra uma lista inteira com `=` ou `>`. Em vez disso, ela entra com `IN`, que verifica se o valor está dentro daquela lista:

```sql
SELECT coluna
FROM tabela
WHERE coluna IN (SELECT algo FROM outra_tabela);
```

Repara que, nos dois casos, a subquery fica entre parênteses, e o banco sempre executa ela primeiro, de dentro pra fora, antes de resolver a consulta de fora.

## Trade-off: cuidado com subquery aninhada demais

Subquery dentro de uma subquery é totalmente válido. Nada impede você de colocar uma subquery dentro da outra, várias vezes seguidas, pra resolver uma pergunta que depende de vários passos intermediários.

Só que isso cobra um preço: legibilidade. Cada subquery aninhada empurra a leitura pra mais longe do que a consulta realmente está perguntando, porque você lê de fora pra dentro, mas o banco resolve de dentro pra fora, e seu olho tem que fazer esse malabarismo toda vez. Duas subqueries aninhadas já dá pra acompanhar sem muito esforço. Três, quatro, cinco, e a consulta vira um quebra-cabeça, difícil de ler, difícil de revisar, difícil de corrigir sem quebrar alguma coisa.

Isso é um problema real o suficiente pra merecer solução própria em SQL, e é exatamente isso que o próximo capítulo, sobre CTE, resolve: um jeito de escrever esses passos intermediários em pedaços nomeados e separados, em vez de empilhar parênteses uns dentro dos outros.

## Exemplo prático

Vamos usar o mesmo dataset de clientes, pedidos e produtos que a gente já vem usando desde os capítulos anteriores.

**Subquery escalar**: quais pedidos tiveram valor acima da média geral de todos os pedidos?

```sql
SELECT id_pedido, valor_total
FROM pedidos
WHERE valor_total > (SELECT AVG(valor_total) FROM pedidos);
```

A subquery `(SELECT AVG(valor_total) FROM pedidos)` roda primeiro, e devolve um valor só: a média de todos os pedidos, que é `160.82` (aproximando as casas decimais). Depois disso, a consulta de fora vira, na prática, `WHERE valor_total > 160.82`, e filtra só quem passa desse número.

Resultado:

| id_pedido | valor_total |
|---|---|
| 103 | 320.00 |
| 105 | 210.00 |

**Subquery de lista**: quais clientes compraram algum produto da categoria Eletrônicos?

```sql
SELECT nome
FROM clientes
WHERE id_cliente IN (
    SELECT pedidos.id_cliente
    FROM pedidos
    JOIN produtos ON pedidos.id_produto = produtos.id_produto
    WHERE produtos.categoria = 'Eletrônicos'
);
```

A subquery junta `pedidos` com `produtos` pra achar o `id_cliente` de todo pedido que envolveu um produto da categoria Eletrônicos (Fone de Ouvido e Teclado Mecânico), e devolve essa lista de `id_cliente`. A consulta de fora então traz o nome de todo cliente cujo `id_cliente` está dentro dessa lista.

Resultado:

| nome |
|---|
| Ana Souza |
| Diego Martins |

Ana Souza comprou o Fone de Ouvido no pedido 101, e Diego Martins comprou o mesmo Fone de Ouvido no pedido 106. O Teclado Mecânico, apesar de também ser Eletrônicos, nunca foi comprado por ninguém, então ele não contribui com nenhum cliente pra essa lista.

Vale ver, rapidamente, o que essa mesma pergunta pareceria sem usar `JOIN` dentro da subquery, aninhando uma subquery dentro da outra:

```sql
SELECT nome
FROM clientes
WHERE id_cliente IN (
    SELECT id_cliente
    FROM pedidos
    WHERE id_produto IN (
        SELECT id_produto
        FROM produtos
        WHERE categoria = 'Eletrônicos'
    )
);
```

Funciona, chega no mesmo resultado, mas repara como fica mais difícil de acompanhar: pra entender o que essa consulta faz, você precisa ler de fora pra dentro, guardar na cabeça o que cada camada depende da de baixo, e só no final juntar tudo. É exatamente esse tipo de aninhamento que o trade-off lá em cima estava avisando.

## Fechando esse capítulo

Com subquery, a gente resolve pergunta que depende de um resultado calculado antes, seja um valor só (subquery escalar) ou uma lista de valores (subquery de lista), tudo dentro da mesma consulta, sem etapa manual no meio. Mas também vimos o limite disso: subquery aninhada demais custa legibilidade.

É esse exato problema que o próximo capítulo resolve, com CTE (Common Table Expression): um jeito de escrever esses mesmos passos intermediários em blocos nomeados e separados, lidos de cima pra baixo, em vez de empilhados uns dentro dos outros.
