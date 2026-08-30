---
kind: veredito
schema: expx-schema-v1
pd_id: PD-2026-0037
titulo: Exportacao no layout proprio da Distribuidora Alfa
data: 2026-03-06
veredito: nao_fazer
via: avaliacao
gatilhos_disparados: [G1, G3]
aprovado_por: "Marcos Vieira"
aprovado_em: 2026-03-06
provisorio: true
trabalho_gerado: -
recorrencia: 1
---

# PD-2026-0037 — Veredito

## Recomendação

**NAO FAZER**

## Raciocínio

1. A Distribuidora Alfa pediu que o faturamento exporte um arquivo no layout do sistema contábil interno dela, com 42 colunas em ordem própria.
2. Num produto único multi-cliente, isso serve a 1 das 34 empresas, e o layout é definido por um sistema de terceiro que a própria Alfa pretende trocar em 2027.
3. O sistema já exporta no layout padrão do mercado, que o contador da Alfa consegue importar com um mapeamento de colunas feito uma vez.

## Evidência principal

Modelo de negócio `produto_unico_multi_cliente` declarado no `PRODUTO.md`
— mesma base para 34 empresas. A exportação existente está em
`Faturamento > Faturar > Exportar`, rota `/faturamento/exportacao` em
`routes/faturamento.rb:88`, no layout padrão do mercado.

Confirmado com a Alfa em 2026-03-05: o sistema contábil deles aceita
importação com mapeamento de colunas, e o contador já faz isso com outro
fornecedor.

## O que muda a recomendação

Três fatos, qualquer um deles, derrubam esta recusa:

- **Outros clientes pedirem o mesmo layout.** A premissa é "serve a um
  cliente só". Se três das 34 empresas pedirem, deixa de ser customização
  e vira produto configurável.
- **A Alfa aceitar pagar por customização** e a casa aceitar manter código
  específico dela. Foi oferecido e recusado por eles em 2026-03-06.
- **O layout virar padrão de mercado ou exigência fiscal.** Aí passa a ser
  restrição, não preferência.

Reavaliar se qualquer um aparecer. **A recusa é datada: vale enquanto os
três continuarem falsos.**

## Escopo mínimo aprovado

Não se aplica — veredito `nao_fazer`.

Registrado para memória: o escopo mínimo avaliado no P4 era um
mapeamento de colunas configurável por empresa, com custo estimado alto
por tocar a zona de risco de faturamento, para benefício de um cliente.
Foi ele que tornou a recusa clara.

## Assinatura

**Deve assinar:** Marcos Vieira (provisório)

| Campo | Valor |
|-------|-------|
| Aprovado por | Marcos Vieira |
| Aprovado em | 2026-03-06 |

## Comunicação

**Texto ao cliente:** escrito, abaixo
**Enviado por:** atendimento — o prodx não fala com o cliente

---

## Texto ao cliente

> Olá, Ricardo.
>
> Sobre a exportação no layout do sistema contábil de vocês: não vamos
> conseguir incluir esse formato específico no produto.
>
> O motivo é que o Gestor é um produto único, com a mesma versão para
> todas as empresas que usam, e um layout feito sob medida para um sistema
> de terceiro precisaria ser mantido só para vocês.
>
> O que dá para fazer hoje, e resolve na prática: a exportação padrão em
> **Faturamento > Faturar > Exportar** gera o arquivo no formato mais
> comum do mercado, e o seu contador consegue configurar a importação com
> um mapeamento de colunas — é uma configuração feita uma vez, e depois
> roda sozinha todo mês.
>
> Se o sistema contábil de vocês mudar em 2027 como comentaram, vale a
> gente conversar de novo: se o layout novo for um padrão de mercado, a
> situação é outra.

---

## Por que este arquivo não é apagado

Regra 9: pedido recusado nunca é apagado. Este veredito é **ativo
permanente**. Quando a Alfa pedir de novo — e clientes pedem de novo — a
avaliação já está feita, e a conversa começa de "o que mudou desde março"
em vez de começar do zero.

O P4 do próximo pedido igual vai contar a recorrência a partir daqui, e a
pergunta será: **o motivo ainda vale?** Se cinco empresas passarem a
pedir, a resposta é não, e a recusa cai por envelhecimento — não por
insistência.
