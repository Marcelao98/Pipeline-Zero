# Módulo concluído: pra onde ir daqui

Se você chegou até aqui, passou pela trilha inteira de SQL desse módulo: consultar dado, agregar e agrupar, juntar tabela, criar e modificar dado, subquery, CTE, window function, e transação. Isso já é uma base de verdade, não decoreba de comando solto. Chegou a hora de falar sobre o que vem depois.

## Isso foi só o básico do básico

Preciso ser direto aqui: esse módulo cobriu o básico do básico de SQL. Não dá, e nunca foi a intenção, ensinar SQL por completo num punhado de capítulos. Ficou faltando um monte de coisa (índice, otimização de consulta, tipo de dado mais avançado, stored procedure, trigger, só pra citar alguns), e isso é proposital. A proposta desse projeto inteiro, desde o primeiro módulo, sempre foi tirar você do zero, te dar o mapa e o raciocínio por trás de cada ferramenta, não formar um especialista dentro de um repositório de markdown. Especialista se forma praticando, com tempo, com projeto de verdade, não lendo capítulo.

## Recursos pra continuar estudando

Com essa base, os recursos abaixo levam você bem mais longe do que esse módulo conseguiu:

- **[MySQL – Curso em Vídeo, Gustavo Guanabara](https://www.cursoemvideo.com/curso/mysql/)**: curso completo, gratuito, com certificado, referência clássica de quem estuda programação em português.
- **[SQL para Iniciantes – LearnSQL.com.br](https://learnsql.com.br/curso/sql-para-iniciantes/)**: plataforma interativa em português, pra praticar direto no navegador.
- **[Módulo Gratuito de SQL Analytics – Data Science Academy](https://blog.dsacademy.com.br/sql_analytics/)**: módulo gratuito de uma escola brasileira de dados, com foco mais analítico.
- **[SQL: Uma abordagem para bancos de dados Oracle](https://archive.org/details/sql-uma-abordagem-para-bancos-de-dados-oracle)**, de Wes Oliveira: livro completo e gratuito. Só um aviso: os exemplos são voltados pra Oracle especificamente, então a sintaxe pode variar um pouco do que a gente usou aqui em cima de PostgreSQL, mas os fundamentos batem igual.
- **[SQLZoo](https://sqlzoo.net/)**: site de exercício interativo, pergunta a pergunta. A interface é em inglês, mas o conteúdo em si é código SQL, que é igual em qualquer idioma.

Por último, dois recursos em inglês, deixados por último de propósito. Estão nessa lista porque são bons o suficiente pra valer a exceção, mas você vai precisar de algum inglês pra acompanhar:

- **[Data with Baraa – SQL Full Course for Beginners (30 Hours)](https://www.youtube.com/watch?v=SSKVgrwhzus)**
- **[freeCodeCamp – curso de SQL](https://www.youtube.com/watch?v=HXV3zeQKqGY)**: esse aqui, especificamente, foi o que eu usei pra começar a aprender SQL.

## Ler é uns 20% do aprendizado

Um conselho antes de qualquer link: vivemos numa era onde escrever código fica cada vez mais fácil, por causa de IA. E é exatamente por isso que entender o conceito por trás do código fica mais importante, não menos. Qualquer um consegue pedir pra uma IA escrever uma consulta SQL hoje. Poucos conseguem explicar por que aquela consulta funciona, o que ela custa, e quando ela é a ferramenta errada pro problema.

E aqui vai o ponto principal: ler capítulo, assistir vídeo, isso é uns 20% do aprendizado, não mais que isso. A maior parte vem de praticar, de errar, de ficar preso numa consulta que não funciona e ter que entender o porquê. Nenhum material, nem esse repositório, nem os cinco links acima, substitui isso.

## Progressão prática sugerida

Comece pequeno. Pega um exercício simples de qualquer um dos recursos acima, e tenta escrever a sintaxe você mesmo, no seu próprio editor SQL, do zero, sem colar pronto. Mas não trava só nisso. Reescrever exercício alheio é ótimo pra pegar o jeito da sintaxe, mas não é o mesmo que resolver um problema seu, com um dado que você escolheu. Assim que você tiver alguma familiaridade, o próximo passo é sair do exercício guiado e começar a construir alguma coisa sua.

## Ideias pra um projeto próprio

Não precisa de nada grandioso. Inventa um cenário simples e monta tabela em cima dele: "eu sou aluno numa escola, quero modelar turma, matéria e nota". "Eu tenho uma loja pequena, quero modelar cliente, produto e pedido" (aliás, bem parecido com o que a gente usou de exemplo nesse módulo inteiro). O cenário importa menos do que o hábito de pensar em tabela, relação e consulta com um problema seu na cabeça.

Se você já trabalha e usa bastante planilha de Excel, cheia de PROCV, fórmula empilhada, aba dependendo de aba, aqui vai uma sugestão concreta: pega uma dessas planilhas e tenta recriar aquelas mesmas tabelas dentro de um banco SQL. Modela aquilo que você já conhece de cor. Você vai sentir na pele a diferença entre planilha e banco relacional, porque vai estar resolvendo um problema que você já resolvia de outro jeito, só que agora com a ferramenta certa.

## Meu projeto: o Riverflow

Quando eu comecei a aprender SQL, fiz um bocado de exercício desses recursos aí de cima. Mas o que realmente consolidou o aprendizado foi um projeto que criei adaptado da minha própria realidade de estágio: uma simulação do ecossistema de uma estação de tratamento de água, com indicadores voltados pra manutenção e confiabilidade de equipamento.

É um projeto de engenharia de dados de ponta a ponta, com três camadas. Primeiro, simulação em Python, gerando dado sintético de falha de equipamento usando distribuição de Weibull, e priorização de manutenção usando princípio de Pareto. Depois, engenharia em SQL, modelando os dados em Star Schema e calculando indicador de confiabilidade (MTBF, MTTR, disponibilidade) através de views. Por último, visualização em Tableau, transformando aquele indicador calculado em dashboard.

O repositório inteiro está aberto aqui: **[Riverflow](https://github.com/Marcelao98/Riverflow)**.

## Fechando esse módulo

Agora é sua vez. Pega alguma referência da sua própria vida, o trabalho que você já faz, o hobby que você tem, a planilha que você já usa, e constrói em cima. Pode inclusive usar o Riverflow como inspiração, já que ele é bem focado em SQL. Começa com tutorial, tudo bem, mas não fica só nisso: parte pra construir com qualquer dado que você já tenha acesso, mesmo que simples.

E se você for encarar um projeto próprio, saiba que vai ter apoio. Hoje esse repositório sou literalmente só eu, sozinho, cuidando disso nas horas vagas, mas se você quiser trocar ideia, mostrar o que construiu, ou travar em alguma dúvida no caminho, abre uma issue. Bora construir.
