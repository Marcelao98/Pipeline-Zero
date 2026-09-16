# O ciclo de vida da engenharia de dados

Na seção passada a gente definiu o que é engenharia de dados e quem faz o quê. Agora vem a pergunta óbvia: **certo, mas na prática, o que o engenheiro de dados realmente faz, passo a passo?**

Antes de continuar, vale eu deixar bem claro uma coisa: eu, que estou escrevendo isso, nunca trabalhei como engenheiro de dados. Sou eletricista de formação e estou estudando essa área por conta própria, do zero, assim como (imagino) boa parte de quem está lendo isso agora. Não estou te ensinando do alto de anos de experiência de mercado. Estou organizando, com as minhas palavras, o que eu fui aprendendo, pra tornar esse caminho menos confuso pra quem também está começando. Dito isso, vamos ao que interessa.

É isso que o ciclo de vida da engenharia de dados responde. E ele vai ser, literalmente, o mapa de tudo que esse repositório vai cobrir daqui pra frente. Cada módulo futuro sobre SQL, Python, Airflow, cloud, seja lá o que for, vai se encaixar em algum pedaço desse ciclo. Então vale a pena entender bem essa estrutura agora, porque ela é a espinha dorsal do resto da história.

## Voltando pra nossa empresa bagunçada

Lembra da empresa lá do módulo anterior, aquela que cresceu e virou uma bagunça de dado espalhado? Vamos usar ela de exemplo de novo, só que agora imagina ela como uma loja online, porque isso facilita enxergar cada etapa do ciclo acontecendo de verdade.

Essa loja tem um app onde o cliente compra produto. Tem um sistema de estoque. Tem uma ferramenta de marketing que dispara anúncio. E o dono da empresa quer, no fim das contas, uma coisa simples: **um relatório confiável mostrando quanto ele vendeu ontem, e por quê**.

Pra esse relatório existir, o dado precisa passar por um caminho. Esse caminho tem cinco etapas.

## As cinco etapas

### 1. Geração

Todo dado nasce em algum lugar. Nesse caso, nasce no momento em que o cliente clica em "comprar" no app, ou quando o sistema de estoque registra que um item saiu da prateleira, ou quando alguém clica num anúncio no Instagram.

O engenheiro de dados, na maioria das vezes, **não controla como esse dado nasce**. Ele só recebe o que os sistemas de origem produzem. Mas ele precisa entender bem como cada sistema gera esse dado: com que frequência, em que formato, se o formato pode mudar do nada (e vai mudar, confia), se é um monte de dado de uma vez (lote) ou se vai pingando aos poucos, em tempo real.

### 2. Armazenamento

Depois que o dado nasce, ele precisa morar em algum lugar. Parece óbvio, mas essa é uma das decisões mais importantes (e mais difíceis) de toda a engenharia de dados. Onde eu guardo isso? Num banco de dados? Num "data lake" (um depósito gigante de arquivo bruto)? Num "data warehouse" (um armazém já mais organizado, pronto pra consulta)? Guardo tudo pra sempre, ou só por um tempo?

Essa decisão não é feita uma vez só e esquecida. O dado geralmente passa por armazenamento *várias vezes* ao longo do ciclo, mudando de forma a cada etapa.

### 3. Ingestão

Ingestão é o processo de **pegar o dado lá na origem e trazer ele pra dentro dos seus sistemas**. É literalmente o cano que liga o sistema de vendas, o sistema de estoque e a ferramenta de marketing num lugar central onde dá pra trabalhar com tudo junto.

Essa etapa costuma ser o maior gargalo e a maior dor de cabeça de todo o ciclo, porque sistema de origem cai, muda de formato sem avisar, manda dado duplicado, manda dado incompleto, ou simplesmente não manda nada por um tempo. Boa parte do trabalho real de um engenheiro de dados no dia a dia mora aqui.

### 4. Transformação

Dado bruto raramente é útil do jeito que chega. Ele precisa ser limpo, corrigido, combinado com outros dados, agregado, calculado. É aqui que "quantidade de item vendido" vira "faturamento do dia", que "clique no anúncio" mais "compra realizada" vira "quanto aquela campanha de marketing realmente trouxe de retorno".

Aqui mora um conceito que você provavelmente já ouviu falar, ou vai ouvir bastante: **ETL** e **ELT**. Não precisa se aprofundar agora, só entender a lógica: ETL significa *extrair, transformar, e só depois carregar* o dado no destino final, ou seja, o dado é arrumado *antes* de chegar no armazém. ELT inverte a ordem: *extrair, carregar, e só depois transformar*. O dado bruto vai direto pro armazém, e a arrumação acontece lá dentro, aproveitando o poder de processamento que as ferramentas de nuvem modernas oferecem. Essa mudança de ETL pra ELT foi, em boa parte, consequência direta da nuvem ter ficado barata e poderosa o suficiente pra isso fazer sentido. A gente volta nesse assunto com calma, e com muito mais profundidade, num módulo específico lá na frente.

### 5. Disponibilização (serving)

De nada adianta todo esse trabalho se o dado não chega em quem precisa dele, do jeito que essa pessoa consegue usar. Essa última etapa é entregar o dado já tratado pro analista montar o relatório, pro cientista de dados treinar o modelo, ou até pra alimentar de volta um sistema (tipo mandar uma lista de clientes com risco de cancelamento direto pra ferramenta que o time de vendas usa).

É aqui, nessa etapa, que a empresa finalmente recebe a resposta pra pergunta "quanto eu vendi ontem, e por quê". É por isso que essa etapa existe: **todo o resto do ciclo só tem razão de existir porque, no final, alguém precisa usar esse dado pra alguma coisa**.

## Uma coisa importante: o ciclo não é uma linha reta

Repara que eu descrevi essas cinco etapas como se fosse 1, 2, 3, 4, 5, bonitinho, em ordem. Na vida real não é bem assim. O dado pode passar por armazenamento várias vezes, voltar, ser transformado de novo, ser servido pra um sistema que gera *outro* dado que entra de novo lá na etapa de geração. É mais um ciclo mesmo, que se repete e se retroalimenta, do que uma esteira de fábrica que só anda pra frente.

## E o que são esses tais de "undercurrents"?

Se você folhear o livro que citei na seção anterior, vai ver que, além dessas cinco etapas, ele fala bastante de um conjunto de temas que **atravessam todas as etapas ao mesmo tempo**, em vez de serem uma etapa própria: segurança, governança de dado, DataOps, arquitetura de dado, orquestração e engenharia de software.

Eu não vou entrar em detalhe sobre cada um agora, e olha, sendo bem sincero contigo: se você (assim como eu) nunca trabalhou de fato como engenheiro de dados, um monte desse conteúdo (principalmente governança) vai soar abstrato e meio inútil nesse momento. E tudo bem, é normal mesmo. O que importa agora é só você saber que esses temas existem, que eles não são "uma etapa a mais", e que alguns deles vão virar módulo próprio aqui no repositório assim que fizer sentido: orquestração, por exemplo (spoiler: é aí que entra o Airflow), e engenharia de software (é aí que entra Git).

## Fechando essa parte

Esse é o mapa. Geração, armazenamento, ingestão, transformação, disponibilização, com um punhado de temas transversais rondando tudo isso. Cada ferramenta que você vai estudar daqui pra frente neste repositório, seja SQL, Python, Airflow, ou qualquer outra coisa, existe pra resolver um problema específico dentro de uma (ou mais) dessas etapas.

Guarda esse mapa. A partir de agora, sempre que um módulo novo aparecer aqui, você vai conseguir se perguntar: "ok, isso resolve que parte do ciclo?". E essa pergunta, sozinha, já vale mais do que decorar o nome de mil ferramentas.
