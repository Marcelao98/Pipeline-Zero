# 2. Onde o dado mora

Módulo de banco de dados relacional e SQL. Cobre o que é um banco de dados relacional e por que ele existe, e depois entra na sintaxe de SQL na prática.

1. [Bancos de dados relacionais e SQL](01-bancos-de-dados-relacionais-e-sql.md) — o que é um banco de dados relacional, o vocabulário básico (tabela, linha, coluna, chave primária, chave estrangeira) e por que SQL existe.
2. [Escolhendo e instalando um banco](02-escolhendo-e-instalando-um-banco.md) — diferença entre SQL e SGBD, panorama dos principais SGBDs do mercado, e passo a passo de instalação do PostgreSQL.
3. [Consultando dado](03-consultando-dado.md) — `SELECT`, `WHERE`, `ORDER BY` e `LIMIT`, pra fazer perguntas simples ao banco e receber resposta.
4. [Agregando e agrupando dado](04-agregando-e-agrupando-dado.md) — `COUNT`, `SUM`, `GROUP BY` e `HAVING`, pra transformar linha em métrica resumida.
5. [Juntando tabelas](05-juntando-tabelas.md) — `JOIN`, pra cruzar dado que está espalhado em mais de uma tabela.
6. [Criando e modificando dado](06-criando-e-modificando-dado.md) — `CREATE TABLE`, `INSERT`, `UPDATE` e `DELETE`, pra criar estrutura e alterar dado, não só lê-lo.
7. [Subqueries](07-subqueries.md) — consulta dentro de outra consulta, pra responder pergunta que depende de um resultado intermediário calculado antes.
8. [CTE](08-cte.md) — `WITH`, um jeito de nomear passo intermediário e ler a consulta de cima pra baixo, em vez de aninhar subquery dentro de subquery.
9. [Window functions](09-window-functions.md) — `OVER`, `PARTITION BY` e `ORDER BY`, pra calcular métrica em cima de um grupo de linha sem perder a linha individual.
10. [Transações](10-transacoes.md) — `BEGIN`, `COMMIT` e `ROLLBACK`, pra tratar várias operações de escrita como uma unidade só, tudo ou nada.
11. [Pra onde ir daqui](11-proximos-passos.md) — fechamento do módulo: recursos pra continuar estudando, e como sair do tutorial e partir pra um projeto próprio.
