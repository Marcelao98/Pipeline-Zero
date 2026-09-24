# Analogias narrativas do Pipeline Zero

Documento de referência para uso interno (chat de brainstorm geral, chat de instrução, Claude Code). Não é conteúdo de capítulo pronto, é o mapa das decisões de analogia tomadas até aqui, com status de cada uma.

## 1. Analogia mestra do curso: água e encanamento

Dado é, na prática, qualquer coisa que pode ser levada, analisada e transformada — poderia ser água, eletricidade, gás pressurizado. A analogia escolhida é água, porque o nome do próprio projeto já entrega o resto sozinho: uma *pipeline* é, literalmente, um encanamento. Engenheiro de dados é quem constrói e mantém encanamento.

Mapeamento com o ciclo de vida do dado já existente no módulo 1 (capítulo 2: Geração → Armazenamento → Ingestão → Transformação → Disponibilização):

| Etapa do ciclo | Equivalente na analogia |
|---|---|
| Geração | Fontes de água (chuva, rio, poço artesiano) — qualidade e volume variam por fonte |
| Ingestão | Captação, bombas |
| Armazenamento | Reservatório |
| Transformação | Estação de tratamento de água ("tratar dado" e "tratar água" é literalmente o mesmo verbo) |
| Disponibilização | Rede de distribuição, a torneira na casa de alguém |

Conceitos que ganham clareza de graça com essa analogia:
- **Data lake** = represa de água bruta, sem tratamento, de qualquer fonte. Não se bebe direto dali.
- **Data warehouse** = reservatório já tratado, estruturado, pronto pro consumo.
- **Data lakehouse** = tentativa de ter as duas coisas na mesma infraestrutura.

**Status:** escrita no capítulo 2 do módulo `1-que-porra-e-essa/` (ciclo de vida), como camada por cima do exemplo da loja online, que continua sendo o caso concreto. Cada uma das cinco etapas ganhou a imagem correspondente da tabela acima; na etapa de armazenamento, data lake (represa) e data warehouse (reservatório tratado) substituíram a explicação literal anterior. A seção "o ciclo não é uma linha reta" ganhou uma comparação curta com o ciclo da água. Undercurrents ficaram de fora da metáfora, de propósito. Data lakehouse não entrou no texto. Capítulo 1 do mesmo módulo ainda sem a analogia (texto enviado, aplicação pendente).

**Regra de uso:** essa analogia serve para explicar *dado e arquitetura de dado*, não ferramentas específicas. Não deve ser esticada para dentro do módulo de Python (ver seção 3).

## 2. Módulo `2-onde-o-dado-mora/` (SQL): reservatório e válvula

Caso particular da analogia mestra — o reservatório é a etapa de armazenamento do encanamento maior.

- Banco de dados relacional = reservatório local (de uma casa, de uma empresa), onde o dado já está menos turbulento
- SQL = as válvulas que controlam esse reservatório
- `SELECT` → abre a válvula
- `WHERE` → regula o fluxo, filtra o que passa
- `JOIN` → conecta canos de reservatórios diferentes
- `GROUP BY` → agrupa a água em baldes por categoria

**Status:** decidida. Módulo já está completo e publicado sem essa camada. Aplicação retroativa (reescrever os capítulos existentes incorporando a analogia) fica **explicitamente adiada até o módulo de Python terminar**, para não fragmentar o trabalho entre conteúdo novo e revisão de conteúdo antigo ao mesmo tempo.

## 3. Módulo `3-python/`: caixa de ferramentas

Python não é canivete suíço. Canivete suíço carrega uma implicação ruim: cada função dele é capenga, a lâmina de canivete não corta como faca de verdade — e essa não é a força real do Python. A força do Python pra dado é ser a caixa que você abre e lá dentro tem a ferramenta certa pra cada etapa: `pandas` pra tabela, `requests` pra API, `psycopg2`/`SQLAlchemy` pra banco. Quem faz o trabalho pesado geralmente é a biblioteca, não a linguagem sozinha.

- **Bloco 1** ("A chave de fenda", substitui o provisório "arroz com feijão"): a ferramenta mais básica da caixa, que todo mundo conhece e todo mundo já usou. Aprender a segurar as ferramentas básicas de qualquer caixa — variável, condicional, função, o fundamento de qualquer linguagem.
- **Bloco 2**: tirar da caixa as ferramentas específicas de dado — pandas, numpy, conexão com banco, consumo de API. (Nome do bloco ainda em aberto — "cozinha industrial" foi proposto quando a analogia central era "a cozinha", que foi substituída por esta; precisa de nome novo ou pode ficar sem sub-nome.)

Analogias de capítulo já travadas dentro do Bloco 1 (essas não mudam com a troca acima, são independentes):
- **Estrutura de dado** → D&D, "Até dragões precisam de dados": um cavaleiro acha que está resgatando uma princesa de um dragão, mas é o contrário — a princesa é a vilã e o dragão precisa de ajuda.
- **Função** → receita de bolo: não se reescreve a receita toda, só se varia o ingrediente.
- **Tratamento de erro** → marido de aluguel: mais cedo ou mais tarde todo mundo precisa de um pra algo que quebra. Não é "se quebrar", é "quando quebrar".

**Status:** "caixa de ferramentas" substitui "canivete suíço" como analogia central do capítulo 1 e do módulo (decidida, escrita). A analogia "a cozinha" (mão inexperiente se corta, boa comida sai dali), proposta antes desta, fica **superada** por "caixa de ferramentas" — não foi formalmente descartada em palavras, mas perdeu a posição de analogia central; usar ou não algum resquício dela (ex: na abertura do README do módulo) é decisão em aberto.

## 4. IA no processo de criação do curso: estagiário com superpoderes

Vale para o curso inteiro, não é analogia de módulo específico.

Um estagiário com superpoder é rápido, tem energia, sabe uma quantidade absurda de coisa, faz em minutos o que levaria horas — mas não tem julgamento de sênior, não tem o contexto todo, e erra de um jeito que parece confiante mesmo quando está errado. Ninguém desconfia de estagiário burro; desconfia de estagiário competente demais que às vezes escorrega. É exatamente por isso que existe revisão humana em cada etapa do processo (esboço → aprovação → revisão educacional → beta reader) — a analogia justifica o processo inteiro, não só descreve a ferramenta.

Exemplo real do próprio projeto que ilustra isso: o bug de ponto flutuante no capítulo de variável, onde o texto afirmava que `3 * 29.90` resultava em `89.7`, quando na real o resultado impresso é `89.69999999999999`. Erro clássico de "estagiário competente que escorrega no detalhe".

**Status:** decidida nesta conversa, ainda não escrita em lugar nenhum. Aplicação mais óbvia: upgrade de linguagem na seção de transparência do README raiz (que já existe, hoje sem essa metáfora). Uso potencial maior: um futuro conteúdo sobre uso responsável de IA no fluxo de trabalho de um engenheiro de dados — isso está **fora do escopo atual** (foco é Python), só fica anotado aqui para não se perder.

## Pendências abertas

- Aplicar a analogia água/encanamento no capítulo 1 do módulo 1 (o capítulo 2 já foi reescrito).
- Conferir convivência entre "data warehouse = reservatório tratado" (módulo 1) e "banco relacional = reservatório" (retrofit planejado do módulo de SQL).
- Se algum resquício de "a cozinha" sobrevive (ex: abertura do README do módulo Python) ou se é descartada de vez.
- Nome definitivo do Bloco 2 do módulo Python, já que "cozinha industrial" caiu junto com "a cozinha".
- Se e quando entra conteúdo específico sobre uso de IA no fluxo de trabalho de dado, usando a analogia do estagiário.
