# Patch — sprintx aceita briefing do prodx

Prompt autônomo. Aplique no repositório onde a skill `sprintx` está
instalada. Trabalhe até o fim, sem perguntar nada.

═══════════════════════════════════════════════════════════════════════
PARTE 1 — CONTRATO
═══════════════════════════════════════════════════════════════════════

O prodx decide SE há trabalho; o sprintx decide COMO fazer. Quando um
pedido é avaliado e assinado como `fazer` ou `fazer_outra_coisa`, o prodx
entrega um `BRIEFING.md` que é a entrada natural da F1.

REGRAS DO PATCH
  1. Nada muda quando o prodx não está instalado. Feature planejada sem
     briefing segue funcionando exatamente como hoje.
  2. O aviso de feature sem veredito assinado é AVISO, não bloqueio.
  3. O patch não altera F2 a F6.
  4. A fronteira não se move: o briefing não traz decisão técnica nem
     estimativa. Arquitetura é da F3; esforço é da F3.5.
  5. Nenhum caminho absoluto.

═══════════════════════════════════════════════════════════════════════
PARTE 2 — O QUE ALTERAR
═══════════════════════════════════════════════════════════════════════

1. REFERENCE DA F1 (`references/01-base.md` ou equivalente)

   Acrescente uma seção "Entrada vinda do prodx", no início do roteiro:

   - Se existir `docs/produto/pedidos/<PD-ID>/BRIEFING.md`, use-o como
     entrada da ingestão.
   - Mapeamento de campos:
       problema                       → descricao da feature
       escopo minimo aprovado         → escopo
       o que esta fora                → nao-objetivos
       criterios de aceite de negocio → criterios de aceite
       PD-ID                          → origem_prodx no frontmatter
   - O que já vem decidido e NÃO se reabre na F2:
       o problema real, já separado da solução pedida
       o escopo mínimo, já aprovado e assinado
       o que está explicitamente fora
     Reabrir escopo já recusado no veredito é retrabalho: se a F2
     concluir que o escopo mínimo não resolve, isso volta ao prodx como
     novo pedido, não é decidido dentro do sprintx.

2. FRONTMATTER DO PLANO

   Acrescente a chave `origem_prodx`, no padrão expx-schema v1:

       origem_prodx: <PD-AAAA-NNNN | ->

   Chave nunca omitida; `-` quando não houver origem no prodx.

3. AVISO DE FEATURE SEM VEREDITO

   No início da F1, quando `docs/produto/` existir mas a feature não
   tiver `origem_prodx`, emita UMA LINHA:

       Aviso: feature planejada sem veredito assinado do prodx. Seguindo.

   Quando `docs/produto/` não existir, não emita aviso nenhum.

4. SKILL.md DO SPRINTX

   Na tabela de integração, acrescente a linha do prodx: ele antecede o
   sprintx e decide se o pedido vira feature. Uma linha, sem seção nova.

═══════════════════════════════════════════════════════════════════════
PARTE 3 — VERIFICAÇÃO E ENTREGA
═══════════════════════════════════════════════════════════════════════

VERIFICAÇÃO
  1. Sem `docs/produto/`: planeje uma feature do zero e confirme
     comportamento idêntico ao anterior, sem aviso.
  2. Com `docs/produto/` e sem briefing: confirme o aviso de uma linha e
     que o planejamento prossegue.
  3. Com `BRIEFING.md`: confirme que a F1 sai com escopo e não-objetivos
     preenchidos, e `origem_prodx` no frontmatter do plano.
  4. Confirme que o briefing não injetou decisão técnica no plano — a F3
     continua sendo quem decide arquitetura.
  5. Grep por caminho absoluto no que foi alterado.

ENTREGA
  Os arquivos alterados com o diff de cada um; a nova seção da F1; a
  chave nova do frontmatter; e o resultado das cinco verificações.
