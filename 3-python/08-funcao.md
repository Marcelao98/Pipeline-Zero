# Função: do pão com manteiga ao bolo

## A receita que ninguém reescreve

O que cozinhar tem a ver com função de Python? Pode não parecer, mas na verdade, tudo.

Pensa no bolo de domingo. Ninguém acorda, entra na cozinha e reinventa o bolo do zero, testando quanto de farinha vai, quantos ovos, quanto tempo de forno. Alguém (geralmente a vó) já fez esse trabalho uma vez, anotou tudo no caderno de receitas, e desde então todo mundo só abre o caderno e segue. Quer bolo de novo semana que vem? Abre o caderno de novo. Quer de chocolate em vez de cenoura? Mesma receita, troca um ingrediente.

Escrever uma vez, repetir sempre que precisar, variando só o que muda. Guarda essa ideia, porque o capítulo inteiro é ela.

### O que existia antes

Sem função, o jeito de repetir um pedaço de código é o de sempre: copiar e colar. É o mesmo problema da abertura do capítulo 6, só que pior. Lá era uma linha repetida. Aqui são blocos inteiros, de cinco, dez, vinte linhas, colados em vários lugares do programa.

E o problema de verdade aparece no dia em que você precisa mudar alguma coisa. Descobriu que o bolo fica melhor com 45 minutos de forno em vez de 40? Agora você precisa achar **todos** os lugares onde colou aquele bloco e corrigir um por um. Esqueceu um? Aquele bolo sai cru, e ninguém sabe por quê.

### O que é uma função

**Função** é um pedaço de código com nome, que você escreve uma vez e chama sempre que precisar. É a receita anotada no caderno: ela tem um nome ("bolo de cenoura"), tem os passos, e pode ser usada quantas vezes você quiser. E se um dia a receita mudar, você corrige num lugar só, e todo bolo dali pra frente já sai do jeito novo.

Além de evitar repetição, a função organiza. Um programa de duzentas linhas corridas é um caderno sem título nenhum, tudo escrito numa página só. Um programa dividido em funções com nome bom é um caderno com índice: você bate o olho e sabe onde está cada coisa.

### Você já usa função (e nem sabia)

Aqui vai uma revelação: você usa função desde o capítulo 3. O `print()` é uma função. O `input()` também. E o `range()`, o `enumerate()`, o `set()`... todos são receitas que alguém já escreveu, deixou prontas, e você só chama pelo nome, colocando entre parênteses o que ela precisa.

Você nunca precisou saber **como** o `print()` faz pra mostrar texto na tela. Só precisou saber o nome dele e o que passar pra ele. A novidade desse capítulo é que agora você vai escrever as suas próprias receitas.

E a gente vai fazer isso do jeito que se aprende a cozinhar: começando pelo mais simples de todos e subindo aos poucos, até chegar no bolo.

## O pão com manteiga: a primeira função

Não existe receita mais básica que pão com manteiga. Então é por ela que a gente começa:

```python
def fazer_pao_com_manteiga():
    print('Pega o pão.')
    print('Corta ao meio.')
    print('Passa manteiga.')
    print('Pão com manteiga pronto!')
```

Peça por peça:

- `def`: abreviação de "define". É a palavra que avisa o Python "lá vem uma receita nova".
- `fazer_pao_com_manteiga`: o nome da função. As regras são as mesmas do nome de variável, e a dica também: nome que diga o que a função faz.
- `()`: os parênteses. Aqui estão vazios, porque o pão com manteiga não precisa de nenhuma informação de fora pra ser feito. Já já eles ganham utilidade.
- Os **dois pontos** no final da linha, igual no `if` e no `for`.
- Embaixo, o **corpo** da função, recuado. O recuo continua sem ser enfeite: tudo que está recuado debaixo do `def` faz parte da receita.

Agora roda isso aí.

Nada. Tela vazia.

Não, não está quebrado. É que você só **escreveu a receita no caderno**. Escrever a receita não faz pão aparecer na mesa. Pra isso, alguém precisa ir pra cozinha e seguir a receita. Em Python, isso se chama **chamar** a função, e é só escrever o nome dela com os parênteses:

```python
fazer_pao_com_manteiga()
```

```
Pega o pão.
Corta ao meio.
Passa manteiga.
Pão com manteiga pronto!
```

Agora sim. E se a família inteira quiser pão com manteiga, é só chamar de novo, quantas vezes precisar, sem reescrever nenhum passo. **Definir** (o `def`) é escrever no caderno. **Chamar** (o nome com parênteses) é cozinhar.

## Parâmetro: e se hoje for requeijão?

O pão com manteiga resolve, mas tem gente em casa que prefere requeijão. E tem o sobrinho que só come se for com doce de leite. Escrever uma função pra cada recheio (`fazer_pao_com_requeijao()`, `fazer_pao_com_doce_de_leite()`...) seria voltar pro copiar e colar.

A receita é a mesma. Só muda **um ingrediente**. E é pra isso que servem os parênteses:

```python
def fazer_pao(recheio):
    print('Pega o pão.')
    print('Corta ao meio.')
    print(f'Passa {recheio}.')
    print(f'Pão com {recheio} pronto!')
```

Esse `recheio` dentro dos parênteses é um **parâmetro**: uma variável que a função recebe de fora, na hora em que é chamada. Quem decide o valor dela é quem chama:

```python
fazer_pao('requeijão')
fazer_pao('doce de leite')
```

```
Pega o pão.
Corta ao meio.
Passa requeijão.
Pão com requeijão pronto!
Pega o pão.
Corta ao meio.
Passa doce de leite.
Pão com doce de leite pronto!
```

Uma receita só, três recheios, e dá pra ter quantos você quiser. O valor que você passa na hora de chamar (o `'requeijão'`) tem o nome de **argumento**. Na prática, muita gente usa "parâmetro" e "argumento" como se fossem a mesma coisa, e tudo bem. Se quiser a diferença exata: parâmetro é o espaço reservado na receita, argumento é o ingrediente de verdade que você coloca ali.

E dá pra ter mais de um parâmetro, separado por vírgula. Isso aparece logo mais.

## return: o suco que vai pro copo

Até aqui, as funções **fazem** alguma coisa: mostram os passos na tela, e acabou. Só que muitas vezes você não quer só que a função faça, você quer que ela **entregue** alguma coisa, pra você usar depois.

Pensa num suco. Você não faz suco pra ficar olhando pro liquidificador. O suco vai pro copo, e o copo vai pra mesa, junto com o resto do café da manhã. Pra função entregar um resultado, existe o `return` ("devolve", em inglês):

```python
def fazer_suco(fruta):
    suco = f'Suco de {fruta}'
    return suco
```

O `return` pega o valor e entrega pra quem chamou a função. E aí quem chamou pode guardar esse valor numa variável, igual qualquer outro:

```python
copo = fazer_suco('laranja')
print(f'Café da manhã servido: pão com manteiga e {copo}.')
```

```
Café da manhã servido: pão com manteiga e Suco de laranja.
```

Repara que a função `fazer_suco()` não mostra nada na tela sozinha. Ela só prepara e entrega. Quem decidiu mostrar foi o `print()` de fora, usando o que estava no `copo`. E podia ter feito outra coisa com ele: juntar numa lista, comparar com um `if`, mandar pra outra função. Uma vez que o valor voltou, ele é seu.

Essa é a diferença que vale guardar:

- **Função que faz uma ação** (tipo o `fazer_pao()`): executa os passos, e o efeito acontece ali dentro. Nada volta pra você.
- **Função que devolve um valor** (tipo o `fazer_suco()`): prepara o resultado e entrega com `return`, pra você usar onde quiser.

No dia a dia, a segunda é a mais útil, justamente porque o resultado não fica preso dentro da função. É como a maior parte das funções que você já usou funciona: o `input()`, por exemplo, devolve o que a pessoa digitou, e você guarda numa variável.

## Valor padrão: se não disser o tempo, são 40 minutos

Hora de ligar o forno. Uma função pra assar qualquer coisa, com dois parâmetros:

```python
def assar(o_que, minutos=40):
    print(f'Assando {o_que} por {minutos} minutos.')
```

Olha o `minutos=40` ali. Isso é um **valor padrão**: se quem chamar a função não disser o tempo, ela assume 40 minutos. Se disser, vale o que foi dito:

```python
assar('bolo')
assar('pão de queijo', 25)
```

```
Assando bolo por 40 minutos.
Assando pão de queijo por 25 minutos.
```

Na primeira chamada, ninguém falou de tempo, então foi o padrão. Na segunda, o `25` substituiu o `40`. É o forno com o botão já girado no tempo que você mais usa: na maioria das vezes, é só colocar a forma e ligar. Quando precisa de outro tempo, você gira.

Isso é muito útil quando uma função tem um valor que quase sempre é o mesmo. Você não obriga todo mundo a repetir o óbvio toda vez, mas deixa a porta aberta pra quem precisar mudar.

## Chamando pelo nome do parâmetro

Nas chamadas lá de cima, o Python descobriu quem era quem pela **ordem**: o primeiro valor foi pro primeiro parâmetro (`o_que`), o segundo foi pro segundo (`minutos`). Isso se chama **argumento posicional**.

Só que dá pra fazer diferente, e dizer explicitamente qual valor vai pra qual parâmetro, usando o nome dele. Isso se chama **argumento nomeado**:

```python
assar(minutos=25, o_que='pão de queijo')
```

```
Assando pão de queijo por 25 minutos.
```

Mesmo resultado, mesmo com a ordem trocada, porque agora o Python não precisa adivinhar nada: cada valor chega com uma etiqueta dizendo onde ele vai.

E o jeito mais comum no dia a dia é misturar os dois: o principal pela posição, e o resto pelo nome.

```python
assar('pão de queijo', minutos=25)
```

Parece frescura com dois parâmetros, mas imagina uma função com seis. `fazer_bolo('cenoura', 4, 45, True, 'média', 2)` não diz nada pra quem lê. Com nome, cada valor explica o que é, e você não precisa ficar abrindo a receita pra lembrar se o tempo era o terceiro ou o quarto parâmetro.

## Docstring: a descrição no topo da receita

Toda receita boa de caderno tem uma linha no topo, antes dos ingredientes: "Bolo fofinho de cenoura, rende 12 fatias, bom pro café da tarde". Você lê aquilo e já sabe se é a receita que está procurando, sem precisar ler os passos.

Função também tem isso. Chama **docstring**, e é um texto entre três aspas logo na primeira linha do corpo da função:

```python
def assar(o_que, minutos=40):
    """Assa qualquer coisa no forno. Se o tempo não for informado, usa 40 minutos."""
    print(f'Assando {o_que} por {minutos} minutos.')
```

São as mesmas três aspas do texto de várias linhas do capítulo de string. A diferença é o lugar: logo abaixo do `def`, ela vira a descrição oficial da função. E não é só enfeite pra quem abre o código: no VS Code, quando você passa o mouse em cima do nome da função, em qualquer lugar do programa, essa descrição aparece ali numa caixinha.

Pode parecer desnecessário numa função de duas linhas. Mas daqui a três meses, quando você (ou outra pessoa) abrir esse código sem lembrar de nada, a docstring é o que separa "entendi em cinco segundos" de "vou ter que ler tudo pra descobrir o que isso faz".

## Escopo: o que fica na tigela não sai da cozinha

Lembra da função do suco? Dentro dela, a gente criou uma variável chamada `suco`. Olha o que acontece se você tentar usar essa variável fora da função:

```python
def fazer_suco(fruta):
    suco = f'Suco de {fruta}'
    return suco

fazer_suco('laranja')
print(suco)
```

```
NameError: name 'suco' is not defined
```

Traduzindo: "não existe nada chamado `suco`". Mas como não existe, se a função acabou de criar?

É que **variável criada dentro de uma função só existe dentro dela**, e só enquanto ela está rodando. Quando a função termina, tudo que foi criado lá dentro some. Pensa na tigela onde você mistura a massa: ela é essencial durante o preparo, mas quando o bolo sai do forno, ninguém serve a tigela na mesa. O que sai da cozinha é o bolo. Esse "onde a variável existe" tem um nome, **escopo**.

E aí dá pra ver por que o `return` é tão importante. Ele é a porta de saída da cozinha. Se você quer usar o resultado fora da função, o caminho é devolver com `return` e guardar numa variável do lado de fora, igual a gente fez com o `copo`:

```python
copo = fazer_suco('laranja')
print(copo)  # Suco de laranja
```

Isso parece uma limitação, mas é uma proteção. Cada função tem a sua própria cozinha, e o que acontece lá dentro não bagunça a cozinha das outras. Duas funções podem ter uma variável chamada `suco` cada uma, sem uma atrapalhar a outra.

## Trade-offs: onde isso começa a apertar

**Esquecer o `return` e receber um prato vazio.** Essa é, de longe, a confusão mais comum de quem está começando. Olha essa função:

```python
def fazer_cafe():
    print('Café passado!')

xicara = fazer_cafe()
print(xicara)
```

```
Café passado!
None
```

A função mostrou a mensagem na tela, então parece que funcionou. Só que ela não tem `return`, então não devolveu nada. E quando uma função não devolve nada, o Python coloca na variável um valor especial chamado `None`, que é o jeito dele dizer "nada". A xícara está vazia. O café foi passado, mas ficou na cozinha. Mostrar na tela e devolver são coisas diferentes: `print()` é pra você ver, `return` é pro programa usar.

**Função que faz coisa demais.** Dá pra escrever uma `fazer_almoco_de_domingo()` que faz o arroz, o feijão, a carne, a salada, a sobremesa e ainda lava a louça. Mas aí, no domingo em que você só quer o arroz, não tem como. E quando o feijão sai salgado, você precisa procurar o erro no meio de cem linhas. O ideal é que cada função faça uma coisa só, e faça bem. Uma receita, um prato.

**Nome ruim.** `f1()`, `processa()`, `teste2()`. Nome de função é a primeira (e às vezes a única) coisa que as pessoas leem. `fazer_bolo()` diz o que faz. `f1()` obriga todo mundo a abrir a receita pra descobrir.

## Exemplo prático: finalmente, o bolo

Do pão com manteiga até aqui, a gente subiu um degrau por vez. Agora dá pra fazer o bolo, juntando não só tudo desse capítulo, mas boa parte do módulo:

```python
def fazer_bolo(sabor, ovos=3, minutos=40):
    """Faz um bolo do sabor escolhido e devolve o bolo pronto.

    Se não disser quantos ovos nem quanto tempo de forno,
    usa 3 ovos e 40 minutos.
    """
    ingredientes = ['farinha', 'açúcar', 'leite', f'{ovos} ovos', sabor]

    for ingrediente in ingredientes:
        print(f'Colocando {ingrediente} na tigela...')

    print(f'Assando por {minutos} minutos...')

    if sabor == 'chocolate':
        cobertura = 'brigadeiro'
    elif sabor == 'cenoura':
        cobertura = 'calda de chocolate'
    else:
        cobertura = 'açúcar de confeiteiro'

    return f'Bolo de {sabor} com cobertura de {cobertura}'


bolo_1 = fazer_bolo('chocolate')
bolo_2 = fazer_bolo('cenoura', ovos=4, minutos=45)

print(f'Na mesa: {bolo_1} e {bolo_2}.')
```

Rodando isso, a tela mostra:

```
Colocando farinha na tigela...
Colocando açúcar na tigela...
Colocando leite na tigela...
Colocando 3 ovos na tigela...
Colocando chocolate na tigela...
Assando por 40 minutos...
Colocando farinha na tigela...
Colocando açúcar na tigela...
Colocando leite na tigela...
Colocando 4 ovos na tigela...
Colocando cenoura na tigela...
Assando por 45 minutos...
Na mesa: Bolo de chocolate com cobertura de brigadeiro e Bolo de cenoura com cobertura de calda de chocolate.
```

Olha quanta coisa trabalhando junto aqui dentro:

- O `def` com três **parâmetros**, dois deles com **valor padrão**.
- A **docstring** no topo, explicando a receita.
- A **lista** de ingredientes, do capítulo 7, montada com f-string, do capítulo 4.
- O **`for`** do capítulo 6 passando por cada ingrediente.
- O **`if`, `elif` e `else`** do capítulo 5 escolhendo a cobertura pelo sabor.
- O **`return`** entregando o bolo pronto pra fora da cozinha.

E nas chamadas: o primeiro bolo usou só o sabor e deixou o resto no padrão. O segundo mudou os ovos e o tempo com **argumento nomeado**. Os dois resultados foram guardados em variáveis e só no final viraram frase na tela. A `ingredientes` e a `cobertura`, que só existem dentro da função, ficaram na cozinha, como tem que ser.

Uma receita escrita uma vez, dois bolos diferentes. E semana que vem, se der vontade de bolo de laranja, é uma linha só: `fazer_bolo('laranja')`.

## Fechando esse capítulo

Função é um pedaço de código com nome, que você escreve uma vez e chama sempre que precisar, igual a uma receita de caderno. Ela evita o copiar e colar, organiza o programa e dá nome pra cada pedaço de lógica. Você cria com `def`, e ela só roda quando é chamada. Os **parâmetros** são os ingredientes que mudam a cada chamada, e podem ter **valor padrão** pro caso de ninguém informar. Na hora de chamar, dá pra passar os valores pela ordem ou pelo nome do parâmetro. O **`return`** devolve o resultado pra quem chamou, e é diferente de só mostrar na tela: sem ele, o que volta é `None`, o prato vazio. A **docstring** descreve a função no topo, e as variáveis criadas lá dentro só existem lá dentro, porque o que fica na tigela não sai da cozinha.

No próximo capítulo a gente vê **tratamento de erro**, ou seja, o que fazer quando alguma coisa dá errado no meio da execução. Porque, na cozinha e no código, uma hora alguma coisa queima.
