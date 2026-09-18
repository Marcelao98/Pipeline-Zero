# SQL na prática: agregando e agrupando dado

No capítulo anterior a gente aprendeu a trazer dado do banco e filtrar linha por linha: `SELECT`, `WHERE`, `ORDER BY`, `LIMIT`. Isso resolve um bocado de pergunta, mas não resolve tudo. Repara que em nenhum momento a gente somou o valor de um pedido, contou quantos pedidos um cliente fez, ou resumiu várias linhas numa métrica só. É exatamente esse buraco que esse capítulo preenche: agregação e agrupamento de dado.

## Relembrando os dados que a gente vem usando

Continuando com a mesma loja online dos capítulos anteriores, a tabela de clientes tem essas linhas. Pra esse capítulo, vou aproveitar e adicionar mais um cliente novo na base, só pra deixar os exemplos de agrupamento mais ricos:

| id_cliente | nome | email | estado |
|---|---|---|---|
| 1 | Ana Souza | ana@email.com | SP |
| 2 | Bruno Lima | bruno@email.com | RJ |
| 3 | Carla Dias | carla@email.com | SP |
| 4 | Diego Martins | diego@email.com | MG |

E a tabela de pedidos tem essas linhas:

| id_pedido | id_cliente | data_pedido | valor_total |
|---|---|---|---|
| 101 | 1 | 2026-08-02 | 150.00 |
| 102 | 2 | 2026-08-10 | 89.90 |
| 103 | 1 | 2026-09-01 | 320.00 |
| 104 | 3 | 2026-09-05 | 45.00 |
| 105 | 1 | 2026-09-12 | 210.00 |
| 106 | 4 | 2026-09-15 | 150.00 |

## COUNT: contando quantas linhas

Primeira pergunta que costuma aparecer: quantas linhas tem isso aqui? Quantos pedidos existem no total, ou quantos pedidos um cliente específico fez? É pra isso que existe o `COUNT`: ele conta quantas linhas atendem ao que você pediu, em vez de te devolver as linhas em si.

Se eu quiser saber quantos pedidos a Ana Souza (id_cliente 1) fez:

```sql
SELECT COUNT(*)
FROM pedidos
WHERE id_cliente = 1;
```

Resultado:

| count |
|---|
| 3 |

Repara que a resposta não é uma lista de pedidos, é um número só. `COUNT` resume várias linhas numa métrica.

Uma observação rápida: `COUNT(*)` conta toda linha, sem exceção. Mas se você trocar o `*` pelo nome de uma coluna, tipo `COUNT(email)`, o comportamento muda: `COUNT(coluna)` ignora linha onde aquela coluna específica está vazia (nula). Não vou entrar em detalhe sobre valor nulo agora, isso é assunto de outro capítulo, só fica registrado que `COUNT(*)` e `COUNT(coluna)` podem dar número diferente.

## SUM: somando o valor de uma coluna

Contar quantas linhas existem é útil, mas às vezes a pergunta é outra: quanto isso dá somado? É pra isso que existe o `SUM`: ele soma o valor de uma coluna numérica ao longo de todas as linhas que baterem com o filtro.

Se eu quiser saber quanto a Ana Souza gastou no total:

```sql
SELECT SUM(valor_total)
FROM pedidos
WHERE id_cliente = 1;
```

Resultado:

| sum |
|---|
| 680.00 |

De novo, a resposta é um número só, não uma lista de pedidos. `150.00 + 320.00 + 210.00 = 680.00`, os três pedidos da Ana somados numa métrica.

## E se eu precisar de outra conta? (AVG, MIN, MAX)

`COUNT` e `SUM` não são as únicas funções de agregação que existem. Tem também `AVG` (tira a média de uma coluna), `MIN` (pega o menor valor) e `MAX` (pega o maior valor). A lógica é a mesma do `COUNT` e do `SUM`: você joga uma coluna dentro delas e recebe um número só de volta. Não vou destrinchar cada uma agora, só fica registrado que elas existem e seguem o mesmo raciocínio.

## GROUP BY: resumindo por grupo, não a tabela inteira

Até aqui, `COUNT` e `SUM` resumiram a tabela inteira (ou o que sobrou depois do `WHERE`) numa linha só. Isso funciona bem quando eu já sei de antemão qual cliente eu quero, tipo o exemplo da Ana Souza acima, onde eu filtrei por `id_cliente = 1` na mão.

Mas e se eu quiser a resposta pra todo cliente de uma vez, sem escrever uma consulta separada pra cada um? Sem nenhum agrupamento, um `SELECT COUNT(*) FROM pedidos` simplesmente conta todas as linhas da tabela inteira, sem separar por cliente nenhum:

```sql
SELECT COUNT(*)
FROM pedidos;
```

Resultado:

| count |
|---|
| 6 |

Um número só, misturando pedido de todo mundo. Não é isso que eu quero. Eu quero uma contagem por cliente. É exatamente isso que o `GROUP BY` resolve: ele separa as linhas em grupos antes de aplicar a agregação, e cada grupo vira uma linha de resultado, com a métrica já calculada só pra aquele grupo.

Pra deixar isso bem concreto, olha a diferença entre a tabela de pedidos antes de agrupar e depois de agrupar por `id_cliente`.

**Antes de agrupar** (a tabela de pedidos crua, linha por linha):

| id_pedido | id_cliente | valor_total |
|---|---|---|
| 101 | 1 | 150.00 |
| 102 | 2 | 89.90 |
| 103 | 1 | 320.00 |
| 104 | 3 | 45.00 |
| 105 | 1 | 210.00 |
| 106 | 4 | 150.00 |

**Depois de agrupar por `id_cliente`** (uma linha por cliente, já com `COUNT` e `SUM` calculados):

| id_cliente | qtd_pedidos | total_gasto |
|---|---|---|
| 1 | 3 | 680.00 |
| 2 | 1 | 89.90 |
| 3 | 1 | 45.00 |
| 4 | 1 | 150.00 |

As seis linhas soltas viraram quatro linhas, uma por cliente. Isso é o `GROUP BY` em ação: sem ele, `COUNT`/`SUM` resumem a tabela inteira numa linha só; com ele, resumem grupo por grupo.

A sintaxe pra chegar nesse resultado é:

```sql
SELECT id_cliente, COUNT(*) AS qtd_pedidos, SUM(valor_total) AS total_gasto
FROM pedidos
GROUP BY id_cliente;
```

Repara em três coisas. Primeiro, `GROUP BY id_cliente` é o que diz pro banco "separa as linhas em grupos, um grupo pra cada `id_cliente` diferente". Segundo, `COUNT(*)` e `SUM(valor_total)` agora são calculados dentro de cada grupo, não na tabela inteira. Terceiro, usei `AS qtd_pedidos` e `AS total_gasto` só pra dar um nome mais legível pra cada coluna do resultado, em vez de deixar aparecer `count` e `sum` genérico.

Uma regra importante: toda coluna que aparece no `SELECT` sem estar dentro de uma função de agregação precisa também aparecer no `GROUP BY`. Faz sentido: se `id_cliente` não estivesse no `GROUP BY`, o banco não saberia dizer qual `id_cliente` mostrar em cada linha do resultado, já que cada linha ali representa vários pedidos misturados.

Isso é fácil de esquecer na prática. Imagina que eu tentasse trazer o nome do cliente junto, sem colocar `nome` no `GROUP BY`:

```sql
SELECT id_cliente, nome, SUM(valor_total) AS total_gasto
FROM pedidos
GROUP BY id_cliente;
```

Essa consulta dá erro. O banco devolveria algo parecido com `column "nome" must appear in the GROUP BY clause or be used in an aggregate function`, porque `nome` não está agregado (não tá dentro de um `SUM`, `COUNT` etc) nem está no `GROUP BY`, e o banco não tem como decidir qual `nome` mostrar numa linha que já resume vários pedidos.

Já que estamos falando de resumir tabela inteira em grupo, vale plantar uma pergunta: e se essa tabela de pedidos tivesse milhões de linhas, em vez de seis, será que `GROUP BY` ainda roda rápido assim? Não vou responder isso agora, mas guarda essa pergunta, ela volta a fazer sentido quando o repositório chegar em data warehouse.

## HAVING: filtrando depois de agrupar

Agora que eu sei agrupar, surge uma pergunta nova: e se eu só quiser ver os clientes que gastaram mais de R$100 no total? Minha primeira tentação seria usar `WHERE`, já que foi ele que aprendi a filtrar linha no capítulo passado. Só que tem um problema: `WHERE` filtra a linha *antes* de ela entrar no grupo, e `total_gasto` só existe *depois* de agrupar e somar. Não dá pra filtrar por uma coisa que ainda não foi calculada.

É pra esse buraco que existe o `HAVING`: ele filtra o grupo, depois que a agregação já rodou. É a mesma ideia do `WHERE`, só que aplicada numa etapa mais tardia da consulta.

```sql
SELECT id_cliente, SUM(valor_total) AS total_gasto
FROM pedidos
GROUP BY id_cliente
HAVING SUM(valor_total) > 100;
```

Resultado:

| id_cliente | total_gasto |
|---|---|
| 1 | 680.00 |
| 4 | 150.00 |

O cliente 2 gastou 89.90 e o cliente 3 gastou 45.00, os dois abaixo de 100, então `HAVING` descartou os dois grupos. Já o cliente 1 (680.00) e o cliente 4 (150.00) passaram do filtro, e ficaram no resultado. Dá pra ver bem o efeito do `HAVING`: ele não muda quantos grupos existem, só decide quais deles sobrevivem no resultado final.

Essa é a confusão clássica de quem tá começando: `WHERE` filtra linha individual, antes de qualquer agrupamento acontecer. `HAVING` filtra grupo já resumido, depois que `GROUP BY` e a função de agregação já rodaram. Se a condição usa uma coluna que existe na tabela original (tipo `estado = 'SP'`), é `WHERE`. Se a condição usa o resultado de uma agregação (tipo `SUM(valor_total) > 100`), é `HAVING`.

Os dois, inclusive, podem conviver na mesma consulta, cada um cuidando da sua etapa.

## Juntando tudo num exemplo só

Vamos combinar tudo que esse capítulo cobriu numa pergunta de negócio real: "quais clientes gastaram mais de R$300 no total, ordenados do maior gasto pro menor?"

```sql
SELECT id_cliente, SUM(valor_total) AS total_gasto
FROM pedidos
GROUP BY id_cliente
HAVING SUM(valor_total) > 300
ORDER BY total_gasto DESC;
```

Resultado:

| id_cliente | total_gasto |
|---|---|
| 1 | 680.00 |

Repara no que aconteceu: `GROUP BY` separou os pedidos por cliente e somou o valor de cada grupo, `HAVING` descartou todo grupo com total igual ou abaixo de R$300, e `ORDER BY` deixou o resultado ordenado do maior gasto pro menor (nesse exemplo só sobrou um cliente, mas a lógica seria a mesma com uma base maior). Essa é a ordem real em que o banco processa uma consulta assim: primeiro filtra linha (`WHERE`, se tivesse), depois agrupa (`GROUP BY`), depois filtra grupo (`HAVING`), e só no fim ordena (`ORDER BY`).

## Fechando esse capítulo

Com `COUNT`, `SUM`, `GROUP BY` e `HAVING`, já dá pra responder pergunta de resumo, tipo "quanto cada cliente gastou" ou "quantos pedidos cada cliente fez". Mas repara que, até aqui, toda consulta trabalhou numa tabela só, a de pedidos. Em nenhum momento a gente trouxe o nome do cliente pra dentro do resultado, só o `id_cliente`, porque o nome mora na outra tabela.

Vale conectar isso com o [ciclo de vida da engenharia de dados](../1-que-porra-e-essa/02-o-ciclo-de-vida-da-engenharia-de-dados.md) que a gente viu lá no primeiro módulo: tudo que fizemos nesse capítulo é a etapa de transformação acontecendo na prática. Dado bruto, linha por linha, virando métrica (total gasto, quantidade de pedido). É exatamente esse tipo de trabalho que mora naquela etapa do ciclo.

É exatamente esse o assunto do próximo capítulo: `JOIN`, o comando que junta tabela com tabela numa consulta só, aproveitando aquela chave estrangeira que a gente desenhou lá no primeiro capítulo desse módulo.

E depois de `JOIN`, tem mais uma peça que ainda falta: existe um jeito de calcular o total gasto por cliente sem perder a linha individual de cada pedido, ao contrário do que `GROUP BY` faz. Isso se chama window function, e fica pra mais pra frente.
