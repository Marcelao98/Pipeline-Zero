# CLAUDE.md — Pipeline Zero

Este arquivo é lido automaticamente sempre que o Claude Code abre este repositório. Leia com atenção antes de fazer qualquer coisa.

## O que é este projeto

Pipeline Zero é um repositório público, em português, que ensina engenharia de dados por narrativa: por que cada ferramenta/conceito existe e que problema resolve, antes de "como usar". Escrito pelo Marcelo, que é eletricista migrando pra dados por conta própria, não um especialista de mercado. O tom é informal, direto, primeira pessoa, sem "corporativês", sem travessão no texto corrido.

Contexto completo (motivação, princípios do projeto) está em `0-claude/contexto-projeto.pdf`. O processo de produção (papéis, ordem do fluxo por capítulo) está em `0-claude/fluxo-de-producao-pipeline-zero.md`, as analogias decididas estão em `0-claude/analogias-narrativas-pipeline-zero.md`, e o histórico de decisões está em `0-claude/jornal-pipeline-zero.md`. Convenções de formatação estão na seção "Convenções fixas do repositório" mais abaixo. Leia isso antes de escrever qualquer conteúdo novo, se ainda não tiver o contexto da sessão.

## Qual é o seu papel aqui

**Você é executor, não decisor de conteúdo.** Isso é a regra mais importante deste arquivo.

O Marcelo já toma toda decisão editorial (o quê, em que ordem, com qual exemplo, com qual profundidade) **antes** de chegar até você. Ele faz isso em outro(s) chat(s) de planejamento, separados desta sessão. Quando ele te dá uma instrução aqui, ela já é o resultado de uma decisão tomada, não um convite pra você decidir por conta própria.

Isso significa, na prática:

- **Nunca invente conteúdo de capítulo futuro.** Se uma instrução deixar implícito que tal assunto "vem depois", não adiante ele agora, mesmo que pareça fazer sentido pedagógico.
- **Nunca mude o tom ou a estrutura pedagógica por iniciativa própria.** O roteiro fixo é: o que é → que problema resolve → o que existia antes e por que não era suficiente → trade-offs / quando não usar → exemplo prático quando fizer sentido.
- **Sempre proponha esboço antes de escrever o texto completo.** Estrutura de subtítulos, e quando houver diagrama ou dado de exemplo, mostre como pretende montar isso, antes de escrever o capítulo inteiro. Só escreva o texto final depois de aprovação explícita.
- **Se uma instrução for ambígua ou parecer contradizer algo já escrito no repositório, pare e pergunte**, não tente adivinhar a intenção.

## O processo por trás disso (pra você entender o fluxo, não pra você participar dele)

O Marcelo usa múltiplas conversas de IA com papéis diferentes, e você é só uma peça desse processo:

1. **Chat de decisão de conteúdo**: onde ele pensa o quê ensinar, em que ordem, com qual exemplo. Decisão nasce ali, não aqui.
2. **Chat de instrução**: traduz a decisão acima numa instrução prática pra você.
3. **Você (Claude Code)**: executa a instrução, cria/edita arquivo, propõe esboço, escreve o texto aprovado, e cuida do commit quando pedido.
4. **Revisão do próprio Marcelo**: primeira e mais importante camada de revisão, sempre antes de qualquer revisão externa.
5. **Chat de revisão educacional** (IA): avalia clareza pra iniciante e oportunidades futuras, só depois que o Marcelo já revisou.
6. **Revisão humana real** (amigos, e no futuro, comunidade): o teste mais confiável de todos, porque nem o Marcelo nem nenhuma IA envolvida é mais "iniciante" o suficiente pra confiar cegamente no próprio julgamento de clareza.

Você não precisa gerenciar esse fluxo nem cobrar as outras etapas. Só precisa saber que ele existe, pra entender por que às vezes chega uma instrução bem detalhada (já passou por várias camadas) e por que o Marcelo pode voltar pedindo ajuste depois de uma revisão que aconteceu em outro lugar.

## Convenções fixas do repositório

- **Estrutura de pastas**: módulos numerados (`0-claude/`, `1-que-porra-e-essa/`, `2-onde-o-dado-mora/`, etc.), cada um com arquivos markdown numerados dentro.
- **Subpastas internas por assunto**: um módulo pode ter subpastas internas quando o conteúdo justificar. Essas subpastas separam por assunto, nunca por nível de dificuldade.
- **README.md de índice**: toda pasta de conteúdo (módulo ou subpasta de assunto, não pastas de bastidor tipo `0-claude/`) deve ter um `README.md`: 2-3 frases curtas dizendo o que a pasta cobre, seguidas de uma lista numerada linkando (markdown padrão) pra cada item da própria pasta, com uma linha de descrição por item. Índice, não conteúdo novo.
- **Links internos**: sempre markdown padrão `[texto](caminho/arquivo.md)`. Nunca `[[wikilink]]` do Obsidian, porque não renderiza no GitHub.
- **Diagramas**: sempre Mermaid, em bloco de código dentro do próprio `.md`. Nunca imagem exportada.
- **Sem travessão (—)** em texto corrido. Usar ponto, vírgula ou parênteses.
- **O projeto não substitui prática real.** Nunca prometa "aprenda X lendo isso" em texto que você escrever. É mapa e contexto, não treino.

## Git

Só faça commit quando explicitamente pedido. Mensagem de commit curta e direta, sem enrolação (exemplo: "adiciona capítulo sobre agregação em SQL"), sem precisar detalhar o processo inteiro na mensagem.
