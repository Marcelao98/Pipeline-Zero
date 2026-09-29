# SQL na prática: CTE (Common Table Expression)

No fechamento do capítulo anterior ficou um problema em aberto: subquery resolve pergunta que depende de um resultado intermediário, mas subquery aninhada demais custa legibilidade. Duas camadas você acompanha sem esforço, três ou quatro já viram um quebra-cabeça de parênteses. É exatamente esse buraco que a CTE (Common Table Expression) preenche.

## O que é uma CTE

Uma **CTE** é um bloco de consulta nomeado e temporário, criado com `WITH`, que existe só durante o tempo daquela consulta específica. Você dá um nome pra ele, escreve o `SELECT` que ele representa, e depois pode usar esse nome como se fosse uma tabela normal no resto da consulta.

A diferença central pra subquery não está no que ela calcula, é em como você lê. Subquery força você a ler de fora pra dentro, porque o `SELECT` de dentro fica encaixado dentro do `WHERE` do `SELECT` de fora. CTE inverte isso: você lê de cima pra baixo, um passo de cada vez, cada um já resolvido antes do próximo começar.

## Que problema isso resolve

O cálculo que a CTE resolve é o mesmo que a subquery já resolvia: uma pergunta que depende de um resultado intermediário, calculado dentro do próprio banco, antes de comparar ou filtrar alguma coisa em cima dele. O que muda é como esse passo intermediário fica organizado na consulta. Em vez de esconder ele dentro de parênteses aninhados, a CTE dá um nome pra ele, e deixa ele declarado antes da consulta principal começar, sem obrigar quem lê a montar o quebra-cabeça de fora pra dentro que a gente viu no capítulo passado.

## A sintaxe do WITH

A estrutura básica é essa:

```sql
WITH nome_da_cte AS (
    SELECT ...
)
SELECT ...
FROM nome_da_cte;
```

`WITH nome_da_cte AS (...)` declara o bloco e dá um nome pra ele. Depois disso, a consulta principal pode usar esse nome em qualquer lugar onde usaria uma tabela normal, num `FROM`, num `JOIN`, no que for.

Dá pra declarar mais de uma CTE na mesma consulta, uma depois da outra, separadas por vírgula, e uma CTE posterior pode inclusive usar o resultado de uma CTE anterior:

```sql
WITH primeira_cte AS (
    SELECT ...
),
segunda_cte AS (
    SELECT ...
    FROM primeira_cte
)
SELECT ...
FROM segunda_cte;
```

Isso é o que permite quebrar um problema com vários passos intermediários numa sequência de blocos nomeados, cada um lido depois que o anterior já foi entendido.

## Trade-off: CTE é sobre legibilidade, não performance

Vale desfazer uma expectativa antes que ela se forme: CTE não roda mais rápido que a subquery equivalente, na maioria dos bancos. O trabalho que o banco precisa fazer pra calcular aquele resultado intermediário é basicamente o mesmo, dando nome a ele ou não. Alguns bancos, inclusive, calculam e guardam o resultado da CTE temporariamente antes de seguir pro resto da consulta, o que ocasionalmente pode deixar ela mais lenta que a subquery equivalente, nunca mais rápida por padrão.

O ganho real de CTE é outro: legibilidade, tanto pra você quanto pra quem for revisar ou dar manutenção nessa consulta depois. Não é sobre fazer o banco trabalhar menos, é sobre fazer a pessoa lendo o código entender mais rápido o que está acontecendo.

Vale também registrar que existe CTE recursiva, um tipo especial que consegue referenciar a si mesma, útil pra percorrer estrutura hierárquica (tipo uma árvore de categoria com subcategoria dentro de subcategoria). Isso foge do escopo desse capítulo, mas fica registrado que existe.

## Exemplo prático

Vamos reescrever os dois exemplos do capítulo anterior, usando CTE em vez de subquery, com o mesmo dataset de clientes, pedidos e produtos.

**Equivalente à subquery escalar**: quais pedidos tiveram valor acima da média geral de todos os pedidos?

```sql
WITH media_pedidos AS (
    SELECT AVG(valor_total) AS media
    FROM pedidos
)
SELECT pedidos.id_pedido, pedidos.valor_total
FROM pedidos
CROSS JOIN media_pedidos
WHERE pedidos.valor_total > media_pedidos.media;
```

A CTE `media_pedidos` calcula a média de todos os pedidos primeiro, `160.82` (aproximando as casas decimais), e dá o nome `media` pra essa coluna. Repara num tipo de `JOIN` que não apareceu no capítulo sobre junção de tabela: `CROSS JOIN` combina toda linha de uma tabela com toda linha da outra (o chamado produto cartesiano), sem nenhuma condição de correspondência envolvida. Aqui ele funciona bem porque `media_pedidos` tem só uma linha, então o resultado do `CROSS JOIN` é simplesmente uma cópia de cada linha de `pedidos`, com a média grudada do lado. Repara que não sobrou nenhum parêntese dentro do `WHERE`: a comparação virou `pedidos.valor_total > media_pedidos.media`, direta, sem aninhamento.

Resultado, idêntico ao do capítulo anterior:

| id_pedido | valor_total |
|---|---|
| 103 | 320.00 |
| 105 | 210.00 |

**Equivalente à subquery de lista**: quais clientes compraram algum produto da categoria Eletrônicos? Essa é a mesma pergunta que, no capítulo anterior, também apareceu numa versão aninhada, subquery dentro de subquery, exatamente o tipo de consulta difícil de acompanhar que motivou esse capítulo.

```sql
WITH produtos_eletronicos AS (
    SELECT id_produto
    FROM produtos
    WHERE categoria = 'Eletrônicos'
),
clientes_compradores AS (
    SELECT DISTINCT pedidos.id_cliente
    FROM pedidos
    JOIN produtos_eletronicos ON pedidos.id_produto = produtos_eletronicos.id_produto
)
SELECT clientes.nome
FROM clientes
JOIN clientes_compradores ON clientes.id_cliente = clientes_compradores.id_cliente;
```

Repara na diferença de estrutura. Primeiro, `produtos_eletronicos` isola os produtos da categoria Eletrônicos. Depois, `clientes_compradores` usa esse resultado pra achar quem comprou algum desses produtos. Por último, a consulta principal só junta `clientes` com esse resultado já pronto. Cada passo lê de cima pra baixo, um dependendo só do anterior, sem nenhum parêntese aninhado dentro de outro. O `DISTINCT` dentro de `clientes_compradores` é só um cuidado geral, pra evitar duplicar um cliente que tivesse comprado mais de um produto elegível, mesmo não fazendo diferença nesse dataset específico.

Resultado, também idêntico ao do capítulo anterior:

| nome |
|---|
| Ana Souza |
| Diego Martins |

Mesmo resultado dos dois exemplos do capítulo passado, mas repara como a leitura fica mais direta: cada bloco tem um nome que já entrega o que ele representa, e você acompanha o raciocínio de cima pra baixo, sem precisar guardar camada nenhuma na cabeça.

## Fechando esse capítulo

Com CTE, a gente ganha um jeito de organizar cálculo intermediário em passo nomeado e legível, sem abrir mão do que subquery já resolvia. O ganho é de leitura, não de velocidade, e isso já vale a troca na maioria das consultas que crescem além de uma ou duas linhas.

Ainda sobra um tipo de pergunta que nem subquery nem CTE, do jeito que a gente viu até aqui, resolvem direito: calcular uma métrica (tipo total acumulado, ou posição num ranking) sem perder a linha individual de cada registro, ao contrário do que `GROUP BY` faz. Isso já foi deixado como gancho lá no capítulo de agregação, e chegou a hora de resolver: window functions, assunto do próximo capítulo.
