# Marido de aluguel

## Todo mundo é marido de aluguel de alguma coisa

Não tem jeito. Uma hora, todo mundo vira o marido (ou a esposa) de aluguel de alguma coisa. Pode ser o chuveiro que parou de esquentar, a tomada da cozinha que faz um barulhinho suspeito, a descarga da casa da mãe que só funciona se segurar a alavanca por exatos quatro segundos. Você não é encanador, não é eletricista, não é nada disso, mas o chuveiro não quer saber. Ele parou, e alguém vai ter que resolver.

Na indústria é igual, só que com placa de patrimônio. Motor queima, sensor pifa, bomba começa a vibrar mais do que devia. E quem trabalha com manutenção sabe que o serviço de verdade não é fazer a máquina funcionar no dia em que tudo está bem. É saber o que fazer no dia em que ela quebra. Porque ela vai quebrar.

E código também quebra. Não é questão de "se", é questão de "quando". Uma leitura que chega vazia, um arquivo que não está onde devia, um dado que veio escrito errado. O capítulo anterior terminou avisando que, na cozinha e no código, uma hora alguma coisa queima. Esse capítulo é sobre o que fazer quando queima.

## Dica número um: o Google é seu amigo

Antes de qualquer linha de código, a dica mais importante do capítulo (talvez do módulo inteiro).

Quando o erro aparecer, e ele vai aparecer, sempre, **copia a mensagem de erro e joga no Google**. Sério. Essa é, disparado, a habilidade mais usada por qualquer pessoa que programa. O iniciante faz isso. O sênior com quinze anos de carreira faz isso. A diferença é que o sênior faz sem vergonha nenhuma, porque já sabe que todo mundo faz.

A chance de você ser a primeira pessoa do planeta a tomar aquele erro é praticamente zero. Alguém já passou por isso, já perguntou num fórum, e alguém já respondeu. Seu trabalho é achar essa resposta e entender por que ela resolve.

Então tira esse peso das costas: ninguém espera que você saiba tudo de cor. Nem o eletricista mais experiente decora o esquema de todo chuveiro que existe. Ele sabe onde procurar. É isso.

## O que é uma exceção

Quando o programa encontra uma situação que ele não sabe resolver sozinho, ele não improvisa. Ele para tudo e avisa. Isso tem nome: **exceção**. É o famoso "quebrou".

Olha um exemplo. Imagina um chuveiro metido a inteligente, que anota a temperatura da água de cada banho. Só que hoje ele queimou logo cedo, antes do primeiro banho, e o programa tenta calcular a temperatura média dos banhos do dia mesmo assim:

```python
total_temperatura = 0
quantidade_banhos = 0

print('Calculando a temperatura média dos banhos...')
media = total_temperatura / quantidade_banhos
print(f'Temperatura média: {media}')
```

```
Calculando a temperatura média dos banhos...
ZeroDivisionError: division by zero
```

Traduzindo: "divisão por zero". O chuveiro queimou, ninguém tomou banho, a quantidade é zero, e nem o Python consegue dividir alguma coisa por zero. Então ele para ali mesmo. Repara que a última linha, a que mostraria a média, **nunca rodou**. O programa não pulou o problema e seguiu em frente. Ele simplesmente parou.

É o chuveiro que parou de funcionar e ninguém fez nada a respeito ainda. A água está fria, o banho acabou, e vai continuar assim até alguém ir lá mexer.

E aqui vai uma notícia boa: você já tomou erro nesse módulo, mais de uma vez. O `IndentationError` do capítulo 5, quando faltou o recuo. O `TypeError` do capítulo 7, quando alguém tentou mudar a caverna do Brasa de lugar. O `NameError` do capítulo 8, quando o suco não saiu da cozinha. Tudo isso era exceção, só não tinha ganhado esse nome ainda.

## Os defeitos mais comuns

Todo técnico de manutenção tem a lista dos defeitos que mais aparecem. Resistência queimada, disjuntor desarmado, fio solto. Em Python também tem os clássicos, e o nome do erro (a primeira palavra da mensagem) já diz qual defeito é.

### ValueError: o valor não serve

Lembra da mochila do Sir Godofredo, lá do capítulo 7? Depois de mais umas rabadas do Brasa, as poções de cura acabaram. Só que o Godofredo, que não conta nada, tenta tomar mais uma:

```python
mochila = ['Espada', 'Escudo', 'Corda', 'Pão velho']
mochila.remove('Poção de cura')
```

```
ValueError: list.remove(x): x not in list
```

Traduzindo: "o item não está na lista". O `.remove()` foi procurar a poção, não achou, e não tem como tirar da mochila uma coisa que não está lá. O `ValueError` aparece quando o tipo até está certo (é um texto, igual aos itens da mochila), mas o **valor** não serve pra aquela operação. Guarda esse nome, porque ele volta no exemplo do final do capítulo.

### KeyError: a chave não existe

Agora a ficha do personagem. O Godofredo decide que quer lançar uma magia:

```python
ficha_godofredo = {'Nome': 'Sir Godofredo', 'Classe': 'Guerreiro', 'PV': 30}
print(ficha_godofredo['Mana'])
```

```
KeyError: 'Mana'
```

Traduzindo: "não existe a chave `'Mana'`". Guerreiro não tem mana, Godofredo. O dicionário foi procurar esse campo na ficha, não achou, e parou tudo. O `KeyError` é o defeito clássico de pedir pra um dicionário uma chave que ele não tem.

### ZeroDivisionError: dividir por zero

Esse você já conhece, foi o do chuveiro queimado. Aparece sempre que alguma conta tenta dividir por zero, e no mundo de dado isso acontece bem mais do que parece: é só a lista chegar vazia na hora de calcular uma média.

### TypeError: o tipo não combina

E pra fechar a lista, um que você já viu na caverna do Brasa. O `TypeError` aparece quando você tenta fazer uma operação com um tipo que não combina com ela. Um exemplo que pega muita gente, somar texto com número:

```python
vibracao = '4.2'
print(vibracao + 1)
```

```
TypeError: can only concatenate str (not "int") to str
```

Traduzindo: "só dá pra juntar texto com texto, não com número". O `'4.2'` está entre aspas, então pro Python ele é texto, não número, e texto não soma com `1`. É tentar ligar um aparelho de 220 V numa tomada de 110 V: os dois são "eletricidade", mas não combinam.

## try/except: o conserto de emergência

Até aqui, em todos os casos, o programa quebrou e parou. Só que nem todo defeito precisa derrubar tudo. Às vezes você já sabe que aquele problema pode acontecer, e já sabe o que fazer quando ele acontecer. Pra isso existe o **try/except**:

```python
total_temperatura = 0
quantidade_banhos = 0

try:
    media = total_temperatura / quantidade_banhos
    print(f'Temperatura média: {media}')
except ZeroDivisionError:
    print('Nenhum banho hoje, o chuveiro queimou. Não dá pra calcular a média.')

print('Programa continua.')
```

```
Nenhum banho hoje, o chuveiro queimou. Não dá pra calcular a média.
Programa continua.
```

Dá pra ler quase em português: "**tenta** (try) fazer isso aqui. Se der `ZeroDivisionError`, **em vez de parar tudo** (except), faz aquilo ali". A estrutura é a mesma do `if` do capítulo 5: dois pontos no final da linha, e o que pertence a cada parte vai recuado embaixo dela.

O que acontece por dentro:

- O Python começa a rodar o que está dentro do `try`, linha por linha.
- Se nenhuma linha der erro, o `except` é ignorado e o programa segue normalmente.
- Se alguma linha der erro, o Python **para o `try` ali mesmo** (as linhas que vinham depois dela dentro do `try` não rodam) e pula direto pro `except`.
- Depois do `except`, o programa continua como se nada tivesse acontecido.

Repara na última linha. Sem o try/except, `Programa continua.` nunca ia aparecer. Com ele, o defeito foi tratado e a vida seguiu. É o chuveiro que parou, mas dessa vez alguém já deixou uma resistência reserva na gaveta.

## Um except pra cada defeito

Um `try` pode ter mais de um `except`, um pra cada tipo de erro. E isso é bom, porque defeito diferente pede conserto diferente:

```python
mochila = ['Espada', 'Escudo', 'Corda', 'Pão velho']
ficha_godofredo = {'Nome': 'Sir Godofredo', 'Classe': 'Guerreiro', 'PV': 30}

try:
    mochila.remove('Poção de cura')
    print(ficha_godofredo['Mana'])
except ValueError:
    print('Acabou a poção. Alguém tem um pão velho aí?')
except KeyError:
    print('Guerreiro não tem mana, Godofredo.')
```

```
Acabou a poção. Alguém tem um pão velho aí?
```

A primeira linha do `try` já deu `ValueError`, então o Python pulou direto pro `except ValueError`. A linha da mana nem chegou a rodar. Se a mochila tivesse poção, o `.remove()` passaria tranquilo, a linha da mana daria `KeyError`, e a mensagem seria a outra. Cada defeito cai no conserto certo.

### O except que pega tudo

Existe um jeito de escrever o `except` sem dizer tipo nenhum:

```python
try:
    mochila.remove('Poção de cura')
except:
    print('Acabou a poção.')
```

Esse `except:` sozinho pega **qualquer** erro, seja qual for. Parece prático, né? Pra que ficar escolhendo tipo, se dá pra pegar tudo de uma vez?

Porque pegar tudo significa também pegar o que você não esperava. Olha o que acontece se você errar a digitação do nome da variável:

```python
try:
    mochla.remove('Poção de cura')
except:
    print('Acabou a poção.')
```

```
Acabou a poção.
```

O problema real aqui é um `NameError` (não existe nada chamado `mochla`), aquele mesmo do capítulo 8. Mas o `except` genérico engoliu o erro e mostrou a mensagem da poção. O programa **mentiu pra você**. E você vai passar meia hora procurando por que a poção acabou, sendo que o defeito era uma letra faltando.

É o eletricista que, pra qualquer problema na casa, desliga o disjuntor geral. Lâmpada queimada? Desliga o geral. Tomada solta? Desliga o geral. Curto-circuito? Desliga o geral. Resolver, até resolve, mas ele nunca sabe qual era o defeito de verdade, e a casa inteira fica no escuro por causa de uma lâmpada.

Por isso a regra é: **diz qual erro você está esperando**. `except ValueError`, `except KeyError`, o que for. Aí só o defeito que você já sabe consertar é tratado, e qualquer coisa inesperada continua aparecendo pra você ver.

## .get(): consertar antes de quebrar

Manutenção tem dois tipos. A **corretiva** é a que conserta depois que quebrou: o motor queimou, você troca. A **preventiva** é a que evita que quebre: você troca o rolamento antes de o motor queimar. As duas têm seu lugar, mas quando dá pra prevenir, geralmente é melhor.

O try/except é manutenção corretiva: deixa o erro acontecer e trata depois. Mas tem casos em que dá pra evitar o erro antes dele existir. O `KeyError` do dicionário é o exemplo perfeito, porque o dicionário tem um método feito pra isso, o `.get()`:

```python
ficha_godofredo = {'Nome': 'Sir Godofredo', 'Classe': 'Guerreiro', 'PV': 30}

print(ficha_godofredo.get('Mana'))
```

```
None
```

Em vez de quebrar, o `.get()` devolve `None`, aquele "nada" do capítulo 8. A chave não existe, e ele simplesmente te avisa disso sem parar o programa.

E fica melhor: dá pra dizer o que ele deve devolver quando a chave não existir, passando um segundo valor:

```python
print(ficha_godofredo.get('Mana', 0))  # 0
print(ficha_godofredo.get('PV', 0))    # 30
```

Se a chave existe, vem o valor dela (o PV continua 30). Se não existe, vem o valor que você escolheu (mana zero, que é exatamente quanto mana o Godofredo tem). Sem try, sem except, sem erro nenhum.

E a mochila? Pra ela você já conhece a preventiva desde o final do capítulo 7, só não sabia que era isso. Antes de tirar o filhote de dragão da bolsa da princesa, o código conferia com `if 'Filhote de dragão' in inventario_princesa:`. Confere antes, tira depois. Se não estiver lá, o `.remove()` nem é chamado, e o `ValueError` nunca acontece.

Então, quando for possível checar antes, checa. O try/except fica pros casos em que não dá pra prever, ou em que checar seria mais trabalhoso do que tratar.

## finally: a ferramenta volta pra caixa

Deu certo ou não deu, todo serviço termina do mesmo jeito: recolhe a ferramenta, religa o disjuntor, limpa a sujeira. Isso não depende de o conserto ter funcionado. Pra esse "roda sempre, no final" existe o **finally**:

```python
try:
    vibracao = float('#&%')
    print(f'Vibração: {vibracao}')
except ValueError:
    print('Leitura com defeito.')
finally:
    print('Leitura encerrada, próximo sensor.')
```

```
Leitura com defeito.
Leitura encerrada, próximo sensor.
```

(O `float()` transforma texto em número com vírgula, e ele vai ser explicado direitinho no exemplo lá embaixo. Por enquanto, basta saber que `'#&%'` não é número nenhum, então dá `ValueError`.)

O que está dentro do `finally` roda **sempre**: se o `try` deu certo, roda; se deu erro e caiu no `except`, roda também. É o lugar da arrumação do fim, aquilo que precisa acontecer de qualquer jeito. Não é algo que você vai usar toda hora, mas vale reconhecer quando aparecer.

## Trade-offs: onde isso começa a apertar

**Esconder o erro em vez de tratar.** O pior uso de try/except é esse aqui:

```python
try:
    mochila.remove('Poção de cura')
except ValueError:
    pass
```

O `pass` é a palavra do Python pra "não faz nada". Então o erro acontece e... nada. Nenhuma mensagem, nenhum aviso, nenhum registro. É o conserto com fita isolante que ninguém fica sabendo que foi feito. Funciona hoje, e daqui a seis meses alguém descobre que metade dos dados sumiu sem explicação. Se você vai tratar um erro, pelo menos deixa um aviso de que ele aconteceu.

**try gigante.** Colocar 50 linhas dentro de um `try` só, com um `except` no final. Quando cair no `except`, qual das 50 linhas deu problema? Ninguém sabe. É como o eletricista que, em vez de testar circuito por circuito, troca a fiação da casa inteira porque "alguma coisa não está funcionando". Deixa dentro do `try` só a linha (ou as poucas linhas) que podem dar aquele erro específico.

**Tratar erro que devia parar o programa.** Nem todo erro deve ser tratado. Às vezes, o programa parar é exatamente o que precisa acontecer, porque continuar com um dado errado é pior do que não continuar. Um defeito que você não sabe consertar é melhor aparecer na tela do que ficar escondido.

## Exemplo prático: o sensor que manda lixo

Lembra do exemplo do final do capítulo 6? As leituras de vibração chegavam numa lista, e quando aparecia um `'ERRO'` no meio, o `break` parava **tudo**. As leituras que vinham depois do erro nunca eram processadas. Na época era o que dava pra fazer. Agora dá pra fazer melhor.

Dessa vez, as leituras chegam do jeito que dado de verdade costuma chegar: uma lista de dicionários (o formato de "tabela dentro do Python" do capítulo 7), com a vibração vindo como texto, do jeito que o sensor manda. E, claro, com defeito no meio:

```python
leituras = [
    {'Bomba': 'BOMBA 01', 'Vibração': '4.2'},
    {'Bomba': 'BOMBA 02', 'Vibração': '#&%'},   # o sensor mandou lixo
    {'Bomba': 'BOMBA 03'},                      # veio sem a vibração
    {'Bomba': 'BOMBA 04', 'Vibração': '9.4'},
    {'Bomba': 'BOMBA 05', 'Vibração': '5.0'},
]
```

Antes do código, uma ferramenta nova e rapidinha: o **`float()`**. Ele pega um texto e tenta transformar em número com vírgula. `float('4.2')` vira o número `4.2`, e aí dá pra fazer conta (lembra do `TypeError` de somar texto com número? É isso que resolve). Mas se o texto não for número nenhum, tipo `'#&%'` ou um texto vazio, o `float()` não tem o que fazer e dá `ValueError`. É exatamente aí que entra o try/except.

A ideia é: passar por cada leitura, pular (e anotar) as que vieram com defeito, avisar quando alguma passar do limite de 7.0, e no final mostrar a média das leituras boas:

```python
leituras = [
    {'Bomba': 'BOMBA 01', 'Vibração': '4.2'},
    {'Bomba': 'BOMBA 02', 'Vibração': '#&%'},
    {'Bomba': 'BOMBA 03'},
    {'Bomba': 'BOMBA 04', 'Vibração': '9.4'},
    {'Bomba': 'BOMBA 05', 'Vibração': '5.0'},
]
limite = 7.0


def mostrar_media(total, quantidade):
    """Mostra a média de vibração. Se nenhuma leitura prestou, avisa em vez de quebrar."""
    try:
        media = total / quantidade
        print(f'Média de vibração: {media}')
    except ZeroDivisionError:
        print('Nenhuma leitura válida, não dá pra calcular a média.')


total = 0
validas = 0
sensores_com_defeito = []

for leitura in leituras:
    bomba = leitura['Bomba']

    try:
        vibracao = float(leitura.get('Vibração', ''))
    except ValueError:
        print(f'{bomba}: leitura com defeito, pulando.')
        sensores_com_defeito.append(bomba)
        continue

    total = total + vibracao
    validas = validas + 1

    if vibracao > limite:
        print(f'{bomba}: ALERTA, vibração de {vibracao}, acima do limite.')
    else:
        print(f'{bomba}: vibração de {vibracao}, tudo normal.')

print(f'Leituras válidas: {validas}')
mostrar_media(total, validas)
print(f'Sensores pra conferir: {sensores_com_defeito}')
```

Rodando isso, a tela mostra:

```
BOMBA 01: vibração de 4.2, tudo normal.
BOMBA 02: leitura com defeito, pulando.
BOMBA 03: leitura com defeito, pulando.
BOMBA 04: ALERTA, vibração de 9.4, acima do limite.
BOMBA 05: vibração de 5.0, tudo normal.
Leituras válidas: 3
Média de vibração: 6.2
Sensores pra conferir: ['BOMBA 02', 'BOMBA 03']
```

Acompanhando leitura por leitura:

- **BOMBA 01:** o `.get()` acha a vibração, o `float()` transforma `'4.2'` em número, e segue o caminho normal.
- **BOMBA 02:** o `.get()` acha a vibração, mas ela é `'#&%'`. O `float()` dá `ValueError`, o `except` anota a bomba na lista de defeito, e o `continue` do capítulo 6 pula pra próxima leitura.
- **BOMBA 03:** aqui nem tem a chave `'Vibração'`. Se o código usasse `leitura['Vibração']`, ia dar `KeyError` e parar tudo. Mas o `.get()` preveniu: devolveu o valor padrão `''` (texto vazio), o `float('')` deu `ValueError`, e caiu no mesmo `except` da BOMBA 02. Dois defeitos diferentes, um conserto só.
- **BOMBA 04 e 05:** caminho normal, uma em alerta e uma tranquila.

E a diferença pro capítulo 6 está justamente aí: o defeito no meio da lista **não parou o processamento**. As duas bombas depois dele foram lidas normalmente, e as leituras com defeito não sumiram em silêncio, foram anotadas pra alguém ir conferir o sensor.

E a função `mostrar_media()`? Com três leituras boas, ela só calcula e mostra. Mas imagina o dia em que **todos** os sensores mandarem lixo. Aí `validas` fica em zero, e sem o try/except dentro da função o programa ia quebrar com aquele `ZeroDivisionError` do começo do capítulo, bem no finalzinho, depois de ter processado tudo. Com o try/except, ela só avisa que não tem média pra mostrar.

Olha quanta coisa trabalhando junto: o **try/except** com erro específico em dois lugares, o **`.get()`** com valor padrão prevenindo o `KeyError`, a **lista de dicionários** do capítulo 7, o **`for`** e o **`continue`** do capítulo 6, o **`if`/`else`** do capítulo 5, e uma **função** com docstring do capítulo 8. Cinco leituras ou cinco mil, com defeito ou sem, o programa vai até o fim.

## Fechando esse capítulo

Código quebra, igual a qualquer equipamento, e quando quebra, a primeira ferramenta é copiar a mensagem de erro e procurar no Google, coisa que todo mundo faz, do iniciante ao sênior. Uma **exceção** é quando o programa encontra algo que não sabe resolver sozinho e para tudo, e o nome do erro já diz qual é o defeito: `ValueError` (o valor não serve), `KeyError` (a chave não existe), `ZeroDivisionError` (divisão por zero), `TypeError` (o tipo não combina). O **try/except** tenta rodar um trecho e, se der o erro esperado, faz outra coisa em vez de parar tudo. O certo é sempre dizer qual erro você está esperando, porque o `except` genérico pega até o que você não previa e esconde o defeito de verdade. Quando dá pra prevenir, melhor ainda: o **`.get()`** evita o `KeyError` antes de ele acontecer, e o `in` confere se o item está na lista antes do `.remove()`. O **finally** roda no final, deu erro ou não. E tratar um erro nunca pode virar esconder um erro.

Com isso, o Bloco 1 está fechado. No próximo capítulo a gente faz uma pausa pra olhar pra trás antes de seguir pro Bloco 2.
