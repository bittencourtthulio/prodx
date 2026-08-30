---
kind: veredito
schema: expx-schema-v1
pd_id: PD-2026-0034
titulo: Relatorio de vendas por regiao
data: 2026-03-05
veredito: ja_existe
via: avaliacao
gatilhos_disparados: [G1, G4]
aprovado_por: "Marcos Vieira"
aprovado_em: 2026-03-05
provisorio: true
trabalho_gerado: -
recorrencia: 2
---

# PD-2026-0034 — Veredito

## Recomendação

**JA EXISTE**

## Raciocínio

1. O cliente pediu um relatório de vendas separado por região, acreditando que o sistema não tem.
2. A tela `Vendas > Relatorios > Analise gerencial` tem agrupamento configurável, e região é uma das opções — o cadastro de clientes já traz o campo desde 2023.
3. Não é caso de construir nada: é caso de mostrar onde está, e registrar que a funcionalidade é difícil de achar.

## Evidência principal

Tela **Analise gerencial**, em `Vendas > Relatorios > Analise gerencial`,
rota `/vendas/relatorios/gerencial` definida em `routes/vendas.rb:44`. O
seletor de agrupamento é montado em `app/reports/sales_summary.rb:120` e
inclui `regiao`, alimentado pelo campo `clientes.regiao_id`.

Confirmado também em `OC-2025-0087`, cujo relatório de uso descreve: "o
usuário filtra por praça no topo da tela" — praça é como um dos clientes
chama região.

## O que muda a recomendação

Se o cliente quiser região definida por **agrupamento de municípios
próprio dele**, e não pelo campo de região do cadastro, aí é outro
pedido: o sistema hoje agrupa pela região cadastrada no cliente, uma por
cliente. Perguntar isso antes de fechar.

## Escopo mínimo aprovado

Não se aplica — veredito `ja_existe`.

## Assinatura

**Deve assinar:** Marcos Vieira (provisório)

| Campo | Valor |
|-------|-------|
| Aprovado por | Marcos Vieira |
| Aprovado em | 2026-03-05 |

## Comunicação

**Texto ao cliente:** escrito, abaixo
**Enviado por:** atendimento — o prodx não fala com o cliente

---

## Texto ao cliente

> Olá, Patrícia.
>
> Sobre o relatório de vendas separado por região: isso já está disponível
> no sistema.
>
> O caminho é: **Vendas > Relatorios > Analise gerencial**. Escolha o
> período que você quer e, no campo "Agrupar por", selecione **Região**. O
> resultado já sai somado por região, e tem o botão de exportar para
> planilha no canto superior direito.
>
> A região usada é a que está no cadastro de cada cliente, em
> **Cadastros > Clientes**. Vale conferir se os cadastros estão todos
> preenchidos, senão eles aparecem agrupados como "sem região".
>
> Se não for bem isso que você precisa, me diga o que ficou faltando que
> a gente avalia.

---

## Achado interno — não vai ao cliente

Segunda vez que este relatório é pedido (`PD-2025-0041` também terminou
em `ja_existe`). Dois pedidos iguais para a mesma tela em oito meses é
**problema de descoberta**, não de funcionalidade. Se aparecer um
terceiro, abrir pedido próprio para melhorar a navegação dos relatórios —
isso serve ao objetivo de diminuir chamados de suporte sobre relatórios.
