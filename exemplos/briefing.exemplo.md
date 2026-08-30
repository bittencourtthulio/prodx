---
kind: briefing
schema: expx-schema-v1
pd_id: PD-2026-0032
data: 2026-03-05
destino: sprintx
classificacao: melhoria
veredito_origem: docs/produto/pedidos/PD-2026-0032-campo-observacao-tela-pedido/VEREDITO.md
aprovado_por: "Marcos Vieira"
aprovado_em: 2026-03-05
---

# PD-2026-0032 — Briefing

## O pedido original, para contexto

> "Coloca um campo de observação na tela de pedido."

**Não é isso que está sendo pedido ao sprintx.** O veredito foi
`fazer_outra_coisa`: a pergunta estruturante do P2 mostrou que, se o
motivo do desconto fosse registrado de outro jeito, o cliente ficaria
satisfeito. O campo de observação era a solução imaginada por ele, não o
requisito.

## O problema

O gerente aprova descontos acima do limite pela tela de aprovação, mas o
motivo da aprovação não fica registrado em lugar nenhum. Quando a
auditoria interna do cliente pergunta, três meses depois, por que aquele
desconto de 18% foi concedido, ninguém consegue responder — a informação
está no WhatsApp de quem aprovou, ou não está em lugar nenhum.

Isso acontece hoje em média 40 vezes por mês, e já gerou dois chamados
de suporte pedindo "extrair o histórico de aprovações", que não existe.

## Escopo mínimo aprovado

Um campo de **motivo** na tela de aprovação de desconto — obrigatório
apenas quando o desconto ultrapassa o limite —, escolhido de uma lista
curta de motivos pré-definidos pela empresa, com opção "outro" que abre
texto livre.

O motivo escolhido aparece no extrato do pedido, junto de quem aprovou e
quando.

**Por que este escopo e não o pedido:** o pedido original era um campo de
observação livre na tela de pedido, preenchido pelo vendedor em todos os
pedidos. O escopo aprovado registra apenas nas aprovações de desconto —
cerca de 40 por mês, contra os milhares de pedidos mensais — e usa lista
em vez de texto livre, o que torna a informação pesquisável. É a versão
bem menor que resolve a maior parte do problema.

## O que está explicitamente fora

- Campo de observação livre na tela de pedido, para todos os pedidos.
- Relatório ou tela de análise de motivos de desconto. Se a lista de
  motivos provar valor, isso vira pedido novo com dado real para embasar.
- Fluxo de aprovação em níveis, ou alçada por valor.
- Anexo de arquivo na aprovação.
- Configuração da lista de motivos por usuário — a lista é por empresa.

## Critérios de aceite do ponto de vista do negócio

- O gerente não consegue aprovar um desconto acima do limite sem informar
  o motivo.
- O motivo aparece no extrato do pedido, junto com quem aprovou e a data.
- Descontos dentro do limite continuam sendo aprovados como hoje, sem
  passo novo — o vendedor não ganha campo nenhum para preencher.
- O administrador da empresa consegue definir a lista de motivos.
- Ao consultar um pedido antigo com desconto aprovado antes desta
  mudança, o sistema não quebra: mostra o motivo em branco.

## Contexto para quem vai investigar

A aprovação de desconto acontece em `Vendas > Aprovações`. Citado apenas
como ponto de partida da investigação, **não como instrução de
implementação** — onde e como isso é construído é decisão do sprintx.

## Origem

**Veredito:** PD-2026-0032 · `docs/produto/pedidos/PD-2026-0032-campo-observacao-tela-pedido/VEREDITO.md`
**Assinado por:** Marcos Vieira, 2026-03-05

---

Regra 10: este briefing não contém decisão técnica. Arquitetura, camada,
tecnologia, modelo de dados e biblioteca são do sprintx. O prodx também
não estima esforço — isso é a F3.5.
