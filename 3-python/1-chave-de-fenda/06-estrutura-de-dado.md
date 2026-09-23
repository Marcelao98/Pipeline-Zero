# Até dragões precisam de dados

## Era uma vez um cavaleiro...

O reino chora. A Princesa Anabela, a mais bela e bondosa de todas as princesas, foi levada para a Montanha Cinzenta e está presa nas garras de Brasa, o dragão mais terrível que esses vales já viram. Os bardos cantam seus gritos de socorro em todas as tavernas. E da taverna mais barulhenta de todas levanta-se ele, Sir Godofredo, cavaleiro de armadura reluzente e coração enorme, que bate a caneca na mesa e jura resgatar a princesa ou morrer tentando. Só falta uma coisa: alguém que saiba ler, escrever e organizar as anotações da missão. Esse alguém é você, o novo **escriba** do grupo.

Vocês sobem a montanha. Três dias de caminhada, duas brigas com goblin, uma noite dormindo na chuva. Chegam na torre onde a princesa está presa, e lá está o dragão, enorme, vermelho, bloqueando a porta. Sir Godofredo desembainha a espada. Você já sabe como essa história termina.

### Só que não

Enquanto o Godofredo faz o aquecimento (ele sempre alonga antes de atacar), você repara em umas coisas estranhas. O dragão não está atacando ninguém. Está sentado na porta da torre, soltando uma fumacinha triste pelo nariz. E lá de dentro, entre um "socorro" e outro, dá pra ouvir um barulhinho: um piado agudo, tipo de filhote.

Juntando as peças, a verdade aparece. A princesa não foi sequestrada. Foi ela quem subiu a montanha escondida, **roubou o filhote do Brasa** pra exibir no baile real como bichinho de estimação exótico, e se trancou na torre quando o dragão veio atrás. O Brasa não é o vilão. Ele é um pai querendo o filho de volta.

E o Sir Godofredo? Coração enorme, armadura reluzente e autocontrole zero. Ele está a três segundos de sair correndo, gritando, pra cima do lado errado da história.

Então a missão muda. Agora o objetivo é ajudar o dragão. E, antes de qualquer um fazer besteira, o primeiro passo é o seu, escriba: **colocar a informação em ordem**. Quem é quem, o que cada um carrega, o que é fato e o que é lenda de taverna.

Pra isso, uma variável guardando um valor só não dá conta. Você precisa guardar vários valores juntos, organizados, numa variável só. Isso tem nome: **estrutura de dado**. Python tem quatro principais (dicionário, lista, tupla e set), e cada uma serve pra um jeito diferente de organizar as coisas. Vamos ver uma por uma, no meio da missão.

## Dicionário: a ficha do personagem

Todo RPG de mesa tem a ficha do personagem: um papel onde está escrito o nome, a classe, os pontos de vida, e por aí vai. Cada linha da ficha é um par: um **nome do campo** e o **valor** dele. "Classe: Guerreiro". "PV: 45".

Com o que a gente viu até agora, o jeito de guardar isso seria uma variável pra cada informação:

```python
nome_godofredo = 'Sir Godofredo'
classe_godofredo = 'Guerreiro'
pv_godofredo = 45
autocontrole_godofredo = 0
```

Funciona, mas é o mesmo problema das `bomba_1`, `bomba_2` e `bomba_3` dos capítulos anteriores. As informações estão soltas, cada uma na sua variável, e nada no código diz que elas pertencem ao mesmo personagem. Agora faz isso pro dragão, pra princesa, e pros três goblins do caminho. São dezenas de variáveis com nome quase igual, e um erro de digitação faz você somar o PV do goblin no cavaleiro.

### Como se escreve um dicionário

O **dicionário** junta tudo isso numa coisa só:

```python
ficha_godofredo = {
    'Nome': 'Sir Godofredo',
    'Classe': 'Guerreiro',
    'PV': 45,
    'Autocontrole': 0
}
```

A estrutura é:

- **Chaves** `{ }` por fora, abrindo e fechando o dicionário.
- Dentro, cada linha é um par **chave: valor**, separado por dois pontos. A **chave** é o nome do campo (`'Classe'`) e o **valor** é o que está escrito nele (`'Guerreiro'`).
- Os pares são separados por vírgula.

O valor pode ser qualquer tipo que a gente já viu: texto, número inteiro, número com vírgula, booleano. E o nome "dicionário" faz sentido: igual num dicionário de papel, você procura pela palavra (a chave) e encontra o significado (o valor).

Não precisa quebrar em várias linhas, dá pra escrever tudo numa linha só. Mas, com mais de dois ou três pares, uma linha por par fica muito mais fácil de ler.

### Pegando um valor pela chave

Pra pegar um valor, você usa colchete, igual na string e na lista, só que em vez de posição, coloca a chave:

```python
print(ficha_godofredo['Classe'])        # Guerreiro
print(ficha_godofredo['Autocontrole'])  # 0
```

Essa é a grande diferença do dicionário: você não precisa lembrar em que posição está cada informação. Não interessa se o PV é o terceiro ou o décimo campo da ficha, você pede pelo nome e pronto.

### Adicionando e atualizando

Lembra do aquecimento do Godofredo? Pois é. Enquanto ele alongava, o Brasa virou de costas pra ir ver o filhote pela janela da torre, e o rabo acertou o cavaleiro em cheio. Sem querer, mas acertou. PV novo:

```python
ficha_godofredo['PV'] = 30
print(ficha_godofredo['PV'])  # 30
```

É o mesmo `=` de guardar valor em variável, do capítulo 2. Se a chave já existe, o valor dela é trocado. E se a chave **não** existe, o Python cria ela na hora:

```python
ficha_godofredo['Cavalo'] = 'Pé de Pano'
print(ficha_godofredo)
```

```
{'Nome': 'Sir Godofredo', 'Classe': 'Guerreiro', 'PV': 30, 'Autocontrole': 0, 'Cavalo': 'Pé de Pano'}
```

A ficha ganhou um campo novo, e o PV continua 30. Adicionar e atualizar são a mesma operação: se tem, troca; se não tem, cria.

E aqui vai o motivo de o dicionário aparecer tanto no dia a dia de dado: ele é praticamente um **registro**. Uma linha de tabela, lá do módulo de SQL, é exatamente isso: nome da coluna e valor. Uma leitura de sensor também:

```python
leitura = {'Bomba': 'BOMBA 01', 'Vibração': 4.2, 'Data': '21/09/2026'}
```

Quando você for buscar dado numa API, mais pra frente no módulo, é nesse formato de chave e valor que ele costuma chegar.

## Lista: o inventário da mochila

Todo aventureiro carrega uma mochila, e todo escriba que se preze anota o que tem nela. A mochila do Godofredo é uma **lista**: uma sequência de itens, um atrás do outro.

### Como se escreve uma lista

A lista já apareceu nos capítulos de string e de loop, e agora ela ganha o espaço dela:

```python
mochila = ['Espada', 'Escudo', 'Poção de cura', 'Poção de cura', 'Corda', 'Pão velho']
```

Colchetes por fora, itens separados por vírgula. E repara em duas coisas que são a cara da lista:

- **A ordem importa.** O primeiro item é a espada, o último é o pão velho, e a lista guarda os itens exatamente nessa ordem.
- **Pode repetir.** Tem duas poções de cura iguais, e isso não é erro: o Godofredo carrega duas mesmo. A lista não liga pra item repetido.

### Indexação: a mochila começa do zero

Pra pegar um item, é igualzinho à indexação da string, lá do capítulo 3. Colchete com a posição, e a contagem começa do **0**:

```python
print(mochila[0])   # Espada
print(mochila[2])   # Poção de cura
print(mochila[-1])  # Pão velho
```

O `-1` continua sendo o último item, sem precisar saber o tamanho da mochila.

### .append() e .remove(): pegando e usando item

A diferença da lista pra string é que a lista **pode ser alterada** depois de criada. Dá pra colocar e tirar item.

No caminho até a torre, vocês acharam um mapa da montanha. Pra colocar ele no fim da mochila, tem o `.append()`:

```python
mochila.append('Mapa da montanha')
print(mochila)
```

```
['Espada', 'Escudo', 'Poção de cura', 'Poção de cura', 'Corda', 'Pão velho', 'Mapa da montanha']
```

E depois da rabada, o Godofredo tomou uma poção. Pra tirar um item, tem o `.remove()`, passando o item que você quer tirar:

```python
mochila.remove('Poção de cura')
print(mochila)
```

```
['Espada', 'Escudo', 'Poção de cura', 'Corda', 'Pão velho', 'Mapa da montanha']
```

Repara que só **uma** poção sumiu. O `.remove()` tira o primeiro item igual que encontrar e para por aí. Faz sentido: ele tomou uma poção, não as duas.

E tem uma diferença importante em relação aos métodos de string. Lembra do aviso do capítulo 3, de que o método de string não altera o texto original e você precisa guardar o resultado de volta na variável? Com o `.append()` e o `.remove()` é o contrário: eles **alteram a própria lista**, direto. Não precisa (e nem deve) escrever `mochila = mochila.append(...)`.

A lista é, disparado, a estrutura mais usada do dia a dia. Toda vez que você tiver "vários de uma mesma coisa" (várias leituras, várias bombas, vários nomes), é bem provável que eles morem numa lista. E, juntando com o dicionário, aparece um formato que você vai ver o tempo todo: uma lista de dicionários, onde cada dicionário é um registro. É basicamente uma tabela inteira dentro do Python.

## Tupla: o que não muda nesse mundo

Algumas coisas nessa história mudam o tempo todo: o PV do cavaleiro, o que tem na mochila. Outras são regra do universo. A caverna do Brasa, por exemplo, fica num ponto fixo da Montanha Cinzenta, e montanha não muda de lugar. Pra guardar esse tipo de coisa, existe a **tupla**:

```python
caverna_brasa = (12, 47)
```

Parece uma lista, só que com **parênteses** no lugar de colchete. Aqui são as coordenadas no mapa: coluna 12, linha 47. A leitura funciona igual à lista:

```python
print(caverna_brasa[0])  # 12
```

A diferença é que a tupla **não pode ser alterada** depois de criada. Nem `.append()`, nem `.remove()`, nem trocar um valor. Se alguém tentar mover a caverna:

```python
caverna_brasa[0] = 13
```

O Python não deixa:

```
TypeError: 'tuple' object does not support item assignment
```

Traduzindo: "tupla não aceita troca de item". E isso é justamente a vantagem. Se as coordenadas estivessem numa lista, bastava uma linha errada em algum lugar do código pra caverna mudar de lugar sem ninguém perceber, e o grupo inteiro ia voltar pro endereço errado. Com tupla, a proteção vem de fábrica: o que é fixo fica fixo.

Quando usar tupla em vez de lista? Quando os valores formam um conjunto que não deve mudar: uma coordenada, uma data quebrada em dia, mês e ano, a faixa de operação de uma bomba (mínimo e máximo). Na dúvida, se é pra ir mudando, lista. Se é pra ficar como está, tupla.

## Set: título não se ganha duas vezes

O Godofredo, apesar de tudo, tem os títulos dele. E título é algo que você tem ou não tem. Ninguém é "Matador de Goblins" duas vezes. Pra isso existe o **set** (ou **conjunto**, em português): uma coleção onde **cada item aparece uma vez só**.

```python
titulos_godofredo = {'Matador de Goblins', 'Salvador de Gatos'}
```

É com chaves, igual ao dicionário, mas sem os pares de chave e valor, só os itens soltos. Pra adicionar um item, tem o `.add()`. E olha o que acontece quando o Godofredo derrota mais um goblin no caminho de volta:

```python
titulos_godofredo.add('Matador de Goblins')
print(titulos_godofredo)
```

```
{'Matador de Goblins', 'Salvador de Gatos'}
```

Nada mudou. O título já estava lá, então o set simplesmente ignora a repetição, sem dar erro nenhum.

Duas coisas pra saber sobre o set. Primeiro, ele **não guarda ordem**: se você rodar isso aí, os títulos podem aparecer em outra ordem na sua tela, e está tudo certo. Por isso não dá pra pegar item por posição, `titulos_godofredo[0]` dá erro. Pra saber se um item está lá, usa o `in`, igual na string. Segundo, pra criar um set vazio, é `set()`, e não `{}`, porque chave vazia o Python entende como dicionário vazio.

### Fora da história: tirando duplicata de dado real

Saindo um pouquinho da montanha e voltando pra planta. O uso mais comum de set no dia a dia de dado é **tirar duplicata**. Imagina a lista de bombas que deram alerta de vibração durante a semana. A mesma bomba aparece várias vezes, uma por alerta:

```python
bombas_em_alerta = ['BOMBA 03', 'BOMBA 07', 'BOMBA 03', 'BOMBA 12', 'BOMBA 07', 'BOMBA 03']
```

Seu chefe não quer saber quantos alertas teve. Ele quer saber **quais bombas** precisam de manutenção. É só transformar a lista em set, usando o `set()` com a lista dentro:

```python
bombas_para_manutencao = set(bombas_em_alerta)
print(bombas_para_manutencao)
```

```
{'BOMBA 03', 'BOMBA 07', 'BOMBA 12'}
```

Seis alertas, três bombas. (E de novo: a ordem pode sair diferente aí na sua tela.)

## enumerate(): numerando a mochila

De volta à missão. Antes do confronto final, o Godofredo pede pra você ler em voz alta o que tem na mochila, numerado, "pra ficar oficial". Com o `for` do capítulo anterior, você já sabe passar por cada item:

```python
for item in mochila:
    print(item)
```

Só que assim sai só o nome do item, sem número. Pra pegar a posição e o item ao mesmo tempo, existe o `enumerate()`:

```python
for posicao, item in enumerate(mochila):
    print(posicao, item)
```

```
0 Espada
1 Escudo
2 Poção de cura
3 Corda
4 Pão velho
5 Mapa da montanha
```

A novidade é que o `for` agora cria **duas** variáveis a cada volta, separadas por vírgula: a primeira recebe a posição, e a segunda recebe o item.

Só que ninguém numera lista de compras começando do zero (e o Godofredo muito menos). O `enumerate()` aceita um `start` pra dizer de onde começa a contagem:

```python
for numero, item in enumerate(mochila, start=1):
    print(f'{numero}. {item}')
```

```
1. Espada
2. Escudo
3. Poção de cura
4. Corda
5. Pão velho
6. Mapa da montanha
```

Agora sim, oficial.

## List comprehension: o mesmo for, numa linha só

O Godofredo, que é meio surdo de tanto levar pancada no elmo, pede pra você ler de novo, mais alto. Você resolve escrever tudo em maiúsculo. Com o que a gente já viu, dá pra montar uma lista nova assim:

```python
mochila_gritada = []

for item in mochila:
    mochila_gritada.append(item.upper())
```

Começa com uma lista vazia (`[]`), passa por cada item, e coloca a versão em maiúsculo na lista nova. Funciona. Mas esse padrão (pegar uma lista, fazer alguma coisa com cada item e montar outra lista) é tão comum que Python tem um atalho pra ele, a **list comprehension**:

```python
mochila_gritada = [item.upper() for item in mochila]
print(mochila_gritada)
```

```
['ESPADA', 'ESCUDO', 'POÇÃO DE CURA', 'CORDA', 'PÃO VELHO', 'MAPA DA MONTANHA']
```

É o mesmo `for`, escrito dentro dos colchetes, numa linha só. Dá pra ler quase em português: "o item em maiúsculo, para cada item na mochila". Não é obrigatório usar, o `for` de três linhas faz exatamente a mesma coisa. Mas você vai encontrar isso em todo código Python por aí, então vale reconhecer quando aparecer.

## Lista, tupla, dicionário ou set?

Antes do final da história, um resumo lado a lado, porque a pergunta de verdade no dia a dia não é "como escreve", e sim "qual eu uso":

| | Lista | Tupla | Dicionário | Set |
|---|---|---|---|---|
| Escreve com | `[ ]` | `( )` | `{chave: valor}` | `{ }` (vazio: `set()`) |
| Pega item por | posição | posição | chave | não pega, só confere com `in` |
| Guarda a ordem? | sim | sim | sim | não |
| Pode repetir? | sim | sim | a chave não | não |
| Dá pra alterar? | sim | não | sim | sim |
| Na história | a mochila | a caverna | a ficha | os títulos |

E em uma linha cada:

- **Lista:** vários itens de uma mesma coisa, em ordem, que vão mudando. É a escolha padrão.
- **Tupla:** poucos valores que andam juntos e não devem mudar.
- **Dicionário:** informação com nome, onde você quer pegar cada valor pelo nome do campo, e não pela posição.
- **Set:** quando o que importa é saber se algo existe e cada coisa aparece uma vez só (tirar duplicata é o caso clássico).

Escolher errado raramente quebra o programa. Só deixa ele mais difícil de ler, ou mais fácil de estragar sem querer. É a caverna que muda de lugar porque estava numa lista, ou o PV que você não acha porque a ficha virou uma lista e você não lembra se ele era o terceiro ou o quarto item.

## O dragão, o filhote e a princesa

Hora do confronto final, que no fim nem foi confronto. Você segura o Godofredo pelo braço (de novo), mostra as anotações, e ele finalmente entende. Guarda a espada, bate na porta da torre, e pede com toda a educação que a princesa mostre o que tem na bolsa.

Pra conferir se o filhote está lá dentro, entra um velho conhecido: o `in`. O mesmo `in` que você viu procurando um trecho dentro de uma string, e que apareceu lá no set pra conferir se um título existe, funciona do mesmo jeito pra saber se um item está dentro de uma lista. Responde `True` ou `False`, e pronto.

Em código, a resolução da história fica assim:

```python
inventario_princesa = ['Coroa', 'Espelho', 'Filhote de dragão', 'Leque']
ficha_brasa = {'Espécie': 'Dragão vermelho', 'PV': 300, 'Humor': 'Furioso'}
titulos_godofredo = {'Matador de Goblins', 'Salvador de Gatos'}
caverna_brasa = (12, 47)

if 'Filhote de dragão' in inventario_princesa:
    inventario_princesa.remove('Filhote de dragão')
    ficha_brasa['Humor'] = 'Feliz'
    titulos_godofredo.add('Amigo dos Dragões')
    print(f'Filhote devolvido! Levando pra caverna, nas coordenadas {caverna_brasa}.')

humor = ficha_brasa['Humor']
print(f'Humor do Brasa: {humor}')

print('O que sobrou na bolsa da princesa:')
for numero, item in enumerate(inventario_princesa, start=1):
    print(f'{numero}. {item}')

print('Amigo dos Dragões' in titulos_godofredo)
```

Rodando isso, a tela mostra:

```
Filhote devolvido! Levando pra caverna, nas coordenadas (12, 47).
Humor do Brasa: Feliz
O que sobrou na bolsa da princesa:
1. Coroa
2. Espelho
3. Leque
True
```

Cada estrutura fez o papel dela. A **lista** guardou a bolsa da princesa, e o `in` do capítulo de string, junto com o `if` do capítulo 4, encontrou o filhote lá dentro. O `.remove()` tirou ele de lá. O **dicionário** teve o humor do Brasa atualizado pela chave. O **set** ganhou um título novo (e, se o Godofredo ajudar mais dragões por aí, esse título nunca vai aparecer duplicado). A **tupla** guiou todo mundo até a caverna, que continua exatamente onde sempre esteve. E o `enumerate()` numerou o que sobrou na bolsa.

O filhote voltou pro ninho, o Brasa soltou uma fumacinha feliz, e a princesa... bom, a princesa vai ter que explicar pro rei por que chegou no baile sem bichinho de estimação. E o Sir Godofredo desceu a montanha com o título novo, jurando que desde o começo tinha desconfiado da história.

Não tinha.

## Fechando esse capítulo

Estrutura de dado é o jeito de guardar vários valores juntos, organizados, numa variável só, em vez de espalhar tudo em dezenas de variáveis soltas. O **dicionário** guarda pares de chave e valor, igual a uma ficha de personagem ou um registro de tabela, e você pega, atualiza e adiciona valor pela chave. A **lista** guarda uma sequência em ordem, aceita repetição, e muda com `.append()` e `.remove()`, que alteram a própria lista. A **tupla** é parecida com a lista, só que não muda, e isso protege o que é fixo. O **set** não repete item nem guarda ordem, e é a ferramenta clássica pra tirar duplicata. Pra percorrer uma lista pegando posição e item juntos tem o `enumerate()`, e a list comprehension monta uma lista nova a partir de outra numa linha só.

No próximo capítulo a gente vê **função**, ou seja, como empacotar um pedaço de lógica pra reaproveitar sem precisar escrever tudo de novo.
