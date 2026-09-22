# Variável e tipo de dado: como o programa guarda informação

No capítulo anterior a gente preparou o terreno, com o Python e o VS Code instalados e funcionando. Agora começa a parte prática de verdade, e o primeiro passo do bloco de fundamento é entender como um programa guarda informação. É a base de tudo que vem depois.

## Hello World

Antes de qualquer conceito, o primeiro código que qualquer pessoa roda em Python é este aqui:

```python
print('Olá, mundo!')
```

Rode esse comando no seu ambiente Python. Se aparecer `Olá, mundo!` na tela, é isso: seu ambiente está funcionando, e você acabou de rodar o primeiro código Python da sua vida. `print()` é o comando que manda Python mostrar alguma coisa na tela. Vamos usar ele bastante daqui pra frente, mas por enquanto o objetivo é só esse: confirmar que o ambiente responde.

## O que é uma variável

Uma variável é um espaço nomeado que guarda um valor, pra você poder usar e reaproveitar esse valor depois sem precisar escrever ele de novo toda hora.

```python
nome_cliente = 'Ana'
```

Aqui `nome_cliente` é o nome da variável, `=` é o comando que atribui o valor a ela (não é "igual" no sentido matemático, é "guarda isso aqui dentro"), e `'Ana'` é o valor guardado. A partir desse momento, toda vez que você usar `nome_cliente` no código, Python entende que você está falando de `'Ana'`.

## Que problema isso resolve

Sem variável, duas coisas ficam difíceis. Primeiro, se você precisa do mesmo valor em vários pontos do código, tem que digitar ele de novo em cada lugar, e se esse valor mudar, você precisa caçar e trocar em todos os lugares onde escreveu na mão. Segundo, e mais importante: sem variável não tem como guardar o resultado de um cálculo pra usar mais adiante.

```python
print(2 + 2)
```

Isso mostra `4` na tela, mas o resultado morre ali. Se eu quiser usar esse `4` de novo daqui a três linhas, não tenho como, porque ele nunca foi guardado em lugar nenhum. Comparando:

```python
soma = 2 + 2
print(soma)
print(soma * 10)
```

Agora o resultado do cálculo ficou guardado em `soma`, e eu reaproveito ele quantas vezes quiser.

## Tipos de dado básicos

Todo valor em Python tem um tipo, e o tipo define que operação faz sentido com aquele valor. Os quatro tipos básicos são:

- **string (texto)**: sequência de caractere, sempre entre aspas simples ou duplas. Exemplo: `'Ana'`.
- **int (número inteiro)**: número sem casa decimal. Exemplo: `3`.
- **float (número decimal)**: número com casa decimal. Exemplo: `29.90`.
- **bool (booleano)**: só existem dois valores possíveis, `True` (verdadeiro) ou `False` (falso).

Por que Python precisa diferenciar isso? Porque cada tipo se comporta diferente numa operação. Somar dois números é uma coisa:

```python
3 + 2
```

Isso dá `5`. Mas "somar" dois textos com o mesmo sinal `+` é outra coisa completamente diferente:

```python
'ma' + 'çã'
```

Isso dá `'maçã'`, ou seja, junta os dois textos em vez de somar. É o mesmo símbolo `+`, mas o comportamento muda de acordo com o tipo do dado. Por isso o tipo importa, mesmo que a gente não precise declarar ele na mão (mais sobre isso já já).

## Tipagem dinâmica: Python descobre o tipo sozinho

Em algumas linguagens, como Java ou C, você precisa declarar o tipo de cada variável na mão antes de usar ela. Em Python isso não é necessário: você só atribui o valor, e o próprio Python descobre o tipo sozinho, olhando pra o que você escreveu.

```python
quantidade_pedido = 3
preco_produto = 29.90
nome_cliente = 'Ana'
```

Python entende, sem você precisar avisar, que a primeira é `int`, a segunda é `float` e a terceira é `string`. Isso é chamado de **tipagem dinâmica**, e é um dos motivos de Python ser mais rápido de escrever no dia a dia. Não vou entrar em comparação mais profunda de linguagem aqui, só fica registrado que essa diferença existe.

## Exemplo prático

Reaproveitando o espírito do que a gente já viu em SQL (as tabelas `clientes`, `pedidos` e `produtos`), dá pra representar um pedacinho desse mundo com variável simples, sem precisar recriar o dataset inteiro:

```python
nome_cliente = 'Ana'
quantidade_pedido = 3
preco_produto = 29.90

valor_total = quantidade_pedido * preco_produto

print(nome_cliente, 'pediu', quantidade_pedido, 'unidade(s), valor total de', valor_total)
```

Rodando isso, a tela mostra:

```
Ana pediu 3 unidade(s), valor total de 89.7
```

Repara que a variável `valor_total` guardou o resultado de um cálculo (quantidade vezes preço), e esse resultado foi reaproveitado dentro do `print()` mais adiante. É exatamente o problema que variável resolve, na prática.

## Fechando esse capítulo

Variável é um espaço nomeado que guarda valor pra reaproveitar depois, e todo valor tem um tipo (string, int, float ou bool) que define como ele se comporta numa operação. Python usa tipagem dinâmica, então você não declara o tipo na mão, o próprio Python descobre sozinho.

No próximo capítulo a gente entra na próxima peça do bloco de fundamento: **estrutura de controle**, ou seja, como fazer o programa tomar decisão (condicional) e repetir uma ação várias vezes (loop).
