# Por onde começar, na prática

Beleza. Você já entende o que é engenharia de dados, sabe diferenciar ela de análise e de ciência de dados, e já tem o mapa geral na cabeça (geração, armazenamento, ingestão, transformação, disponibilização). Agora vem a pergunta que provavelmente foi o motivo real de você ter chegado até esse repositório: **tá, mas por onde eu começo a estudar isso de verdade?**

Essa seção existe justamente pra isso. Ela não vai te ensinar SQL, Python ou Airflow de verdade aqui dentro. Ela vai te dizer, em ordem, o que estudar, o porquê de estudar naquela ordem, e pra qual parte do ciclo de vida aquilo serve. Cada tópico abaixo vai virar (ou já é) uma seção própria nesse repositório, com muito mais profundidade.

Vale um aviso: esse roadmap também está em construção, junto com o resto do repositório. A ordem e os itens abaixo podem mudar conforme o projeto cresce.

## Antes de tudo: um recado sincero pra quem é do Brasil

Isso aqui eu quero deixar bem claro, porque ninguém fala isso em curso nenhum, e devia falar.

Antes de sair correndo pra aprender Python e SQL, se você ainda não sabe se virar bem numa planilha de Excel (ou Google Sheets), pare e aprenda isso primeiro. Sério.

Não estou falando de virar um mago do Excel, cheio de fórmula maluca e macro em VBA. Isso vem com o tempo, com a prática, trabalhando. Estou falando do básico funcional: saber montar uma tabela organizada, usar um PROCV (ou PROC-X, a versão mais nova), montar uma tabela dinâmica simples, fazer uma fórmula básica de soma condicional. Se esse tipo de coisa ainda te dá um nó na cabeça, engenharia de dados vai te dar um nó bem maior, porque muita coisa que você vai fazer com SQL e Python é, na essência, a mesma lógica de organizar, cruzar e resumir dado que uma planilha já faz, só que em outra escala e com outra ferramenta. Dominar essa lógica num ambiente mais simples primeiro facilita muito a virada de chave pra ferramentas mais pesadas depois.

Então, resumindo esse recado: se Excel ainda é um mistério pra você, para aqui, aprenda o básico funcional dele primeiro, e só depois volta pra essa lista.

## Agora sim, o roadmap

### 1. Fontes de dado (começando por SQL)

Todo dado vem de algum lugar, e conforme esse repositório crescer, essa categoria pode ganhar mais fontes além de banco relacional (Excel, API, arquivo, o que for). Por enquanto, o ponto de partida é o mais comum de todos: banco de dados relacional e SQL. Essa é a base de tudo, e não é exagero dizer isso. A imensa maioria do dado que existe em empresa mora, em algum momento, dentro de um banco de dados relacional. SQL é a linguagem universal pra conversar com esse tipo de banco: perguntar "me dê todas as vendas de outubro", "quantos clientes compraram mais de uma vez", esse tipo de coisa.

Lembrando do ciclo de vida: SQL aparece com força nas etapas de **armazenamento**, **ingestão** e principalmente **transformação**. É a ferramenta que você vai usar pra limpar, organizar e extrair sentido do dado bruto.

*(Módulo dedicado a SQL e bancos relacionais: [2-onde-o-dado-mora/](../2-onde-o-dado-mora/README.md).)*

### 2. Lógica de programação e Python

Depois de entender SQL, o próximo passo natural é aprender a programar de verdade. E aí entra o Python, a caixa de ferramentas que você carrega daqui pra frente. Não é a linguagem mais rápida nem a mais elegante, mas é a que tem a ferramenta certa pronta pra quase qualquer etapa do ciclo de dado, e é exatamente essa versatilidade que pesa mais do que qualquer vantagem técnica isolada de outra linguagem.

Python entra forte nas etapas de **ingestão** (escrever o código que busca o dado lá na origem) e **transformação** (fazer cálculo, limpeza e lógica que SQL sozinho não dá conta, ou não dá conta de forma elegante).

*(Módulo dedicado a Python: [3-python/](../3-python/README.md), com o Bloco 1 completo e o Bloco 2 ainda não escrito.)*

### 3. Git e controle de versão

Assim que você começa a escrever código de verdade, uma pergunta aparece rapidinho: "e se eu quebrar tudo? e se eu precisar voltar pro que tinha antes? e se eu quiser trabalhar junto com outra pessoa no mesmo código sem sobrescrever o trabalho dela?"

Git resolve exatamente isso. Ele guarda o histórico de tudo que você mudou no seu código, permite voltar no tempo, permite trabalhar em equipe sem bagunçar o trabalho de ninguém. Isso não é uma etapa do ciclo de vida propriamente dita, é um daqueles temas transversais que mencionei na seção anterior (a parte de engenharia de software), mas na prática, você vai usar Git o tempo todo, em praticamente tudo que fizer daqui pra frente.

*(Módulo dedicado a Git: ainda a ser escrito neste repositório.)*

### 4. Orquestração (e aqui entra o Airflow)

Depois que você já sabe escrever um código em Python que busca dado, e já sabe usar SQL pra transformar esse dado, uma nova pergunta surge: "beleza, mas quem roda esse código todo dia, sozinho, na hora certa, na ordem certa, e me avisa se algo der errado?"

Rodar um script na mão funciona quando você tem um script. Quando você tem vinte scripts, cada um dependendo do resultado do anterior, rodar tudo na mão vira um pesadelo, e é impossível de manter. Isso é o que a etapa de **orquestração** resolve: ela é a peça que organiza, agenda e monitora todos esses passos automaticamente. A ferramenta mais usada do mercado pra isso hoje é o Apache Airflow, e é por isso que ele aparece tanto quando você pesquisa sobre a área.

*(Módulo dedicado a orquestração e Airflow: ainda a ser escrito neste repositório.)*

### 5. Nuvem (cloud)

Só depois de entender os fundamentos (banco de dados, programação, versionamento e orquestração) é que faz sentido de verdade entrar na nuvem. Por quê nessa ordem? Porque a nuvem não é um conceito novo, ela é basicamente **infraestrutura de computador alugada**, disponível na internet, que te dá acesso a versões escaláveis e gerenciadas de tudo que você já aprendeu até aqui: banco de dados, armazenamento, poder de processamento, ferramentas de orquestração prontas.

Se você entende os fundamentos antes, a nuvem passa de "um monte de nome de serviço que eu não entendo" pra "ah, isso aqui é só a versão gerenciada daquilo que eu já sei o que é".

*(Módulo dedicado a cloud: ainda a ser escrito neste repositório.)*

## E por que existe tanta ferramenta, afinal?

Se você já pesquisou qualquer coisa sobre isso, sabe do que estou falando: AWS, mas também Azure, mas também Google Cloud, mas tem Databricks, mas tem Snowflake, e a lista não acaba nunca. É normal isso parecer um caos completo no início.

A explicação curta é a seguinte: a maioria dessas ferramentas está resolvendo o mesmo tipo de problema, mas com trade-offs diferentes entre custo, escala, facilidade de uso e o quanto você fica "preso" àquele fornecedor depois de escolher ele. Não existe uma ferramenta "melhor" de forma absoluta, existe a ferramenta mais adequada pra um contexto específico, e empresas diferentes, com problemas e tamanhos diferentes, vão fazer escolhas diferentes.

A boa notícia é que você não precisa aprender todas elas. Depois que você entende os fundamentos desse roadmap (SQL, Python, Git, orquestração), aprender uma nuvem específica, ou uma ferramenta específica dentro dela, vira muito mais rápido, porque os conceitos de fundo são praticamente os mesmos em qualquer lugar. Você troca o nome do botão, não a lógica por trás dele.

## Resumindo o roadmap

1. Excel funcional (se você ainda não tem isso, comece por aqui, sério)
2. Fontes de dado (começando por SQL)
3. Lógica de programação e Python
4. Git e controle de versão
5. Orquestração (Airflow)
6. Nuvem (cloud)

Depois disso, você já tem chão suficiente pra escolher, com calma e entendimento, quais ferramentas mais específicas do ecossistema (dbt, Spark, Databricks, Snowflake, e por aí vai) fazem sentido pro caminho que você quer seguir dentro da área.
