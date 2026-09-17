# SQL na prática: criando e modificando dado

No capítulo anterior a gente aprendeu a juntar tabela com tabela usando `JOIN`. Somando isso com o que veio antes (`SELECT`, `WHERE`, `ORDER BY`, `LIMIT`, `COUNT`, `SUM`, `GROUP BY`, `HAVING`), dá pra dizer que a gente já sabe ler dado de banco relacional de verdade. Só que repara numa coisa: em nenhum momento, em nenhum dos quatro capítulos anteriores, a gente criou uma tabela do zero, inseriu uma linha nova, corrigiu um valor errado ou apagou algo que não servia mais. A gente só leu dado que já existia, pronto, esperando ser consultado. Chegou a hora de aprender o outro lado: criar e modificar dado.

## CREATE TABLE: criando uma tabela do zero

Toda tabela que a gente usou até aqui (`clientes`, `pedidos`, `produtos`) já vinha pronta, como se tivesse surgido do nada. Na prática, alguém precisou definir a estrutura dela antes de qualquer linha existir: quais colunas ela tem, e que tipo de dado cada coluna guarda. É pra isso que existe o `CREATE TABLE`.

Vamos criar uma tabela nova pra loja: `avaliacoes`, guardando a avaliação que um cliente deixa sobre um produto que comprou.

```sql
CREATE TABLE avaliacoes (
    id_avaliacao INT PRIMARY KEY,
    id_cliente INT,
    id_produto INT,
    nota INT,
    comentario TEXT,
    data_avaliacao DATE
);
```

Repara na estrutura: cada linha dentro dos parênteses é uma coluna, seguida do tipo de dado que ela vai guardar. `INT` é número inteiro, sem casa decimal, usado aqui em `id_avaliacao`, `id_cliente`, `id_produto` e `nota`. `TEXT` é texto livre, de tamanho variável, usado no `comentario`. `DATE` é data, usado em `data_avaliacao`. Existe também o `DECIMAL`, pra número com casa decimal, que a gente já vem usando desde o capítulo 2 em `valor_total` e `preco`, só que essa tabela aqui não precisou dele. Não vou entrar em todos os tipos de dado que existem, esses já cobrem a maioria do que você vai precisar no início.

E o `PRIMARY KEY` depois de `id_avaliacao` é a mesma chave primária que a gente já conhece desde o capítulo 1: marca aquela coluna como o identificador único de cada linha dessa tabela.

Feito isso, a tabela `avaliacoes` existe, mas está vazia. Nenhuma linha nela ainda.

## INSERT: adicionando linha nova

Com a tabela criada, o próximo passo é colocar dado dentro dela. É pra isso que existe o `INSERT`.

```sql
INSERT INTO avaliacoes (id_avaliacao, id_cliente, id_produto, nota, comentario, data_avaliacao)
VALUES (1, 1, 1, 5, 'Produto excelente, chegou rápido', '2026-09-20');
```

A estrutura é direta: depois de `INSERT INTO nome_da_tabela`, você lista as colunas que vai preencher, e depois de `VALUES`, os valores correspondentes, na mesma ordem. Aqui, a Ana Souza (`id_cliente = 1`) deixou nota 5 pro Fone de Ouvido (`id_produto = 1`), com um comentário e uma data.

Depois desse `INSERT`, a tabela `avaliacoes` já tem uma linha. Rodar o mesmo comando de novo, com um `id_avaliacao` diferente, adicionaria outra linha, sem apagar a primeira.

## UPDATE: alterando dado que já existe

Às vezes o dado que já está na tabela precisa ser corrigido. Imagina que o `valor_total` do pedido 102, lá na tabela `pedidos`, foi registrado errado, e o valor certo era outro. É pra isso que existe o `UPDATE`.

```sql
UPDATE pedidos
SET valor_total = 95.00
WHERE id_pedido = 102;
```

`UPDATE` diz qual tabela alterar, `SET` diz qual coluna muda e pra qual valor novo, e `WHERE` diz qual linha (ou linhas) recebe essa mudança.

E aqui vale um alerta sério: o `WHERE` não é opcional na prática, mesmo sendo opcional na sintaxe. Se eu rodasse esse mesmo `UPDATE` sem o `WHERE`, o banco não erraria, não perguntaria "tem certeza?", ele simplesmente aplicaria `valor_total = 95.00` em toda linha da tabela `pedidos`, apagando de vez o valor correto que existia em cada uma. `UPDATE` sem `WHERE` altera a tabela inteira, sempre.

## DELETE: removendo linha

`DELETE` remove linha de uma tabela. A sintaxe segue o mesmo raciocínio do `UPDATE`, só que sem o `SET`, porque não tem valor novo pra colocar, só a linha que some.

```sql
DELETE FROM avaliacoes
WHERE id_avaliacao = 1;
```

Isso remove a avaliação que a gente acabou de inserir.

Agora o alerta fica ainda mais sério do que no `UPDATE`. `DELETE` sem `WHERE` não altera a tabela inteira, ele apaga a tabela inteira, linha por linha, sem deixar rastro, sem confirmação, sem "tem certeza?". É provavelmente o erro mais perigoso e mais comum que quem tá começando em SQL comete: esquecer o `WHERE` num `DELETE` e, num segundo, perder um monte de dado que não tem como recuperar só rodando outro comando. Antes de rodar `UPDATE` ou `DELETE` de verdade, principalmente `DELETE`, vale sempre a pena reler o `WHERE` uma segunda vez, ou primeiro rodar um `SELECT` com aquele mesmo `WHERE`, só pra confirmar exatamente quais linhas vão ser afetadas antes de mudar de comando.

## Cuidado extra quando o assunto é alterar e apagar dado de verdade

Vale abrir um parêntese curto aqui. Tudo que a gente viu nesse capítulo funciona, mas no mundo real, alterar ou apagar dado direto numa base de produção (aquela que o sistema de verdade usa, não um ambiente de teste) não costuma ser feito assim, no improviso. Existe prática de segurança em volta disso: testar o comando antes num ambiente separado, que existe justamente pra isso; ter backup recente, pra sempre existir um jeito de voltar atrás se algo sair errado; e pedir pra outra pessoa revisar o comando antes de rodar, principalmente quando ele muda muita linha de uma vez. Não vou entrar em detalhe de como cada uma dessas práticas funciona agora, só fica registrado que elas existem, e que existem por um motivo muito claro: `UPDATE` e `DELETE` não têm desfazer.

## Fechando esse capítulo

Com `CREATE TABLE`, `INSERT`, `UPDATE` e `DELETE`, fecha um ciclo importante: agora a gente sabe tanto ler dado que já existe quanto criar e modificar dado do zero. Juntando com tudo dos capítulos anteriores (`SELECT`, `WHERE`, `ORDER BY`, `LIMIT`, `COUNT`, `SUM`, `GROUP BY`, `HAVING`, `JOIN`), isso já forma uma base sólida de SQL.

Mas repara que "base sólida" não é "SQL inteiro". Ainda tem chão pela frente dentro desse mesmo módulo: coisa como CTE (uma forma de organizar consulta complexa em pedaço menor e mais legível), window function (que a gente já deixou como gancho lá no capítulo 3, calcular métrica sem perder a linha individual) e subquery (consulta dentro de outra consulta). Esses assuntos ainda vão virar capítulo aqui dentro de `2-onde-o-dado-mora/`, antes da gente seguir pro próximo módulo do repositório.
