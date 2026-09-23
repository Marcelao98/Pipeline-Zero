# Jornal de decisões — Pipeline Zero

Registro histórico de todas as decisões tomadas sobre o projeto até aqui, organizado por tema. Não substitui os documentos dedicados (`analogias-narrativas-pipeline-zero.md` e `fluxo-de-producao-pipeline-zero.md`), que são referenciados nas seções correspondentes.

## 1. Posicionamento do projeto

- Pipeline Zero é o **carro-chefe** do conjunto de projetos pessoais do Marcelo (junto com a iniciativa "Nova Aurora", um Discord de D&D, e aulas particulares). Decisão explícita: é o foco atual, porque pode puxar atenção pros outros projetos. **[decidido]**
- Público: iniciante absoluto em engenharia de dados, sem acesso fácil a conteúdo estruturado em português. **[decidido]**
- Formato: um **guia** (não um curso completo) — "resumo do resumo", narrativo, explica o porquê antes do como, e aponta pra fontes mais completas pra quem quiser se aprofundar. **[decidido]**
- Estrutura narrativa fixa por capítulo: o que é → que problema resolve → o que existia antes e por que não era suficiente → trade-offs/quando não usar → exemplo prático. **[decidido]**
- Autor não é profissional de dados atuante — isso é tratado como recurso de autenticidade, não como fraqueza a esconder. **[decidido]**
- Transparência sobre uso de IA: seção no README raiz explicando que o conteúdo é escrito com assistência de IA (Claude Code), mas com processo humano de revisão em cada etapa — "IA é ferramenta, não quem decide". **[decidido, escrito]**

## 2. Estrutura do repositório

- Estrutura atual por módulo numerado: `1-que-porra-e-essa/` (intro + roadmap + ciclo de vida do dado), `2-onde-o-dado-mora/` (SQL, completo), `3-python/` (em andamento). **[decidido]**
- Cada pasta de conteúdo tem um `README.md` de índice (contexto curto + lista numerada de capítulos). Já aplicado nos módulos 1, 2 e 3. **[decidido, aplicado]**
- Dentro de `2-onde-o-dado-mora/`, foi testada uma subpasta por assunto/dificuldade e depois **revertida** para numeração linear (flat). **[decidido — versão final é flat]**
- Reorganização futura maior: reestruturar o repositório inteiro por **estágio do ciclo de vida do dado**, não por ferramenta. Ex: pasta "onde o dado mora" vira o estágio de armazenamento e passa a conter SQL + Excel + APIs; uma pasta separada de "ferramentas transversais" (Python, Claude Code) que podem ser usadas em qualquer estágio; e uma pasta de fundamentos gerais de engenharia de software não específicos de dado (Docker, testes, Git). Um diagrama Mermaid no README raiz mostraria a "trilha" de leitura sugerida separadamente da estrutura categórica de pastas, já que a ordem ideal varia por leitor (alguns pulam Excel, alguns querem começar direto em Airflow). **[adiado até ter bem mais conteúdo]**
- Renumeração de pastas pra inserir um módulo de Excel antes de `2-onde-o-dado-mora/` foi cogitada mas não executada. **[adiado]**

## 3. Módulo SQL (`2-onde-o-dado-mora/`) — completo

Estrutura final (numeração flat): 1) bancos relacionais e SQL (conceitual), 2) escolhendo e instalando um banco, 3) consultando dado (SELECT/WHERE/ORDER BY/LIMIT), 4) agregando e agrupando (COUNT/SUM/GROUP BY/HAVING), 5) juntando tabelas (JOIN), 6) criando e modificando dado (CRUD), 7) subqueries, 8) CTEs, 9) window functions, 10) transações, 11) fechamento do módulo (recursos + mensagem pessoal + história do projeto Riverflow). **[decidido, completo]**

- Dataset recorrente usado em todos os exemplos: `clientes` (5 linhas), `pedidos` (6 linhas, ids 101-106), `produtos` (4 linhas, incluindo um produto nunca pedido de propósito). **[decidido]**
- Analogia central do módulo: **reservatório e válvula** (banco relacional = reservatório local; SQL = as válvulas — SELECT abre, WHERE filtra o fluxo, JOIN conecta canos de reservatórios diferentes, GROUP BY agrupa em baldes por categoria). Detalhes em `analogias-narrativas-pipeline-zero.md`. **[decidido, ainda não aplicado ao texto já publicado — retrofit adiado até o módulo de Python terminar]**
- Fechamento do módulo inclui lista curada de recursos gratuitos em português (+ 2 exceções em inglês sinalizadas: canal Data With Baraa e curso de SQL do freeCodeCamp, este último deixado por último e com aviso de estar em inglês). **[decidido, escrito]**

## 4. Módulo Python (`3-python/`) — em andamento

Escopo evoluiu em três rodadas de correção do autor: de "lógica de programação" pura → "tudo relevante pra engenharia de dados, mas nada além disso" → expansão final após comparação com sumário de vídeo de referência (adicionando "Instalando Python", `input()` e operadores matemáticos explícitos). Estrutura final, 15 capítulos em 2 blocos:

**Bloco 1 — fundamento da linguagem:**
1. Por que Python — ✅ aprovado
2. Instalando Python — não iniciado
3. Hello World + variável e tipo de dado (+ `input()` + operadores matemáticos) — esboço escrito, correção de bug pendente (ver abaixo)
4. Texto (string): manipulação, fatiamento, métodos comuns, f-string
5. Estrutura de controle: condicional e loop
6. Função
7. Estrutura de dado: lista e dicionário (+ menção breve a tupla, set, list comprehension)
8. Tratamento de erro (try/except)
9. Ambiente e pacote (pip, ambiente virtual — só pra bibliotecas externas, não pra instalar o interpretador)

**Bloco 2 — Python aplicado a dado:**
10. Ler e escrever arquivo
11. NumPy (mínimo, só o suficiente pra motivar pandas)
12. Manipular dado tabular com pandas ("SQL fora do banco")
13. Conectar Python a banco de dado (psycopg2/SQLAlchemy)
14. Consumir API / requisição HTTP (requests, noção de JSON)
15. Fechamento do módulo (recursos + mensagem final, mesmo formato do fechamento de SQL)

**Explicitamente fora de escopo:** programação orientada a objeto (classe, herança), match case, operadores de associação/identidade (`in`/`is`), arredondamento/random/validação numérica avançada, edge cases de case de string. `datetime` como capítulo próprio segue **em aberto**.

- Analogia central do módulo: **caixa de ferramentas** (não canivete suíço — a força do Python é abrir a caixa certa pra cada etapa, quem faz o trabalho pesado geralmente é a biblioteca). Substitui a proposta anterior "a cozinha", que fica restrita ao README do módulo (organização interna) e à nomeação do Bloco 1 ("arroz com feijão" — básico, essencial, sem frescura). Nome do Bloco 2 ainda em aberto, já que "cozinha industrial" caiu junto com "a cozinha" como analogia central. Detalhes completos em `analogias-narrativas-pipeline-zero.md`. **[decidido, escrito]**
- Bug encontrado no capítulo 3 (`03-variavel-e-tipo-de-dado.md`): o exemplo prático afirma que `3 * 29.90` resulta em `89.7`, mas o resultado real impresso é `89.69999999999999`. Instrução de correção enviada (reconhecer o resultado real no texto e explicar que é representação de ponto flutuante, não erro do leitor). **[correção enviada, confirmação de aplicação pendente]**
- Decisão de trocar os exemplos do Bloco 2 pra usar o domínio profissional real do autor (engenharia elétrica, manutenção de planta industrial, paralelo com o projeto pessoal Riverflow) em vez de dataset genérico de loja online. **[adiado — "vamos escrever como tá primeiro"]**
- Gancho de abertura do capítulo 3 (`03-variavel-e-tipo-de-dado.md`) com Heráclito: "a única constante é a mudança" e "ninguém se banha duas vezes no mesmo rio" (nome do rio = constante, água = variável), mais a convenção de CAIXA_ALTA pra constante em Python. O rio de Heráclito é analogia própria, separada da analogia mestra de água/encanamento, então não fere a regra de não esticar a mestra pro módulo de Python. **[decidido, escrito]**
- Revisão da abertura da seção "Ferramenta certa pra cada serviço" (capítulo 2 do módulo 3-python/), mantida separada do gancho do capítulo 3, pra tratar em rodada à parte. **[pendente]**

## 5. Módulo Excel — futuro, ainda não iniciado

- Ordem de produção: SQL → Python → Excel (decidido explicitamente duas vezes). **[decidido]**
- Escopo mínimo definido: fórmula básica/referência, PROCV, PROCX/XLOOKUP, filtrar/ordenar, tabela dinâmica, gráfico. VBA e Power Query **excluídos**. **[decidido]**
- Formato de produção: planilha `.xlsx` funcional como companion, viável de automatizar agora (skill `xlsx` disponível); prints de UI ficam pra depois (manual); vídeo fica pra mais tarde ainda, dependendo de encontrar um colaborador de edição de vídeo. **[decidido]**

## 6. Processo de trabalho (humano no loop)

- Rejeitada a proposta de automatizar/agrupar a produção de capítulos sem revisão individual — o autor preferiu manter revisão humana em cada capítulo, um de cada vez, pra garantir tom, exemplos e didática corretos. **[decidido]**
- Esboço sempre antes do texto completo, pra qualquer capítulo novo (regra do `CLAUDE.md`). **[decidido, regra fixa]**
- Fluxo de produção com personas nomeadas (Catarina, Claudia Coda, Dr Chatonildo, Mestre Enredo, Garimpo, Bardo) e regra de a Claudia Coda perguntar antes de decidir qualquer coisa não explícita. Detalhes completos em `fluxo-de-producao-pipeline-zero.md`. **[decidido]**
- Registro histórico de todas as alterações (código e storytelling), incluindo o motivo — decidido usar duas camadas: commit git (com motivo no corpo quando for decisão de conteúdo) + log de decisões vivo (este jornal e o de analogias). **[decidido]**

## 7. Prontidão para divulgação (LinkedIn)

- Recomendação dada: SQL e Python completos já são barra suficiente pra divulgar oficialmente — não é necessário esperar Git, Airflow ou Nuvem. **[recomendação dada, aguardando SQL+Python completos]**
- Recomendado antes de divulgar oficialmente: mais beta readers além de um amigo, auditoria completa de links/README, e uma seção honesta de "estado atual" no README. **[recomendação dada, ainda não executada]**
- Um amigo do autor (sem experiência prévia em SQL) já testou o módulo de SQL de forma informal e relatou ter entendido tudo. **[feedback positivo recebido, informal]**

## 8. Cheatsheets

- Produzir cheatsheets de referência rápida (sintaxe, sem a narrativa) pra cada módulo já concluído. Público diferente do guia principal: quem já manja e só quer consultar rápido, não reler a explicação. **[decidido como conceito, produção adiada até os módulos de SQL e Python estarem prontos]**

## 9. Projeto Garimpo (separado, mas relacionado)

- Iniciativa de curadoria de conteúdo educacional livre via mineração de transcript de vídeo (`youtube-transcript-api` ou `yt-dlp --write-auto-sub --skip-download`), em vez de assistir o vídeo inteiro. **[decidido como conceito]**
- Testado tecnicamente neste ambiente e confirmado que **não funciona neste sandbox** (allowlist de rede bloqueia YouTube) — precisa rodar de um ambiente com acesso normal à internet (ex: Claude Code local do autor). **[testado, limitação confirmada]**
- Vai ter seu próprio chat dedicado, separado deste. **[decidido]**
- Reaproveitado também como sandbox pra testar analogias novas antes delas irem pros módulos oficiais (ver `fluxo-de-producao-pipeline-zero.md`). **[decidido]**

## 10. Futuro distante (fora do escopo atual)

- Site dedicado (Docusaurus ou MkDocs) como versão mais acessível do que navegar o GitHub direto — o autor pretende aprender um pouco de front-end por conta própria antes de partir pra isso, mesmo podendo tecnicamente fazer com Claude Code agora. **[adiado até ter muito mais conteúdo]**
- Conforme o projeto crescer, a ideia é trazer gente de outras áreas pra cobrir tópicos que o autor não domina — por ora o foco dele é só a parte de dado. **[intenção registrada, sem prazo]**
- Possível conteúdo futuro sobre uso responsável de IA no fluxo de trabalho de um engenheiro de dados, usando a analogia do "estagiário com superpoderes" — fora do escopo atual (foco é Python). **[ideia registrada, sem prazo]**

## 11. Pendências consolidadas

- Confirmação de que Claude Code aplicou a correção do bug de ponto flutuante no capítulo 3 de Python.
- Criação do capítulo "Instalando Python".
- Decisão sobre `datetime` como capítulo próprio ou não.
- Nome do revisor de storytelling (proposto: Mestre Enredo).
- Retrofit da analogia reservatório/válvula no módulo de SQL já publicado.
- Definição de central analogy pra `1-que-porra-e-essa/` (candidata natural: água e encanamento, ver `analogias-narrativas-pipeline-zero.md`) e decisão de quando reescrever o capítulo 2 desse módulo.
- Nome do Bloco 2 do módulo Python (órfão desde que "cozinha industrial" caiu).
- Domínio dos exemplos do Bloco 2 de Python (genérico vs. engenharia elétrica/industrial real do autor).
- Produção dos cheatsheets (formato, escopo por módulo) quando SQL e Python estiverem prontos.
- Execução da auditoria de links/README e da seção de "estado atual" antes da divulgação oficial no LinkedIn.
