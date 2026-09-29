# Fontes de dado: de onde a água vem

Antes de entrar em banco de dados, vale dar um passo pra trás e fazer uma pergunta que parece boba: a água que sai da sua torneira veio de onde?

A resposta honesta é: depende. Água não vem de um lugar só. Pode ter vindo da chuva, de um rio, de um poço artesiano, de uma represa, e em alguns lugares até do mar. Cada uma dessas fontes tem um jeito próprio de aparecer, de fluir, e de precisar (ou não) de tratamento antes de virar aquela água que você enche o copo sem pensar duas vezes. Ninguém trata água de chuva do mesmo jeito que trata água do mar, e ninguém espera que um poço funcione igual a um rio.

## Com dado é a mesma coisa

Não existe "um tipo" de fonte de dado. Existem várias, cada uma com a sua personalidade, e boa parte do trabalho de quem mexe com dado é reconhecer com qual delas está lidando antes de sair abrindo registro. Esse módulo é justamente sobre isso: reconhecer as fontes e aprender a lidar com elas.

Vou passar rapidinho por cada uma, só pra você saber que elas existem. Sem profundidade técnica agora, é só o mapa.

## As fontes, uma por uma

**Banco de dado relacional.** É o reservatório tratado: água já organizada, estruturada, pronta pro consumo. O dado ali dentro tem forma definida e regra pra entrar. É por aqui que esse módulo começa, e é onde ele vai passar a maior parte do tempo.

**NoSQL.** É a água menos domesticada. Formato livre, sem aquela organização certinha do reservatório, e às vezes com um volume gigantesco, tipo represa ou mar bruto. Tem muita água ali, mas ela não chega arrumadinha na sua mão.

**Streaming (tempo real).** É o rio correndo. Fluxo contínuo, que não para de chegar. Você não vai lá buscar um balde e pronto: a água está passando agora, e daqui a um segundo já tem mais.

**Arquivo e planilha.** É o poço artesiano, ou o balde. Fonte pontual: você vai lá, busca o que precisa e volta. Não tem torneira automática, se quiser mais, vai ter que ir buscar de novo.

**API e serviço externo.** É a torneira da casa do vizinho, que você tem permissão de abrir quando precisa. A água não é sua, o encanamento não é seu, mas combinaram que você pode pegar um pouco quando precisar (e, como bom vizinho, sem abusar).

## Toda água precisa de um lugar pra descansar

Chuva, rio, poço, represa ou torneira do vizinho: não importa de onde a água veio, em algum momento ela precisa parar num lugar onde dá pra usar de verdade. Com dado é igual. Todas essas fontes, cedo ou tarde, precisam de um lugar pra descansar e virar algo consultável.

E o reservatório mais maduro e mais comum que existe hoje pra isso é o banco de dado relacional. Por isso o módulo começa ali.

## Fechando esse capítulo

Não é por acaso que o banco relacional vem primeiro, e ele tá pertinho: é já o [próximo capítulo](01-bancos-de-dados-relacionais-e-sql.md).
