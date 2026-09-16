# Fluxo de trabalho: Claude Code + Obsidian

## Passo a passo

1. **Abra o Claude Code na pasta do projeto** (a mesma pasta que tem `.git`, `.obsidian`, `README.md` etc).

2. **Na primeira mensagem, peça pra ele se contextualizar antes de escrever qualquer coisa.** Exemplo de prompt:

   ```
   Antes de criar qualquer conteúdo, leia o README.md, os arquivos dentro de
   que-porra-e-essa/, e o PDF em CONTEXTO DO CLAUDE/. Absorva o tom de escrita
   (informal, direto, sem corporativês, sem travessão), a estrutura de módulos,
   e as convenções de link deste arquivo (Fluxo de trabalho: Claude Code +
   Obsidian). Depois confirme que entendeu antes de começarmos.
   ```

3. **Peça o módulo novo direto, nomeando a pasta e o padrão a seguir.** Exemplo:

   ```
   Crie a pasta onde-o-dado-mora/ com o primeiro arquivo, sobre bancos de dados
   relacionais (o que é, por que existe, tabela, linha, coluna, chave primária,
   chave estrangeira). Siga exatamente o mesmo tom e formato dos arquivos de
   que-porra-e-essa/.
   ```

4. **Revise o que ele escreveu abrindo no Obsidian.** Se algo estiver fora do tom, corrija no próprio Claude Code pedindo o ajuste, igual se faz aqui no chat.

5. **Depois de revisar, peça pra ele commitar.** Exemplo:

   ```
   Adiciona tudo e commita com a mensagem "adiciona módulo de bancos de dados
   relacionais".
   ```

6. Repete esse ciclo (contexto já absorvido nas próximas vezes, não precisa repetir o passo 2 toda hora dentro da mesma sessão) pra cada novo módulo.

## Convenções de link e formatação

- **Nunca usar `[[wikilink]]` puro do Obsidian.** Ele não vira link clicável no GitHub. Usar sempre o formato markdown padrão: `[texto do link](caminho/do/arquivo.md)`.
- **Diagramas em Mermaid**, direto em bloco de código dentro do `.md`. Renderiza nativo no GitHub e no Obsidian, sem exportar imagem.
- **Sem travessão (—)** no texto corrido. Preferir ponto, vírgula ou parênteses.
- **Tom sempre informal e direto**, sem "corporativês", sem soar tutorial engessado. Mesma pegada do README e dos arquivos de `que-porra-e-essa/`.
- **Estrutura de cada módulo**: o que é → que problema resolve → o que existia antes e por que não era suficiente → trade-offs → exemplo prático (quando fizer sentido pro tópico).
