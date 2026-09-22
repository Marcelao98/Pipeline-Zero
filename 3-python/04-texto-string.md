# Texto (string): o dado que mais dá trabalho pra limpar

## A mesma bomba com cinco nomes

Antes de migrar pra dados, eu trabalhei em planta industrial. E uma coisa que eu vi de perto, sem nem saber que isso tinha nome, é que o maior inimigo de quem trabalha com dado não é o volume, nem a ferramenta. É o campo de texto livre.

Imagina um formulário de manutenção onde cada técnico escreve o nome do equipamento do jeito que quiser. Num mês de relatório, a mesma bomba aparece assim:

- `Bomba 01`
- `BOMBA 01` (o técnico que escreve tudo com o Caps Lock ligado, toda planta tem um)
- `bomba 01` (o que tem preguiça de apertar o Shift)
- `" Bomba 01 "` (esse aqui é o mais traiçoeiro, porque o espaço sobrando no começo e no fim nem aparece na tela)

E não para no nome do equipamento. A medição que um escreve como `Temperatura`, o outro escreve `Temp`, e o terceiro, caprichoso, escreve `Temp.` com ponto. A data do mesmo relatório vem como `21/09/2026` numa linha e `21-09-2026` na outra.

Pra qualquer pessoa da planta, é tudo a mesma bomba, a mesma medição e o mesmo dia. Pro computador, são coisas completamente diferentes. Se você pedir pra ele contar quantas manutenções a Bomba 01 teve no mês, ele vai contar cada variação como um equipamento separado, e o seu relatório sai errado sem nenhum aviso.

Esse é, de longe, o problema mais comum que qualquer pessoa em dados vai encontrar, seja analista, seja engenheiro. E a caixa de ferramentas pra atacar ele é justamente o assunto desse capítulo: como Python trabalha com texto.

## O que é uma string

A string já apareceu no capítulo anterior como um dos tipos básicos: é o tipo que guarda texto. Agora é hora de olhar pra ela por dentro.

Pra criar uma string, você coloca o texto entre aspas. Pode ser aspas simples ou duplas, pro Python dá na mesma:

```python
equipamento = 'Bomba 01'
equipamento = "Bomba 01"
```

As duas linhas fazem exatamente a mesma coisa. A diferença aparece quando o próprio texto tem aspas dentro. Se você escrever `'Bomba d'água'` com aspas simples, o Python acha que a string terminou no apóstrofo do `d'` e se perde. Nesse caso, usa aspas duplas por fora:

```python
equipamento = "Bomba d'água"
```

E quando o texto tem mais de uma linha (uma observação de campo num relatório, por exemplo), dá pra usar três aspas:

```python
observacao = '''Bomba 01 com ruído anormal.
Verificar rolamento na próxima parada.'''
```

## O que existia antes

Antes de ter código pra isso, a limpeza era na mão. Abre a planilha, olha linha por linha, corrige o que está errado. Quem é mais esperto usa o "Localizar e substituir" do Excel e troca tudo de uma vez.

Isso funciona quando a planilha tem 20 linhas. Não funciona quando tem 200 mil. E, principalmente, não funciona quando o relatório chega de novo toda semana, com as mesmas sujeiras de sempre (e algumas novas), e você precisa repetir a mesma limpeza toda vez, torcendo pra não esquecer nenhum passo. Código faz a mesma limpeza, sempre do mesmo jeito, quantas vezes precisar.

## Indexação e fatiamento: pegando um pedaço do texto

Em planta, é comum o equipamento ter uma tag (um código de identificação) que junta várias informações num texto só. Por exemplo:

```python
tag = 'AREA2-BOMBA-01'
```

Aqui dentro tem a área, o tipo de equipamento e o número. E muitas vezes você só quer um desses pedaços.

Pra isso, você precisa saber que cada caractere de uma string tem uma posição, chamada **índice**. E o detalhe que confunde todo mundo no começo: a contagem começa do **0**, não do 1.

| Caractere | A | R | E | A | 2 | - | B | O | M | B | A | - | 0 | 1 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Índice | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 |

Pra pegar um caractere, você usa colchete com o índice:

```python
print(tag[0])   # A
print(tag[-1])  # 1
```

O índice negativo conta de trás pra frente: `-1` é o último caractere, `-2` o penúltimo, e assim por diante. Muito útil quando você quer o final do texto e não sabe (nem quer saber) o tamanho dele.

Pra pegar um pedaço inteiro, você usa **fatiamento**, informando onde começa e onde termina, separado por dois pontos:

```python
print(tag[6:11])  # BOMBA
```

Olha a tabela de novo: o `B` de `BOMBA` está no índice 6, e o último `A` está no 10. Mesmo assim, o fatiamento é `[6:11]`, e não `[6:10]`. Isso porque o número do fim **não entra** no resultado. É a pegadinha clássica, e todo mundo erra isso algumas vezes antes de acostumar.

Só que o fatiamento tem uma limitação séria no mundo real: ele depende da posição. Funciona perfeitamente se todas as tags tiverem exatamente o mesmo tamanho. Se aparecer uma `AREA10-VALVULA-003`, o `[6:11]` pega lixo. Pra esse caso tem uma ferramenta melhor, que aparece logo abaixo.

## Métodos do dia a dia de limpeza

Uma string sabe fazer uma série de coisas sozinha. Essas ações se chamam **métodos**, e você chama um método colocando um ponto depois do texto (ou da variável), o nome do método e parênteses:

```python
equipamento.upper()
```

Antes de ver os métodos, um aviso que vale ouro: **o método não altera o texto original**. Ele devolve um texto novo, já modificado. Se você não guardar esse texto novo em algum lugar, a limpeza se perde:

```python
equipamento = ' Bomba 01 '
equipamento.strip()
print(equipamento)  # ' Bomba 01 ' (continua sujo!)

equipamento = equipamento.strip()
print(equipamento)  # 'Bomba 01' (agora sim)
```

Esse é o erro mais comum de quem está começando: chamar o método, achar que limpou, e seguir com o dado sujo. Guarda o resultado de volta na variável.

Agora sim, os métodos, cada um atacando um dos problemas lá da abertura.

### .strip(): espaço sobrando

Tira os espaços do começo e do fim do texto (os do meio ficam, ainda bem):

```python
equipamento = ' Bomba 01 '
equipamento = equipamento.strip()
print(equipamento)  # Bomba 01
```

### .upper() e .lower(): padronizando maiúscula e minúscula

`.upper()` deixa tudo maiúsculo e `.lower()` deixa tudo minúsculo. Não importa muito qual dos dois você escolhe, o que importa é escolher um e aplicar em tudo:

```python
print('Bomba 01'.upper())  # BOMBA 01
print('bomba 01'.upper())  # BOMBA 01
print('BOMBA 01'.upper())  # BOMBA 01
```

Três técnicos diferentes, um resultado só.

### .replace(): trocando um trecho por outro

Você informa o que quer trocar e pelo que quer trocar:

```python
medicao = 'Temp.'
medicao = medicao.replace('Temp.', 'Temperatura')
print(medicao)  # Temperatura

data = '21-09-2026'
data = data.replace('-', '/')
print(data)  # 21/09/2026
```

É o "Localizar e substituir" do Excel, só que dentro do código.

### .split(): quebrando o texto em partes

Lembra da tag que o fatiamento não dava conta? O `.split()` quebra o texto em pedaços, usando o separador que você informar:

```python
tag = 'AREA2-BOMBA-01'
partes = tag.split('-')
print(partes)  # ['AREA2', 'BOMBA', '01']
```

Esse resultado entre colchetes é uma **lista**, que tem capítulo próprio mais pra frente. Por agora, basta saber que você pega cada pedaço pela posição, do mesmo jeito da indexação:

```python
print(partes[1])  # BOMBA
```

E a grande vantagem: isso funciona com `AREA2-BOMBA-01` e com `AREA10-VALVULA-003`, porque o `.split()` não se importa com o tamanho de cada pedaço, só com onde está o separador.

### .join(): o inverso do split

Se o `.split()` quebra, o `.join()` junta. Você escreve o separador que quer usar, e passa os pedaços:

```python
partes = ['AREA2', 'BOMBA', '01']
print('-'.join(partes))  # AREA2-BOMBA-01
print(' '.join(partes))  # AREA2 BOMBA 01
```

A sintaxe parece de trás pra frente no começo (o separador vem antes, e não depois), mas é assim mesmo.

### in: esse trecho existe no texto?

Às vezes você não quer mudar nada, só saber se um trecho aparece dentro do texto. Pra isso tem o `in`, que responde com `True` ou `False`:

```python
tag = 'AREA2-BOMBA-01'
print('BOMBA' in tag)    # True
print('VALVULA' in tag)  # False
```

Útil, por exemplo, pra saber se uma tag é de bomba ou de válvula sem precisar recortar nada.

## Encaixando variável no texto com f-string

No capítulo anterior, pra mostrar variável no meio de uma frase, a gente separou tudo por vírgula dentro do `print()`:

```python
print(nome_cliente, 'pediu', quantidade_pedido, 'unidade(s), valor total de', valor_total)
```

Funciona, mas fica difícil de ler, cheio de aspa abrindo e fechando. O jeito padrão hoje em Python é a **f-string**: você coloca um `f` antes das aspas e escreve a variável entre chaves, direto dentro do texto:

```python
equipamento = 'BOMBA 01'
area = 'AREA2'
print(f'Equipamento {equipamento} na área {area}')
# Equipamento BOMBA 01 na área AREA2
```

Você lê a linha e já enxerga exatamente como a frase vai sair na tela. É isso que a gente vai usar daqui pra frente.

## Trade-offs: onde isso começa a apertar

Esses métodos resolvem muita coisa, mas têm limite, e é bom conhecer antes de tropeçar nele.

**Eles são literais, então a ordem importa.** O `.replace()` troca exatamente o que você mandou, onde quer que apareça. Olha o que acontece se você tentar padronizar `Temp` pra `Temperatura` num texto que já estava certo:

```python
print('Temperatura'.replace('Temp', 'Temperatura'))  # Temperaturaeratura
```

Ele achou o `Temp` dentro de `Temperatura` e trocou, gerando uma palavra que não existe. Parece piada, mas é exatamente o tipo de coisa que acontece com dado real e passa despercebido.

**Maiúscula e minúscula fazem diferença.** Pro Python, `'bomba'` e `'BOMBA'` são textos diferentes, então o `in` e o `.replace()` também diferenciam:

```python
print('bomba' in 'BOMBA 01')  # False
```

A solução é padronizar a caixa primeiro (com `.upper()` ou `.lower()`) e só depois procurar ou trocar.

**Padrão complicado demais.** Quando a sujeira fica muito variada (tipo "qualquer sequência de números seguida de um traço e duas letras"), esses métodos simples começam a virar uma gambiarra atrás da outra. Pra esses casos existe uma ferramenta própria chamada **regex** (expressão regular). Ela existe, é poderosa, e fica pra outro momento.

**O melhor remédio é na origem.** Se o formulário da planta tivesse uma lista fechada de equipamentos pra escolher, em vez de campo de texto livre, metade desse capítulo nem seria necessária. Só que, na vida real, quem trabalha com dado quase sempre recebe ele já sujo, e não tem como voltar no tempo e consertar o formulário.

## Exemplo prático: juntando tudo

Voltando pra abertura. Três registros do mesmo equipamento, cada um escrito de um jeito, mais uma medição com abreviação:

```python
equip_1 = ' Bomba 01 '
equip_2 = 'BOMBA 01'
equip_3 = 'bomba 01'
medicao = ' temp. '

equip_1 = equip_1.strip().upper()
equip_2 = equip_2.strip().upper()
equip_3 = equip_3.strip().upper()
medicao = medicao.strip().upper().replace('TEMP.', 'TEMPERATURA')

print(f'{equip_1} | {equip_2} | {equip_3}')
print(f'Medição: {medicao}')
```

Rodando isso, a tela mostra:

```
BOMBA 01 | BOMBA 01 | BOMBA 01
Medição: TEMPERATURA
```

Repara em duas coisas. Primeiro, dá pra chamar um método atrás do outro na mesma linha (`.strip().upper()`): o resultado de um vira a entrada do próximo, da esquerda pra direita. Segundo, a ordem fez diferença na linha da medição: como o `.upper()` vem antes do `.replace()`, o texto já está maiúsculo quando chega na troca, então o `.replace()` procura `'TEMP.'`, e não `'temp.'`.

Três jeitos diferentes de escrever viraram um só. Agora o computador enxerga o que qualquer pessoa da planta já enxergava: é tudo a mesma bomba.

## Fechando esse capítulo

String é o tipo que guarda texto, e é nele que mora a maior parte da sujeira que você vai encontrar em dado real. Dá pra pegar pedaço de texto por posição com indexação e fatiamento, e limpar com métodos como `.strip()`, `.upper()`, `.lower()`, `.replace()`, `.split()` e `.join()`, lembrando sempre de guardar o resultado de volta na variável. O `in` confere se um trecho existe no texto, e a f-string é o jeito padrão de encaixar variável dentro de uma frase. E esses métodos são literais: a ordem importa, e maiúscula é diferente de minúscula.

No próximo capítulo a gente entra na próxima peça do bloco de fundamento: **comparação e condicional**, ou seja, como fazer o programa tomar decisão.
