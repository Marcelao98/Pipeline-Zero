# Engenharia de Dados em Português

## Por que mais um "tutorial" de engenharia de dados?

Essa é a pergunta óbvia, e ela merece uma resposta honesta.

Eu não sou formado em Ciência da Computação. Sou engenheiro eletricista, e decidi entrar no mundo de dados por conta própria. Estudei, e ainda estudo, Python, SQL, Airflow, Git, e agora estou avançando em nuvem. Tenho projetos próprios rodando. Mas o caminho até aqui foi mais difícil do que precisava ser, e não por falta de conteúdo. Pelo contrário: **tem conteúdo demais**. O problema é outro.

### O problema não é a falta de material. É a falta de mapa.

Se você fala inglês fluente (e eu falo), a internet gringa tem uma quantidade absurda de cursos, blogs, vídeos e documentações sobre engenharia de dados. Só que isso vira um novo problema: ninguém te entrega um "comece por aqui". Você vira garimpeiro. Um vídeo indiano ótimo sobre Airflow, um post de blog perdido sobre modelagem de dados, um curso caro que promete tudo e entrega pouco. Você aprende, mas aprende os pedaços soltos, sem saber como eles se conectam.

E tem um segundo problema, mais grave: **para quem não tem inglês fluente, essa barreira nem chega a ser "difícil de organizar", é uma parede**. A pessoa simplesmente não acessa 90% do que existe de bom sobre o assunto. E eu não acho isso certo. Conhecimento técnico de qualidade não deveria depender de você falar outro idioma.

### A proposta desse projeto

Este repositório é a minha tentativa de construir o mapa que eu não tive.

Alguns princípios que guiam como isso vai ser feito:

- **Totalmente em português.** Não é tradução automática de conteúdo gringo, é explicação escrita pensando em quem tem português como idioma nativo.
- **Prioridade máxima para conteúdo em português.** Sempre que existir um material bom em português (vídeo, artigo, curso), ele vai ser priorizado e linkado aqui.
- **Quando não existir substituto em português, eu linko o conteúdo em inglês mesmo assim.** Não faz sentido esconder um recurso bom só porque está no idioma errado. Quando possível, pretendo entrar em contato com os criadores desses conteúdos (incluindo criadores indianos, que produzem um material técnico excelente sobre engenharia de dados) para pedir permissão de tradução e upload legendado ou dublado.
- **Narrativa, não lista de tecnologias.** Cada módulo conta uma história: por que aquela ferramenta ou conceito surgiu, que problema ela resolveu, o que existia antes e por que não era suficiente. Não é "aprenda SQL porque sim", é "veja por que SQL precisou existir".
- **Conhecimento deveria ser gratuito.** Esse é o princípio por trás de tudo isso.

### O caos que esse projeto tenta resolver

Se você está começando agora, provavelmente já sentiu isso: é Python, mas também é SQL, mas tem Airflow, mas também tem dbt, é AWS mas também tem Azure, mas tem Databricks, mas tem Snowflake, e aí você para e pensa **"por onde eu começo, e por que existem tantas ferramentas fazendo, aparentemente, a mesma coisa?"**

A resposta é: elas não fazem a mesma coisa, e entender a diferença entre elas é o que separa quem decora comando de quem realmente entende engenharia de dados. E hoje, com IA, escrever código ficou fácil. O que continua difícil, e o que continua importando, é saber *por que* aquele código existe, *que problema* ele resolve, e *quando* você não deveria estar usando aquela ferramenta.

É isso que esse projeto vai tentar construir: não uma pilha de tutoriais, mas uma linha narrativa que explica a evolução da engenharia de dados, módulo por módulo, para que no final você não tenha só "aprendido as ferramentas", você tenha entendido o raciocínio por trás delas.

## Como o conteúdo está organizado

A narrativa vem primeiro, módulo por módulo, contando a evolução da área do jeito que faz sentido pra quem está aprendendo: conceito antes de ferramenta, sempre perguntando "que problema isso resolve" antes de "como eu uso isso". Depois, conforme o repositório crescer, um glossário interconectado deve permitir consulta rápida a qualquer conceito já explicado nos módulos, sem precisar reler tudo.

Os diagramas deste repositório usam [Mermaid](https://mermaid.js.org/), que renderiza nativamente tanto no GitHub quanto no Obsidian, direto do texto do markdown, sem precisar de imagem exportada.

### Estrutura atual

```
.
├── README.md
├── 1-que-porra-e-essa/
└── 2-onde-o-dado-mora/
```

- **[1-que-porra-e-essa/](1-que-porra-e-essa/README.md)** é o módulo zero, o ponto de partida. Ele responde: o que é engenharia de dados, como ela se diferencia de análise de dados e ciência de dados, qual o ciclo de vida que todo dado percorre numa empresa, e um roadmap prático de por onde começar a estudar.
- **[2-onde-o-dado-mora/](2-onde-o-dado-mora/README.md)** é o módulo de banco de dados relacional e SQL. Cobre o que é um banco de dados relacional e por que ele existe, e depois entra na sintaxe de SQL na prática.

### Próximos módulos planejados

Ainda não escritos, mas já com o lugar deles reservado no roadmap:

- Python (um resumo enxuto de lógica e sintaxe, não um curso completo)
- Git e controle de versão
- Orquestração (Airflow)
- Nuvem (cloud)
- Lista curada de recursos e links úteis em português

## Como contribuir

Esse repositório é público de propósito, e a ideia é que ele cresça de forma colaborativa. A área de dados é grande demais para uma pessoa só documentar com profundidade sozinha. Um guia formal de contribuição ainda não existe, mas se você quiser sugerir algo, corrigir algo ou trocar ideia, abra uma issue.

## Status

🚧 Projeto em construção, e por natureza, sempre vai estar. Este é o pipeline zero, o começo de tudo.
