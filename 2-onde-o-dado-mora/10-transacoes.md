# SQL na prática: transações

No capítulo de CRUD a gente aprendeu a criar tabela, inserir linha, corrigir valor e apagar dado que não servia mais. Mas repara numa pergunta que aquele capítulo nunca respondeu: e se eu precisar rodar várias operações de escrita juntas, como se fossem uma coisa só, e uma delas falhar no meio do caminho? O que acontece com as que já tinham rodado antes do erro? Ficam valendo, mesmo incompletas? É exatamente esse buraco que esse capítulo fecha.

## O que é uma transação

Uma **transação** é um bloco de uma ou mais operações de escrita tratado como uma unidade só, tudo ou nada. Ou todas as operações dentro dela acontecem de verdade, ou nenhuma acontece. Não existe meio-termo: o banco nunca deixa parte da transação salva e parte descartada.

## Que problema isso resolve

O problema é o que se costuma chamar de escrita parcial: um conjunto de operações que deveriam acontecer juntas, mas só parte delas de fato acontece, geralmente porque algo deu errado no meio do caminho, uma queda de conexão, um valor inválido, uma trava do banco.

O exemplo clássico pra isso é a transferência bancária. Transferir dinheiro de uma conta pra outra é, na prática, duas operações: debitar o valor da conta de origem, e creditar esse mesmo valor na conta de destino. Imagina que o banco debita R$500 da conta de origem, e bem nesse instante o sistema cai, antes de creditar o valor na conta de destino. Se cada operação valesse por si só, esse dinheiro simplesmente sumiria: saiu de uma conta, e nunca chegou na outra. Ninguém quer um banco que funciona assim.

## ACID, rapidamente

Você provavelmente vai esbarrar com a sigla **ACID** quando o assunto é transação, então vale nomear rapidamente as quatro letras, sem se aprofundar em cada uma: **Atomicidade** (tudo ou nada, a que resolve diretamente o problema descrito acima), **Consistência** (a transação sempre leva o banco de um estado válido pra outro estado válido, nunca pra um estado que quebra alguma regra), **Isolamento** (transações rodando ao mesmo tempo não enxergam o resultado parcial umas das outras) e **Durabilidade** (depois que uma transação é confirmada, ela sobrevive mesmo se o banco cair logo em seguida).

A que interessa de verdade pra esse capítulo é a primeira, atomicidade. É ela que garante o "tudo ou nada" que resolve o problema da transferência bancária: ou as duas operações (débito e crédito) acontecem juntas, ou nenhuma delas fica valendo.

## Como seria sem transação

Por padrão, cada comando SQL que você roda já fica salvo assim que termina de executar. Isso se chama **autocommit**: não existe uma etapa separada de "confirmar", o comando já vale sozinho no instante em que roda. Isso funciona bem pra comando isolado, mas não tem como agrupar vários comandos autocommit e desfazer todos juntos se um deles no meio der errado. Uma vez que um comando rodou, ele já está salvo, ponto final, mesmo que o próximo comando (que deveria acontecer junto) falhe logo em seguida.

## A sintaxe: BEGIN, COMMIT e ROLLBACK

Uma transação começa com `BEGIN` (alguns bancos usam `START TRANSACTION`, mesmo efeito), que avisa o banco "os comandos daqui pra frente não são pra valer sozinhos ainda, segura tudo até eu mandar confirmar". Depois disso, você roda os comandos normalmente, `INSERT`, `UPDATE`, `DELETE`, o que precisar.

Pra confirmar de vez tudo que rodou desde o `BEGIN`, usa `COMMIT`. É só depois do `COMMIT` que as mudanças realmente ficam valendo, visíveis pra qualquer outra consulta no banco.

Pra desistir de tudo que rodou desde o `BEGIN`, usa `ROLLBACK`. O banco desfaz cada operação daquele bloco, como se nenhuma delas tivesse acontecido, mesmo que algumas já tivessem rodado sem erro antes do `ROLLBACK`.

```sql
BEGIN;

-- comandos de escrita aqui

COMMIT;    -- confirma tudo
-- ou
ROLLBACK;  -- desfaz tudo
```

## Trade-offs

Transação não é de graça. Enquanto ela está aberta, o banco costuma travar (lock) a linha ou a tabela que está sendo alterada, pra garantir que nenhuma outra operação mexa naquele mesmo dado no meio do caminho e gere inconsistência. Isso é necessário, mas cobra um preço: se você deixar uma transação aberta por muito tempo, sem dar `COMMIT` nem `ROLLBACK`, esse lock fica segurando qualquer outra operação que dependa daquele mesmo dado, criando fila e travando o sistema pra outras pessoas.

Vale mencionar rapidamente também que nem todo motor de armazenamento suporta transação do mesmo jeito. O próprio MySQL, um dos SGBDs que a gente listou lá no capítulo 2, teve historicamente dois motores de armazenamento diferentes: MyISAM, que não suportava transação, e InnoDB, que suporta, e que virou o padrão a partir do MySQL 5.5. PostgreSQL, o banco escolhido pra esse repositório, suporta transação de forma sólida desde sempre, então isso não é uma preocupação aqui, mas vale saber que esse tipo de diferença existe entre bancos.

## Exemplo prático

Lá no capítulo de JOIN, a Elisa Ferreira (cliente 5) apareceu como o cliente que nunca tinha feito nenhum pedido. Vamos usar ela pra ilustrar transação: ela finalmente compra dois produtos no mesmo checkout. Na simplificação didática desse repositório, onde cada pedido representa a compra de um produto só, isso vira dois `INSERT` na tabela `pedidos`, que precisam acontecer juntos. Se só um deles fosse gravado, o sistema mostraria pra Elisa que a compra deu certo, mas só metade do carrinho teria sido salva de verdade.

**Caminho feliz**, com `COMMIT`:

```sql
BEGIN;

INSERT INTO pedidos (id_pedido, id_cliente, data_pedido, valor_total, id_produto)
VALUES (107, 5, '2026-09-20', 150.00, 1);

INSERT INTO pedidos (id_pedido, id_cliente, data_pedido, valor_total, id_produto)
VALUES (108, 5, '2026-09-20', 45.00, 2);

COMMIT;
```

Os dois `INSERT` rodam sem erro, o `COMMIT` confirma os dois juntos, e a tabela `pedidos` ganha duas linhas novas: o pedido 107 (Fone de Ouvido) e o pedido 108 (Caneca Térmica), os dois do cliente 5.

**Caminho de erro**, com `ROLLBACK`: na semana seguinte, Elisa tenta comprar de novo, mas um bug no sistema reusa por engano um `id_pedido` que já existe, o 103, que já pertence a um pedido da Ana Souza:

```sql
BEGIN;

INSERT INTO pedidos (id_pedido, id_cliente, data_pedido, valor_total, id_produto)
VALUES (109, 5, '2026-09-25', 210.00, 3);

INSERT INTO pedidos (id_pedido, id_cliente, data_pedido, valor_total, id_produto)
VALUES (103, 5, '2026-09-25', 320.00, 3);
-- erro: duplicate key value violates unique constraint (id_pedido 103 já existe)

ROLLBACK;
```

O primeiro `INSERT` (pedido 109) roda sem problema nenhum. Mas o segundo falha, porque `id_pedido` é chave primária, e 103 já existe na tabela, apontando pra um pedido da Ana Souza. Mesmo o primeiro `INSERT` já tendo rodado dentro dessa transação, o `ROLLBACK` desfaz os dois juntos: o pedido 109 nunca chega a existir de verdade. A tabela `pedidos` volta a ter exatamente as oito linhas de antes desse bloco (as seis originais mais as duas confirmadas no `COMMIT` anterior), sem nenhum resquício da tentativa que falhou.

É esse o efeito prático da atomicidade: mesmo um comando que já rodou sem erro nenhum é desfeito, se outro comando do mesmo bloco falhar depois dele.

## Fechando esse capítulo

Com transação, fecha o último capítulo técnico desse módulo. Juntando tudo que veio desde o capítulo 1 (o que é banco relacional e SQL, como instalar um banco, consultar, agregar, juntar tabela, criar e modificar dado, subquery, CTE, window function, e agora transação), esse repositório já cobriu uma base sólida o suficiente de SQL pra você sair usando de verdade, num banco de verdade, com confiança de que o dado que você grava não fica pela metade se algo der errado no meio do caminho.
