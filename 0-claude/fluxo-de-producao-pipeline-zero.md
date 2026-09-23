# Fluxo de produção do Pipeline Zero

Documento de referência sobre como o conteúdo é produzido, revisado e publicado. Complementa `analogias-narrativas-pipeline-zero.md` (que registra decisões de conteúdo) — este aqui registra o processo em si.

## Papéis (personas)

| Persona | Função | Status |
|---|---|---|
| Este chat (Gerência) | Decide escopo e conteúdo de cada módulo, mantém a visão geral do projeto | ativo |
| **Catarina** | Um chat por módulo. Gente boa, sem trocadilho de "chato" porque não é ela quem implica com nada. Pega as decisões da Gerência e instrui a Claudia Coda sobre o que escrever | ativo, nome confirmado |
| **Claudia Coda** (Claude Code) | O "estagiário com superpoderes" — executa: escreve esboço, depois texto completo, nunca inventa conteúdo futuro nem muda tom/estrutura por conta própria. Qualquer coisa que não esteja explícita na instrução da Catarina, ela pergunta antes de fazer (ver regra abaixo) | ativo, apelido já em uso |
| **Dr Chatonildo** | Revisor de lógica e coerência: checa se o conteúdo faz sentido, se não tem erro factual, se não está "viajando na maionese" | ativo, apelido já em uso |
| **Mestre Enredo** (nome proposto) | Revisor de storytelling: checa se a analogia e a narrativa estão funcionando, se o gancho pega | nome pendente de confirmação |
| **Garimpo** | Antigo chat de curadoria de conteúdo externo (transcrição de vídeo, etc). Reaproveitado também como sandbox para testar analogias novas antes de elas irem pros módulos | ativo, função expandida |
| **Bardo** | Orienta a transformação de conteúdo já pronto em publicação (LinkedIn, etc), fora do fluxo de produção do conteúdo em si | ativo |
| Marcelo (autor) | Aprovação final, no fim de todo o fluxo. Além disso, é a quem a Claudia Coda recorre toda vez que tem dúvida sobre qualquer aspecto não coberto explicitamente — ver regra abaixo | ativo, papel explicitado |
| Beta reader externo | Validação com gente de fora do processo (ex: amigo que testou o módulo de SQL sem saber nada de SQL antes) | etapa separada, pós-fluxo interno, já em uso |

### Regra da Claudia Coda: perguntar antes de decidir

Tudo que não estiver explicitamente coberto pela instrução da Catarina ou por uma decisão já registrada nos documentos deste projeto, a Claudia Coda pergunta antes de agir — no formato "posso fazer isso, Marcelo?". Isso vale pra qualquer aspecto: testar uma analogia nova, redigir de um jeito diferente do combinado, mudar estrutura, o que for. Ela não preenche lacuna sozinha, mesmo que a lacuna pareça pequena.

## Ordem do fluxo por capítulo

1. Gerência decide escopo/conteúdo do capítulo (este chat)
2. Catarina traduz a decisão em instrução para a Claudia Coda
3. Claudia Coda produz esboço (perguntando ao Marcelo sempre que algo não estiver explícito) → aprovação do autor → texto completo
4. Dr Chatonildo revisa lógica e coerência
5. Mestre Enredo revisa storytelling e analogia
6. Autor aprova no fim, como gate final
7. Beta reader externo testa (quando aplicável)
8. Bardo transforma em material de divulgação, se for o caso

Analogias novas (ex: água/encanamento, caixa de ferramentas) passam pelo **Garimpo** como sandbox antes de entrarem oficialmente em qualquer módulo.

## Registro histórico (changelog)

Duas camadas, formatos diferentes:

- **Mudança de código/estrutura do repositório**: mensagem de commit git curta e direta (padrão já definido no `CLAUDE.md`), com uma linha de motivo no corpo do commit quando a mudança reflete uma decisão de conteúdo, não só ajuste técnico.
- **Decisão de storytelling/analogia**: log de decisões vivo, no mesmo formato de `analogias-narrativas-pipeline-zero.md` — não é o capítulo em si, é o porquê por trás dele.

## Pendências

- Confirmar o nome proposto para o revisor de storytelling (Mestre Enredo) ou substituir.
- Confirmar que o beta reader externo continua como etapa separada, fora do fluxo interno de personas de IA.
