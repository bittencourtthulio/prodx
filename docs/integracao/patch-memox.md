# Patch — memox indexa o prodx

Prompt autônomo. Aplique no repositório onde a skill `memox` está
instalada. Trabalhe até o fim, sem perguntar nada.

═══════════════════════════════════════════════════════════════════════
PARTE 1 — CONTRATO
═══════════════════════════════════════════════════════════════════════

O memox é o índice do que já foi feito. O prodx produz dois ativos de
longo prazo que hoje não são indexados:

  docs/produto/INDICE.md   uma linha por pedido, com veredito e motivo
  os VEREDITO.md           a avaliação completa de cada pedido

Indexá-los faz a verificação de existência do prodx (P3) melhorar com o
tempo: quanto mais o memox sabe, menos o P3 depende de alguém lembrar
que uma funcionalidade existe.

REGRAS DO PATCH
  1. Nada muda quando o prodx não está instalado. Sem `docs/produto/`, o
     comportamento do memox é idêntico ao atual.
  2. O patch só acrescenta fontes de indexação. Não altera o que já é
     indexado nem o formato do índice existente.
  3. Vereditos `nao_fazer` são indexados como todos os outros — pedido
     recusado é ativo permanente, não lixo.
  4. Nenhum caminho absoluto.

═══════════════════════════════════════════════════════════════════════
PARTE 2 — O QUE ALTERAR
═══════════════════════════════════════════════════════════════════════

1. FONTES DE INDEXAÇÃO

   Acrescente duas fontes ao roteiro de indexação:

   a) `docs/produto/INDICE.md`
      Uma entrada por linha da tabela. Indexe por:
        termo do titulo · PD-ID · veredito · data · trabalho_gerado

   b) `docs/produto/pedidos/*/VEREDITO.md`
      Uma entrada por arquivo. Indexe por:
        termo do titulo · PD-ID · veredito · modulo afetado · data
      Do corpo, guarde a evidência principal e o campo "o que muda a
      recomendação" — são eles que respondem, no futuro, por que aquilo
      foi decidido e o que derrubaria a decisão.

2. CONSULTA POR VEREDITO

   Acrescente a capacidade de responder três perguntas:

     "isso ja foi pedido antes?"        busca por termo no INDICE.md
     "isso ja foi recusado?"            busca por termo + veredito nao_fazer
     "quantas vezes pediram isso?"      contagem de PD-IDs por termo

   A terceira alimenta o campo de recorrência do P4 do prodx.

3. O QUE NÃO INDEXAR

   Os arquivos intermediários `01-pedido.md`, `02-existencia.md` e
   `03-avaliacao.md` NÃO entram no índice: são insumo do veredito, e o
   veredito já carrega a conclusão. Indexá-los polui a busca com
   hipóteses que foram descartadas.

4. SKILL.md DO MEMOX

   Na tabela de fontes, acrescente as duas novas linhas. Uma linha cada,
   sem seção nova.

═══════════════════════════════════════════════════════════════════════
PARTE 3 — VERIFICAÇÃO E ENTREGA
═══════════════════════════════════════════════════════════════════════

VERIFICAÇÃO
  1. Sem `docs/produto/`: rode a indexação e confirme que o resultado é
     idêntico ao anterior.
  2. Com `INDICE.md` de dez linhas: confirme que as dez entram no índice.
  3. Com três `VEREDITO.md`, um deles `nao_fazer`: confirme que os três
     são indexados, inclusive o recusado.
  4. Busque um termo que só aparece num veredito e confirme que ele é
     encontrado.
  5. Confirme que `01-pedido.md`, `02-existencia.md` e `03-avaliacao.md`
     NÃO foram indexados.
  6. Grep por caminho absoluto no que foi alterado.

ENTREGA
  Os arquivos alterados com o diff de cada um; as duas fontes novas; as
  três consultas suportadas; e o resultado das seis verificações.
