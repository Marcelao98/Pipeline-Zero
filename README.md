# Engenharia de Dados em Português

## Por que mais um "tutorial" de engenharia de dados?

Essa é a pergunta óbvia, e ela merece uma resposta honesta.

Eu não sou formado em Ciência da Computação. Sou engenheiro eletricista, e decidi entrar no mundo de dados por conta própria. Estudei, e ainda estudo, Python, SQL, Airflow, Git, e agora estou avançando em nuvem. Tenho projetos próprios rodando. Mas o caminho até aqui foi mais difícil do que precisava ser, e não por falta de conteúdo. Pelo contrário: **tem conteúdo demais**. O problema é outro.

### O problema não é a falta de material. É a falta de mapa.

Se você fala inglês fluente (e eu falo), a internet gringa tem uma quantidade absurda de cursos, blogs, vídeos e documentações sobre engenharia de dados. Só que isso vira um novo problema: ninguém te entrega um "comece por aqui". Você vira garimpeiro. Um vídeo indiano ótimo sobre Airflow, um post de blog perdido sobre modelagem de dados, um curso caro que promete tudo e entrega pouco. Você aprende, mas aprende os pedaços soltos, sem saber como eles se conectam.

Eu vivi isso. Virei madrugada inteira assistindo vídeo de criador indiano no YouTube, ótimos, de verdade, tentando entender um conceito que hoje eu consigo explicar em duas páginas. E não foi porque faltou inteligência ou disciplina da minha parte. Foi porque não existia um mapa. Acredito que ninguém deveria precisar virar madrugada sozinho pra aprender o básico do básico, e é exatamente isso que esse projeto tenta resolver pra quem vier depois de mim.

E tem um segundo problema, mais grave: **para quem não tem inglês fluente, essa barreira nem chega a ser "difícil de organizar", é uma parede**. A pessoa simplesmente não acessa 90% do que existe de bom sobre o assunto. E eu não acho isso certo. Conhecimento técnico de qualidade não deveria depender de você falar outro idioma.

### A proposta desse projeto

Este repositório é a minha tentativa de construir o mapa que eu não tive.

Alguns princípios que guiam como isso vai ser feito:

- **Totalmente em português.** Não é tradução automática de conteúdo gringo, é explicação escrita pensando em quem tem português como idioma nativo.
- **Prioridade máxima para conteúdo em português.** Sempre que existir um material bom em português (vídeo, artigo, curso), ele vai ser priorizado e linkado aqui.
- **Quando não existir substituto em português, eu linko o conteúdo em inglês mesmo assim.** Não faz sentido esconder um recurso bom só porque está no idioma errado. Quando possível, pretendo entrar em contato com os criadores desses conteúdos (incluindo criadores indianos, que produzem um material técnico excelente sobre engenharia de dados) para pedir permissão de tradução e upload legendado ou dublado.
- **Narrativa, não lista de tecnologias.** Cada módulo conta uma história: por que aquela ferramenta ou conceito surgiu, que problema ela resolveu, o que existia antes e por que não era suficiente. Não é "aprenda SQL porque sim", é "veja por que SQL precisou existir".
- **Conhecimento deveria ser gratuito.** Não é discurso bonito, é o princípio por trás de cada decisão desse projeto: se existe uma forma de tirar alguém do zero sem cobrar nada por isso, essa é a forma que eu vou escolher.
- **Ensino técnico não precisa ser sem graça.** Sempre que fizer sentido, esse guia vai usar analogia de coisa que eu gosto de verdade (culinária, música, jogo eletrônico, RPG de mesa, entre outras) pra explicar conceito técnico. Isso é de propósito, não enfeite: acho que aprender fica mais fácil, e mais gostoso, quando o conceito gruda em alguma coisa que já faz sentido pra você.

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
├── 2-onde-o-dado-mora/
└── 3-python/
```

- **[1-que-porra-e-essa/](1-que-porra-e-essa/README.md)** é o módulo zero, o ponto de partida. Ele responde: o que é engenharia de dados, como ela se diferencia de análise de dados e ciência de dados, qual o ciclo de vida que todo dado percorre numa empresa, e um roadmap prático de por onde começar a estudar.
- **[2-onde-o-dado-mora/](2-onde-o-dado-mora/README.md)** é o módulo de banco de dados relacional e SQL. Cobre o que é um banco de dados relacional e por que ele existe, e depois entra na sintaxe de SQL na prática.
- **[3-python/](3-python/README.md)** é o módulo de Python. Um resumo enxuto, focado só no que serve pra engenharia de dados: fundamentos da linguagem e Python aplicado a dado. Não é um curso completo de Python.

### Estado atual do conteúdo

- **[1-que-porra-e-essa/](1-que-porra-e-essa/README.md)**: completo.
- **[2-onde-o-dado-mora/](2-onde-o-dado-mora/README.md)**: completo.
- **[3-python/](3-python/README.md)**: Bloco 1 (fundamento da linguagem) completo. Bloco 2 (Python aplicado a dado) ainda não escrito.

### Próximos módulos planejados

Ainda não escritos, mas já com o lugar deles reservado no roadmap:

- Excel (fórmulas, PROCV/PROCX, tabela dinâmica, gráfico)
- Git e controle de versão
- Orquestração (Airflow)
- Nuvem (cloud)
- Lista curada de recursos e links úteis em português

## Transparência sobre como esse conteúdo é escrito

Isso também merece ser dito com a mesma honestidade do resto desse README: o texto desse repositório não é escrito inteiramente à mão, mas também não é gerado sem controle nenhum. Ele é escrito com assistência de IA, através de um processo manual, capítulo por capítulo.

O processo funciona assim: a decisão do que ensinar, em que ordem, com qual exemplo, é sempre minha, tomada antes de qualquer texto ser gerado. A IA entra na etapa de execução, como ferramenta de escrita, mas cada capítulo é lido e revisado por mim, linha por linha, antes de ir pro ar, e ainda passa por uma camada de revisão adicional depois disso.

Por que fazer assim, e não escrever tudo manualmente do zero? Honestamente, porque escrever cada capítulo inteiramente à mão consumiria muito mais tempo do que eu tenho disponível pra manter esse projeto vivo, sozinho, nas horas vagas. Esse processo é o que torna viável esse repositório continuar crescendo.

Pra ser direto sobre a ferramenta: eu uso o Claude Code pra escrever. Se você tiver qualquer dúvida sobre como esse processo funciona, abre uma issue e eu respondo.

E um lembrete importante, nesse mesmo tom: IA é uma ferramenta extremamente útil, mas é só isso, uma ferramenta. Ela precisa de direcionamento humano o tempo todo, e não substitui a decisão de conteúdo nem o julgamento de qualidade, que continuam sendo meus, do início ao fim.

## Como contribuir

Esse repositório é público de propósito, e a ideia é que ele cresça de forma colaborativa. A área de dados é grande demais para uma pessoa só documentar com profundidade sozinha. Um guia formal de contribuição ainda não existe, mas se você quiser sugerir algo, corrigir algo ou trocar ideia, abra uma issue.

## Status

🚧 Projeto em construção, e por natureza, sempre vai estar. Este é o pipeline zero, o começo de tudo.
