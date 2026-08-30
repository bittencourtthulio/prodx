# Patch — runx aceita briefing do prodx

Prompt autônomo. Aplique no repositório onde a skill `runx` está instalada.
Trabalhe até o fim, sem perguntar nada.

═══════════════════════════════════════════════════════════════════════
PARTE 1 — CONTRATO
═══════════════════════════════════════════════════════════════════════

O prodx é a camada de produto do ecossistema: ele decide SE há trabalho,
antes de o runx decidir COMO fazer. Quando um pedido é avaliado e
assinado, o prodx entrega um `BRIEFING.md`.

Este patch faz o E1 do runx aceitar esse briefing como entrada.

REGRAS DO PATCH
  1. Nada muda quando o prodx não está instalado. Ocorrência aberta sem
     briefing segue funcionando exatamente como hoje.
  2. O aviso de ocorrência sem veredito assinado é AVISO, não bloqueio.
     O runx nunca recusa trabalho por causa disso.
  3. O patch não altera E2 a E5.
  4. Nenhum caminho absoluto.

═══════════════════════════════════════════════════════════════════════
PARTE 2 — O QUE ALTERAR
═══════════════════════════════════════════════════════════════════════

1. REFERENCE DO E1 (`references/01-causa.md` ou equivalente)

   Acrescente uma seção "Entrada vinda do prodx", no início do roteiro:

   - Se existir `docs/produto/pedidos/<PD-ID>/BRIEFING.md` referente a
     esta ocorrência, use-o como base do `00-OCORRENCIA.md`.
   - Mapeamento de campos:
       problema                      → descricao da ocorrencia
       escopo minimo aprovado        → escopo da correcao
       o que esta fora               → fora de escopo
       criterios de aceite de negocio → criterios de aceite
       PD-ID                         → origem_prodx no frontmatter
   - Duas coisas vêm prontas do prodx e NÃO precisam ser refeitas no E1:
       o tipo já classificado como `correcao`
       o comportamento intencional já verificado (regra 7 do prodx)
     Registre no `00-OCORRENCIA.md` que essa verificação foi feita e por
     quem, citando o PD-ID.

   Acrescente também o caminho da triagem: pedido aprovado na triagem do
   prodx entrega um briefing de UMA LINHA no `docs/produto/INDICE.md`,
   não um arquivo. Esse formato também é entrada válida:

       <PD-ID> | correcao | <problema em uma linha> | aprovado por: <nome>, <data> | runx

2. FRONTMATTER DO `00-OCORRENCIA.md`

   Acrescente a chave `origem_prodx`, no padrão expx-schema v1:

       origem_prodx: <PD-AAAA-NNNN | ->

   Chave nunca omitida; `-` quando não houver origem no prodx.

3. AVISO DE OCORRÊNCIA SEM VEREDITO

   No início do E1, quando `docs/produto/` existir mas a ocorrência não
   tiver `origem_prodx`, emita UMA LINHA:

       Aviso: ocorrencia aberta sem veredito assinado do prodx. Seguindo.

   Quando `docs/produto/` não existir, não emita aviso nenhum.

4. SKILL.md DO RUNX

   Na tabela de integração, acrescente a linha do prodx: ele antecede o
   runx e decide se o pedido vira ocorrência. Uma linha, sem seção nova.

═══════════════════════════════════════════════════════════════════════
PARTE 3 — VERIFICAÇÃO E ENTREGA
═══════════════════════════════════════════════════════════════════════

VERIFICAÇÃO
  1. Sem `docs/produto/`: abra uma ocorrência do zero e confirme que o
     comportamento é idêntico ao anterior, sem aviso nenhum.
  2. Com `docs/produto/` e sem briefing: confirme o aviso de uma linha e
     que a ocorrência prossegue.
  3. Com `BRIEFING.md`: confirme que o `00-OCORRENCIA.md` sai preenchido,
     com `origem_prodx` e com a verificação de comportamento intencional
     registrada.
  4. Com briefing de uma linha vindo da triagem: confirme que é aceito.
  5. Grep por caminho absoluto no que foi alterado.

ENTREGA
  Os arquivos alterados com o diff de cada um; a nova seção do E1; a
  chave nova do frontmatter; e o resultado das cinco verificações.
