# Escolhendo e instalando um banco de dados relacional

No capítulo anterior a gente entendeu o que é um banco de dados relacional (tabela, linha, coluna, chave primária, chave estrangeira) e o que é SQL, a linguagem que existe pra conversar com esse banco. Só que tem um detalhe que ainda não resolvemos: SQL sozinho não roda em lugar nenhum. Você pode saber escrever a consulta perfeita, que se não tiver alguém (ou melhor, alguma coisa) por trás pra receber esse comando e executar de verdade, não existe banco de dado algum. Falta a peça que efetivamente guarda o dado em disco, entende o SQL que você manda, e devolve resposta. É disso que esse capítulo trata, antes de a gente escrever a primeira consulta de verdade.

## SQL é a linguagem, quem executa é o SGBD

SQL é só a linguagem, o conjunto de regras de como escrever um pedido pro banco. Ela não roda sozinha, do mesmo jeito que português não "roda" sozinho, alguém precisa ler e entender o que foi escrito. Quem cumpre esse papel é o **SGBD**, o Sistema Gerenciador de Banco de Dados: o programa que efetivamente guarda o dado em disco, organiza ele em tabela, recebe o comando SQL que você escreve, interpreta, executa, e devolve o resultado.

MySQL, PostgreSQL, SQLite, SQL Server e Oracle são todos exemplos de SGBD. Cada um é um programa diferente, escrito por gente diferente, com histórico e dono diferente, mas todos entendem (com pequenas variações) a mesma linguagem SQL que a gente viu no capítulo anterior. É por isso que aprender SQL uma vez te dá uma base que atravessa praticamente qualquer um desses programas.

## Os principais SGBDs relacionais do mercado

Vale só situar, sem se aprofundar, quem são os nomes que você vai esbarrar por aí:

- **MySQL**: um dos SGBDs open source mais usados do mundo, historicamente forte em aplicação web. Foi comprado pela Oracle em 2010, o que fez parte da comunidade migrar pra forks como o MariaDB.
- **PostgreSQL**: SGBD open source, conhecido por seguir o padrão SQL de forma mais rigorosa e por ter um conjunto de recursos avançado (tipos de dado customizados, extensões, forte suporte a dado geoespacial, entre outros). É o banco que mais cresceu em popularidade no mercado de dados nos últimos anos.
- **SQLite**: um SGBD que não roda como um servidor separado, ele vive dentro de um único arquivo no seu disco. Não precisa instalar servidor, configurar usuário, nada. É o banco que roda "escondido" dentro do seu navegador, do seu celular, de aplicativo desktop.
- **SQL Server**: SGBD proprietário da Microsoft, comum em empresa que já vive dentro do ecossistema Microsoft (Windows Server, .NET, Azure).
- **Oracle Database**: SGBD proprietário, historicamente forte em empresa grande, sistema financeiro e governo, conhecido também por ter licenciamento caro.

## Trade-offs: código aberto vs. proprietário, self-hosted vs. nuvem gerenciada

Duas perguntas separadas entram em jogo na hora de escolher um SGBD, e vale distinguir elas.

A primeira é **código aberto vs. proprietário**. SGBD open source (MySQL, PostgreSQL, SQLite) é gratuito, o código é público, e existe uma comunidade grande por trás. SGBD proprietário (SQL Server, Oracle) geralmente cobra licença, mas costuma vir com suporte oficial da empresa dona e integração mais profunda com o próprio ecossistema dela.

A segunda é **self-hosted vs. gerenciado na nuvem**. Self-hosted é você (ou sua empresa) instalando e mantendo o banco numa máquina própria, cuidando de backup, atualização, segurança, tudo na mão. Gerenciado na nuvem é pagar um provedor (AWS, Google Cloud, Azure, entre outros) pra cuidar dessa parte operacional pra você, e você só usa o banco. Essa segunda opção é assunto pro módulo de nuvem, ainda não escrito, então por enquanto fica só o gancho: por hoje, a gente vai instalar e rodar tudo local, na sua própria máquina.

## Qual banco esse repositório vai usar

Pra esse repositório, o banco principal vai ser o **PostgreSQL**. Ele é open source, então você não paga nada e não depende de licença, e é hoje um dos SGBDs mais usados no mercado de engenharia de dados, o que significa que o que você aprender aqui se aplica direto no trabalho real.

Se você só quer testar alguma coisa rapidinho, sem instalar servidor nenhum, o **SQLite** é uma alternativa zero-fricção: é só um arquivo, não precisa configurar usuário nem processo rodando em segundo plano. Mas pra seguir os exemplos desse repositório, especialmente quando a gente chegar em tópicos mais avançados, PostgreSQL vai ser a referência.

## Instalando o PostgreSQL

### Windows

Baixe o instalador oficial em [postgresql.org/download/windows](https://www.postgresql.org/download/windows/) e siga o assistente. Durante a instalação, ele vai pedir uma senha pro usuário administrador padrão (`postgres`), guarde ela, você vai precisar dela pra conectar depois.

### Mac

O jeito mais simples é via [Homebrew](https://brew.sh/): `brew install postgresql@16` e depois `brew services start postgresql@16` pra deixar o serviço rodando. Se preferir instalador gráfico, também tem opção em [postgresql.org/download/macosx](https://www.postgresql.org/download/macosx/).

### Linux

Na maioria das distribuições, o PostgreSQL está no próprio gerenciador de pacote. Em distro baseada em Debian/Ubuntu, por exemplo: `sudo apt install postgresql`. Em outras distros, o nome do pacote é parecido, vale checar o [postgresql.org/download/linux](https://www.postgresql.org/download/linux/) pro comando exato da sua distribuição.

### Confirmando que a instalação funcionou

Depois de instalado, abra um terminal e rode:

```
psql --version
```

Se aparecer um número de versão (tipo `psql (PostgreSQL) 16.x`), o cliente de linha de comando do PostgreSQL está instalado corretamente. Pra confirmar que o servidor está de pé e realmente respondendo, conecte com:

```
psql -U postgres
```

Ele vai pedir a senha que você definiu na instalação. Depois de conectado, rode:

```sql
SELECT version();
```

Se voltar uma linha descrevendo a versão do PostgreSQL, está tudo funcionando: você tem um SGBD de verdade rodando na sua máquina, pronto pra receber comando SQL.

## Fechando esse capítulo

Agora sim: SQL é a linguagem, PostgreSQL é o SGBD que vai executar ela na prática, e ele já está instalado e rodando na sua máquina. No próximo capítulo a gente larga de vez a teoria e começa a escrever consulta SQL de verdade, com exemplo prático rodando.
