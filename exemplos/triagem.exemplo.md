# Exemplo — triagem de três chamados

Três chamados típicos de uma software house, triados em sequência.
Nenhum deles gerou pasta. Cada um saiu em menos de cinco linhas.

O tom aqui é **seco de propósito**: modo didático não vale na triagem.
Ninguém quer aula para aprovar a correção de um rótulo.

---

## Chamado 1

> "o botão salvar está desalinhado no mobile na tela de pedido"

```
Triagem PD-2026-0031 — "Botao salvar desalinhado no mobile"
Gatilhos: nenhum
Veredito: fazer (correcao visual, escopo obvio, tela existente)
Destino: runx
Registrado no INDICE.md. Confirme com uma linha para seguir.
```

Nenhum gatilho: não é novo (G1), descreve o problema e não uma solução
(G2), vale para todos os clientes (G3), não é funcionalidade a procurar
(G4), é defeito visual e não regra de negócio (G5), a tela de pedido não
está nas zonas de risco (G6), nunca foi pedido antes (G7), e é meio dia
de trabalho (G8).

---

## Chamado 2

> "o cliente não consegue emitir a segunda via do boleto, dá erro"

```
Triagem PD-2026-0032 — "Erro ao emitir segunda via de boleto"
Gatilhos: nenhum
Veredito: fazer (erro tecnico em funcionalidade existente)
Destino: runx
Registrado no INDICE.md. Confirme com uma linha para seguir.
```

G5 não dispara: "dá erro" é falha técnica, não regra de negócio. Se o
chamado fosse "o sistema não deixa emitir segunda via depois do
vencimento", G5 dispararia — aquilo pode ser trava intencional.

---

## Chamado 3

> "como faço para cancelar um pedido já faturado?"

```
Triagem PD-2026-0033 — "Duvida: cancelar pedido faturado"
Gatilhos: nenhum
Veredito: ja_existe (duvida de uso, fluxo de devolucao)
Destino: atendimento — texto de resposta abaixo
Registrado no INDICE.md.
```

> Olá. Pedido já faturado não é cancelado: ele é devolvido, para manter o
> documento fiscal correto. O caminho é **Faturamento > Devolucoes**, onde
> você escolhe o pedido e marca devolução total ou parcial. O estoque volta
> automaticamente. Se o caso for outro, me diga que a gente vê junto.

Dúvida de uso é o veredito `ja_existe` mais barato que existe: não gera
trabalho e o cliente sai atendido no mesmo dia.

---

## Linhas geradas no INDICE.md

```
| 2026-03-04 | PD-2026-0031 | Botao salvar desalinhado no mobile | suporte | triagem | fazer | correcao visual sem gatilho | runx:OC-2026-0112 |
| 2026-03-04 | PD-2026-0032 | Erro ao emitir segunda via de boleto | suporte | triagem | fazer | erro tecnico em funcionalidade existente | runx:OC-2026-0113 |
| 2026-03-04 | PD-2026-0033 | Duvida: cancelar pedido faturado | cliente | triagem | ja_existe | fluxo e devolucao, nao cancelamento | - |
```

Três chamados, três linhas, zero pastas, zero arquivos. **É assim que a
maioria dos chamados de uma software house deve terminar.**
