# Comparação e condicional: ensinando o programa a decidir

## Se estiver chovendo...

Até aqui, todo código que a gente escreveu rodou em linha reta. Faz isso, depois isso, depois aquilo, e acabou. Guarda um valor numa variável, calcula, limpa um texto, mostra na tela. Sempre na mesma ordem, sempre do mesmo jeito, não importa o valor que estiver ali dentro.

Só que a vida real raramente funciona em linha reta. A gente toma decisão o tempo todo, muitas vezes sem nem perceber. Você olha pela janela antes de sair de casa e pensa: "se está chovendo, eu levo guarda-chuva". Pronto, isso é uma decisão. Dependendo de uma condição, você faz uma coisa ou outra.

Com programa é igual. Um programa que só sabe seguir a lista de instruções na ordem é um programa burro: ele faz sempre a mesma coisa, mesmo quando a situação muda. O que transforma ele num programa útil é a capacidade de decidir. E é disso que esse capítulo trata.

## O que existia antes

Sem condicional no código, quem decide é você. O programa calcula, mostra o resultado na tela, e aí você olha e resolve o que fazer. É o mesmo problema do "na mão" que a gente viu no capítulo de string: funciona quando são poucos casos, e para de funcionar quando são milhares, ou quando a mesma decisão precisa ser tomada todo dia.

Se você já mexeu com Excel, talvez já tenha usado a ideia sem saber o nome. A função `SE()` faz exatamente isso:

```
=SE(A1>80; "alto"; "normal")
```

"Se o valor da célula A1 for maior que 80, escreve alto. Senão, escreve normal." O que a gente vai ver aqui é a mesma lógica, só que dentro do código, e com muito mais liberdade.

## Comparação: verdadeiro ou falso

Antes de decidir qualquer coisa, o programa precisa responder uma pergunta de sim ou não. "Está chovendo?" "A temperatura passou de 80?" "Esse texto é igual àquele?" Pra fazer essas perguntas, existem os **operadores de comparação**. Usando `7` e `2` de novo, igual na lista de operadores matemáticos do capítulo 2:

- `==` igual a: `7 == 2` dá `False`.
- `!=` diferente de: `7 != 2` dá `True`.
- `>` maior que: `7 > 2` dá `True`.
- `<` menor que: `7 < 2` dá `False`.
- `>=` maior ou igual a: `7 >= 7` dá `True`.
- `<=` menor ou igual a: `7 <= 2` dá `False`.

Repara no resultado de cada uma. Não é número, não é texto. É sempre `True` (verdadeiro) ou `False` (falso). Lembra do **booleano** (`bool`), o quarto tipo básico lá do capítulo 2? Na hora ele parecia meio sem utilidade, mas é aqui que ele entra em cena: **toda comparação devolve um booleano**. E dá pra guardar esse resultado numa variável, igual qualquer outro valor:

```python
chance_de_chuva = 70
vai_chover = chance_de_chuva > 50
print(vai_chover)  # True
```

Guarda bem essa ideia, porque o resto do capítulo inteiro se apoia nela: uma comparação é uma pergunta, e a resposta é sempre `True` ou `False`.

Agora, um aviso que vale ouro, porque essa é a confusão número 1 de quem está começando: **`=` e `==` são coisas completamente diferentes**. Um `=` sozinho guarda um valor na variável (é o "guarda isso aqui dentro" do capítulo 2). Dois `==` comparam se dois valores são iguais. Trocar um pelo outro é um erro que todo mundo comete, e mais de uma vez.

E comparar texto também funciona, com um detalhe que você já conhece do capítulo anterior:

```python
print('bomba' == 'BOMBA')  # False
```

Pro Python, maiúscula e minúscula continuam fazendo diferença. Se for comparar texto, padroniza antes.

## if e else: a primeira decisão

Agora que a gente sabe fazer uma pergunta que vira `True` ou `False`, dá pra tomar uma decisão em cima dela. Pra isso existe o `if` ("se", em inglês):

```python
chovendo = True

if chovendo:
    print('Vou levar o guarda-chuva.')
```

Lendo em português: "se está chovendo, mostra na tela que vou levar o guarda-chuva". A estrutura é sempre essa: a palavra `if`, a condição, os **dois pontos** no final da linha, e embaixo o que deve acontecer se a condição for verdadeira.

Como `chovendo` já é um booleano, dá pra usar ele direto como condição. Mas a condição também pode ser uma comparação, que no fim vira booleano do mesmo jeito:

```python
chance_de_chuva = 70

if chance_de_chuva > 50:
    print('Vou levar o guarda-chuva.')
```

### O recuo não é enfeite

Repara que a linha do `print()` está deslocada pra direita, com quatro espaços antes. Isso se chama **indentação** (ou recuo), e em Python ela **não é enfeite**. É justamente o recuo que diz pro Python quais linhas estão "dentro" do `if`, ou seja, quais linhas só rodam se a condição for verdadeira.

Isso pega muita gente que vem de outra linguagem, e muita gente que não vem de linguagem nenhuma. Em várias outras linguagens, o que marca o começo e o fim do bloco é um par de chaves `{ }`, e o recuo é só pra deixar bonito. Em Python não tem chave: o recuo é a regra.

Olha a diferença:

```python
chovendo = False

if chovendo:
    print('Vou levar o guarda-chuva.')
print('Saindo de casa.')
```

A primeira mensagem está recuada, então só aparece se estiver chovendo. A segunda está encostada na margem, fora do `if`, então aparece sempre. Rodando isso com `chovendo = False`, a tela mostra só `Saindo de casa.`

E se você esquecer o recuo de vez, o Python nem roda o programa:

```python
chovendo = True

if chovendo:
print('Vou levar o guarda-chuva.')
```

Ele reclama na hora:

```
IndentationError: expected an indented block after 'if' statement on line 3
```

Traduzindo: "eu esperava um bloco recuado depois do `if`". Quando aparecer esse erro, já sabe onde olhar. O padrão é usar quatro espaços, e o VS Code já faz isso sozinho quando você aperta a tecla Tab, então na prática você quase não precisa se preocupar.

### else: o senão

E se não estiver chovendo? Pra isso tem o `else` ("senão"):

```python
chovendo = False

if chovendo:
    print('Vou levar o guarda-chuva.')
else:
    print('Deixo o guarda-chuva em casa.')
```

Se a condição do `if` for verdadeira, roda o primeiro bloco. Se for falsa, roda o bloco do `else`. Nunca os dois, sempre um deles. Repara que o `else` também leva dois pontos e também tem o bloco dele recuado.

## elif: quando tem mais de dois caminhos

O `if` com `else` resolve bem quando só existem dois caminhos, tipo chove ou não chove. Mas nem tudo na vida é sim ou não. Pensa num semáforo: ele tem três cores, e cada uma pede uma ação diferente. Pra isso existe o `elif` (abreviação de "else if", ou "senão, se"):

```python
cor = 'amarelo'

if cor == 'vermelho':
    print('Pare.')
elif cor == 'amarelo':
    print('Atenção, vai fechar.')
elif cor == 'verde':
    print('Pode seguir.')
else:
    print('Semáforo com defeito, redobra a atenção.')
```

Rodando isso, a tela mostra `Atenção, vai fechar.`

Você pode colocar quantos `elif` precisar. O `else` no final é opcional, mas costuma ser uma boa ideia: ele pega qualquer situação que você não previu (um semáforo piscando, quebrado, ou alguém que digitou a cor errada).

E um detalhe importante: o Python testa as condições **de cima pra baixo**, e **para no primeiro que der `True`**. Assim que uma condição é verdadeira, ele roda aquele bloco e pula todo o resto, sem nem olhar as condições de baixo. Isso vai ser importante lá nos trade-offs.

## Operador lógico: and, or, not

Voltando pro guarda-chuva. Às vezes uma condição só não basta pra decidir. Tipo: "se está chovendo **e** tem vento forte, eu nem saio de casa". Aqui são duas condições juntas, e a decisão depende das duas. Pra juntar condições, existem os **operadores lógicos**.

### and: as duas precisam ser verdadeiras

```python
chovendo = True
vento_forte = True

if chovendo and vento_forte:
    print('Hoje eu nem saio de casa.')
```

O `and` ("e") só dá `True` se **as duas** condições forem verdadeiras. Se só estiver chovendo, sem vento, ele dá `False`, e o bloco não roda.

### or: basta uma ser verdadeira

```python
chovendo = False
sol_forte = True

if chovendo or sol_forte:
    print('Vou levar o guarda-chuva.')
```

O `or` ("ou") dá `True` se **pelo menos uma** das condições for verdadeira. Guarda-chuva serve tanto pra chuva quanto pra sol forte, então qualquer uma das duas já é motivo pra levar.

Se ajudar, dá pra resumir os dois numa tabelinha:

| Condição A | Condição B | A `and` B | A `or` B |
|---|---|---|---|
| True | True | True | True |
| True | False | False | True |
| False | True | False | True |
| False | False | False | False |

### not: inverte

O `not` ("não") é o mais simples dos três. Ele só inverte o valor: o que era `True` vira `False`, e o que era `False` vira `True`.

```python
chovendo = False

if not chovendo:
    print('Dá pra sair sem guarda-chuva.')
```

Lendo em português: "se **não** está chovendo, dá pra sair sem guarda-chuva".

## Condicional aninhado: if dentro de if

Só pra você não se assustar quando encontrar por aí: dá pra colocar um `if` dentro do bloco de outro `if`. Isso se chama **condicional aninhado**:

```python
chovendo = True
tenho_guarda_chuva = False

if chovendo:
    if tenho_guarda_chuva:
        print('Saio com o guarda-chuva.')
    else:
        print('Vou me molhar.')
else:
    print('Saio sem preocupação.')
```

Repara que o `if` de dentro tem o próprio recuo, somado ao recuo do `if` de fora. É o recuo que diz quem está dentro de quem. Primeiro o Python decide se está chovendo, e só se estiver ele vai pra segunda pergunta.

Funciona, e às vezes é o jeito mais claro de escrever. Mas não é algo pra usar à toa, e o motivo está logo abaixo.

## Trade-offs: onde isso começa a apertar

**Aninhar demais vira uma escadinha.** Um `if` dentro de outro é tranquilo de ler. Três ou quatro, um dentro do outro, viram uma escada de recuo que ninguém consegue acompanhar, nem você mesmo uma semana depois. Muitas vezes dá pra trocar o `if` dentro de `if` por um `and` numa linha só, e o código fica bem mais fácil de ler.

**A ordem do elif pode esconder um bug.** Lembra que o Python para na primeira condição verdadeira? Olha o que acontece se a condição mais ampla vier antes da mais específica:

```python
chance_de_chuva = 90

if chance_de_chuva > 30:
    print('Leva o guarda-chuva.')
elif chance_de_chuva > 80:
    print('Nem sai de casa.')
```

Com 90% de chance de chuva, você esperava `Nem sai de casa.`, mas a tela mostra `Leva o guarda-chuva.` Como 90 também é maior que 30, a primeira condição já dá `True`, e o Python nem chega no `elif`. Na verdade, esse `elif` nunca vai rodar, com valor nenhum. O programa não dá erro nenhum, ele só faz a coisa errada em silêncio. A solução é colocar a condição mais específica (`> 80`) primeiro.

**Comparar texto sem padronizar dá errado.** Se o seu semáforo receber `'Vermelho'` com V maiúsculo, ele cai no `else` do "semáforo com defeito", porque `'Vermelho' == 'vermelho'` dá `False`. É exatamente a sujeira do capítulo de string, agora quebrando decisão em vez de relatório. Padroniza antes (com `.lower()`, por exemplo) e compara depois.

## Exemplo prático: juntando tudo

Pra fechar, a decisão completa de sair de casa, juntando comparação, `and`, `or`, `if`, `elif` e `else`:

```python
chance_de_chuva = 70  # em porcentagem
vento_kmh = 45
ceu_nublado = True

if chance_de_chuva >= 60 and vento_kmh > 40:
    print('Chuva com vento forte: hoje eu nem saio de casa.')
elif chance_de_chuva >= 60 or ceu_nublado:
    print('Vou sair, mas levo o guarda-chuva.')
else:
    print('Pode sair tranquilo, sem guarda-chuva.')
```

Rodando isso, a tela mostra:

```
Chuva com vento forte: hoje eu nem saio de casa.
```

As duas comparações do `if` deram `True` (70 é maior ou igual a 60, e 45 é maior que 40), então o `and` deu `True`, e o Python parou ali mesmo.

Agora muda só o vento pra `vento_kmh = 10` e roda de novo. A primeira condição passa a dar `False`, porque o vento não é mais forte. O Python desce pro `elif`, onde basta uma das condições ser verdadeira, e a chance de chuva ainda está alta. A tela mostra `Vou sair, mas levo o guarda-chuva.`

E se o dia estiver limpo de vez, com `chance_de_chuva = 10` e `ceu_nublado = False`, nenhuma condição dá `True`, e quem responde é o `else`: `Pode sair tranquilo, sem guarda-chuva.`

Repara também na ordem: o caso mais específico (chuva **e** vento) vem primeiro, e o mais amplo (chuva **ou** céu nublado) vem depois. Se fosse ao contrário, a gente cairia exatamente no bug do trade-off lá de cima.

É o mesmo código, com os mesmos três caminhos, e ele decide sozinho qual seguir dependendo do valor que chega. Esse é o salto de um programa burro pra um programa útil.

## Fechando esse capítulo

Todo programa precisa decidir, e toda decisão começa com uma pergunta de sim ou não. Os operadores de comparação (`==`, `!=`, `>`, `<`, `>=`, `<=`) fazem essa pergunta e sempre devolvem um booleano, `True` ou `False`. Em cima disso, o `if` decide o que rodar, o `else` cobre o "senão", e o `elif` resolve quando tem mais de dois caminhos, testando de cima pra baixo e parando no primeiro verdadeiro. O `and`, o `or` e o `not` juntam ou invertem condições. E em Python o recuo não é enfeite: é ele que diz o que está dentro de cada bloco.

No próximo capítulo a gente vê a outra metade da estrutura de controle: como fazer o programa **repetir** uma ação várias vezes, sem você precisar escrever a mesma linha de novo (loop).
