# AGENTS.md

Repositório da skill **prodx** — a camada de produto do ecossistema Expx.

## O que é

O prodx fica entre o pedido do cliente e o planejamento técnico. Recebe um
pedido cru — de cliente, de suporte, de dentro de casa — e produz um
veredito com evidência; apenas quando o veredito for favorável, um
briefing pronto para o sprintx ou o runx.

Ele responde a pergunta que as skills irmãs não fazem: **vale fazer?**

## Estrutura deste repositório

```
.claude/skills/prodx/     a skill (SKILL.md, references, assets)
.claude/commands/         os seis comandos, para Claude Code
.opencode/commands/       os mesmos seis, conteudo identico, para OpenCode
assets/                   os SVGs do fluxo, claro e escuro
docs/integracao/          prompts de patch para runx, sprintx e memox
exemplos/                 exemplos completos sobre um ERP de software house
```

A skill vive **apenas** em `.claude/skills/`, que os dois harnesses leem
nativamente. Não crie `.opencode/skills/`: nomes de skill precisam ser
únicos entre todas as localizações.

## Ao trabalhar neste repositório

- **Comandos duplicados devem permanecer idênticos.** Ao alterar um
  arquivo em `.claude/commands/`, copie-o para `.opencode/commands/` e
  confirme com `diff -r` entre as duas pastas.
- **Sem caminho absoluto** em qualquer arquivo.
- **Sem prefixo `expx`** em nomes de arquivo, comando ou skill. O
  empacotamento como plugin com namespace pode vir depois; nada é
  prefixado agora.
- **Frontmatter no padrão expx-schema v1**: chaves em `snake_case` sem
  acento, enums minúsculos sem acento, datas em ISO, chave nunca omitida.
- **Os SVGs não levam `<script>`, `<foreignObject>`, animação, fonte
  externa nem `prefers-color-scheme`.** A troca de tema é feita no README,
  com dois arquivos e o elemento `<picture>`.
- **Ao alterar as regras invioláveis**, altere no `SKILL.md` (fonte da
  verdade), e verifique se os references, os templates e o README
  continuam coerentes.

## As 12 regras invioláveis

Estão no `SKILL.md`, uma por linha. As duas que mais restringem o
comportamento do agente:

1. **A skill não decide.** Ela recomenda com evidência; humano assina. O
   agente nunca preenche `aprovado_por` ou `aprovado_em` por conta
   própria.
2. **Nenhum trabalho segue para sprintx ou runx sem veredito assinado.**
   Gerar `BRIEFING.md` com `aprovado_por: PENDENTE` é bloqueio duro.

## Para usar a skill

Veja o `README.md`. Os comandos são `/prodx`, `/prodx-produto`,
`/prodx-triar`, `/prodx-avaliar`, `/prodx-existe` e `/prodx-briefing`.
