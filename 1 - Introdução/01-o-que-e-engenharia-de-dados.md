# O que é, afinal, engenharia de dados?

Beleza, vamos começar do começo mesmo. Sem enrolação, sem definição de dicionário decorada. Vamos entender isso do jeito que faz sentido: pensando no problema primeiro.

## Imagina a seguinte cena

Uma empresa nasce pequena. No começo, os dados dela cabem inteiros numa cabeça só — o dono sabe quantas vendas fez na semana, sabe quem são os clientes, sabe o estoque de cabeça. Não precisa de "engenharia" de coisa nenhuma.

Só que a empresa cresce. Agora tem um sistema de vendas, um app, um monte de gente comprando, planilhas se multiplicando, um banco de dados aqui, outro sistema ali, uma API de pagamento acolá. E de repente, ninguém mais sabe ao certo quantas vendas foram feitas ontem, porque o número do sistema de vendas não bate com o número do financeiro, que não bate com o que o time de marketing está enxergando no relatório dele.

Isso não é ficção, isso é o dia a dia de praticamente toda empresa que cresce. E é exatamente aqui, nessa bagunça, que nasce a necessidade de alguém pensar: *"como a gente pega esse monte de dado espalhado, bagunçado, gerado em lugares diferentes, e transforma isso em algo confiável, disponível e útil pra quem precisa tomar decisão com isso?"*

Essa pessoa (ou esse time) é o engenheiro de dados. E o trabalho dele **não é analisar o dado**. É construir e manter os canos por onde o dado passa, garantindo que ele chegue limpo, confiável e no lugar certo, na hora certa, pra quem for usá-lo.

## Uma definição de verdade (sem enrolar)

Se você quiser uma definição mais "oficial" pra guardar, essa é boa: engenharia de dados é a disciplina responsável por **desenvolver, implementar e manter os sistemas e processos que pegam dado bruto e o transformam em informação de alta qualidade e confiável**, pronta para ser usada em análises, relatórios, machine learning e no que mais o negócio precisar.

Repara: a definição não fala em "usar dado pra tomar decisão". Ela fala em **construir o que possibilita** que a decisão seja tomada com dado bom. Essa diferença é o cerne de tudo. O engenheiro de dados entrega a matéria-prima tratada. O que vai ser feito com essa matéria-prima é trabalho de outras pessoas — e é aí que entram os outros dois personagens dessa história: o analista de dados e o cientista de dados / engenheiro de machine learning.

## Analista de dados, cientista de dados, engenheiro de dados: quem faz o quê

Isso confunde todo mundo no começo, e com razão, porque as fronteiras entre essas funções realmente são meio embaçadas na prática do dia a dia de muita empresa. Mas conceitualmente, dá pra separar bem:

**Analista de dados** olha pro passado e pro presente. Pega o dado que já está limpo, organizado e disponível, e responde perguntas de negócio com ele: "por que as vendas caíram em outubro?", "qual campanha de marketing trouxe mais retorno?". O trabalho dele é interpretação e comunicação — ele transforma dado em insight que um humano consegue entender e agir em cima.

**Cientista de dados** olha pro futuro, e usa estatística e machine learning pra fazer previsão e recomendação: "qual a chance desse cliente cancelar a assinatura no próximo mês?", "que produto eu deveria recomendar pra esse usuário?". Ele constrói modelos que aprendem padrão nos dados e geram previsão em cima disso.

**Engenheiro de dados** não olha pro passado nem pro futuro do negócio diretamente. Ele olha pro **cano**. O trabalho dele é garantir que o dado saia do sistema de origem (um banco de dados de um app, uma API, um sensor de IoT, sei lá) e chegue de forma limpa, estruturada e confiável até o lugar onde o analista e o cientista de dados vão trabalhar. Sem esse trabalho de base, o analista fica fazendo relatório com dado errado, e o cientista de dados treina modelo em cima de lixo — e modelo treinado com lixo, adivinha, produz previsão de lixo.

Existe até uma pirâmide famosa pra ilustrar isso, a **Hierarquia de Necessidades da Ciência de Dados** (inspirada na pirâmide de Maslow, aquela da psicologia). A base dela é justamente coleta, tratamento e infraestrutura de dado — ou seja, engenharia de dados. Só depois de construída essa base é que dá pra subir pra análise, e só no topo da pirâmide é que mora machine learning e IA de verdade.

E aqui vai um dado curioso pra você guardar: na prática, boa parte dos cientistas de dados passa a maior parte do tempo deles fazendo trabalho que, na teoria, deveria ser de engenharia de dados — limpando, coletando e organizando dado bagunçado — em vez de fazer o que eles foram contratados pra fazer, que é modelagem estatística e machine learning de verdade. Isso não é porque cientista de dados gosta de sofrer. É porque, quando não existe uma boa fundação de engenharia de dados, alguém precisa fazer esse trabalho na marra, e geralmente sobra pra quem está mais perto do problema.

É exatamente esse buraco que a engenharia de dados, como área, existe pra tapar.

## Então, resumindo essa bagunça toda

- **Engenheiro de dados**: constrói e mantém o cano. Garante que o dado saia do lugar A, chegue limpo e confiável no lugar B, no tempo certo.
- **Analista de dados**: usa o dado que já está tratado pra entender o que aconteceu e por quê.
- **Cientista de dados / engenheiro de machine learning**: usa o dado tratado pra prever o que vai acontecer, ou pra automatizar decisão através de modelos.

Nenhuma dessas funções é "mais importante" que a outra — elas são dependentes. Sem engenharia de dados boa, as outras duas ficam patinando em cima de dado ruim. E é por isso que, cada vez mais, engenharia de dados tem virado a base sobre a qual empresa nenhuma séria consegue fazer nada de relevante com dado.

## Uma recomendação séria, antes de seguir em frente

Se você quiser entender a parte conceitual de engenharia de dados com muito mais profundidade do que eu vou conseguir passar aqui (e eu recomendo fortemente que você entenda), o livro que eu uso como referência principal — e que estou estudando agora mesmo — é o **Fundamentals of Data Engineering**, de Joe Reis e Matt Housley.

É, sem dúvida, um dos melhores materiais que existem sobre o assunto. O problema é o de sempre: **está disponível só em inglês**, e por isso eu não vou deixar o link dele aqui no repositório. A ideia deste projeto é ser 100% em português, então prefiro te indicar o caminho — procure por esse título, é um livro relativamente fácil de encontrar — e deixar aqui, nesse repositório, a versão explicada com as minhas palavras, no meu tom, pra quem quer entender o conceito sem precisar enfrentar a barreira do idioma.

Na próxima seção, a gente entra no ciclo de vida da engenharia de dados — ou seja, as etapas que um dado percorre desde que nasce até virar informação útil pra alguém. Bora.
