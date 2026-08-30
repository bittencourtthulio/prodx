---
kind: produto
schema: expx-schema-v1
produto: Gestor ERP
criado_em: 2026-02-10
atualizado_em: 2026-03-02
modelo_negocio: produto_unico_multi_cliente
signatario: Marcos Vieira
signatario_provisorio: true
tem_perfil_legadox: true
lacunas_abertas: 3
---

# Produto — Gestor ERP

## 1. O que o produto é

ERP para distribuidoras e comércios atacadistas de médio porte. Cobre o
ciclo de venda: cadastro de clientes e produtos, pedido, faturamento,
contas a receber e estoque. Vendido como produto único, com a mesma base
de código para todos os clientes, parametrizada por empresa. Hoje atende
34 empresas. Quem paga é o dono ou o gestor administrativo; quem usa o
dia inteiro é o time de vendas e o faturista.

## 2. O que o produto deliberadamente NÃO é

- Não é sistema de folha de pagamento nem de ponto. Integra com o que o
  cliente já usa, via exportação.
- Não controla frota, entrega ou roteirização.
- Não é ferramenta de BI. Entrega relatórios operacionais e exportação;
  análise livre é no BI do cliente.
- Não faz emissão fiscal própria — integra com o emissor contratado.
- Não é CRM. Registra o cliente e o histórico de pedidos, não o funil.

## 3. Cliente que paga e usuário que usa

| | Quem | Observação |
|---|---|---|
| Paga | Dono ou gestor administrativo | Pede o que quer ver: relatório, indicador, controle |
| Usa | Vendedor, faturista, estoquista | Sofre com o que foi pedido: mais campos para preencher |

São pessoas diferentes, e isso explica boa parte dos pedidos ruins: o
gestor pede um campo novo, o vendedor é quem digita mil vezes por mês.

## 4. Perfis de usuário

| Perfil | O que faz no sistema |
|--------|---------------------|
| Vendedor | Lança pedido, consulta preço e estoque, acompanha seus clientes |
| Faturista | Fatura pedidos, emite documentos, trata devoluções |
| Estoquista | Entrada de mercadoria, inventário, ajustes |
| Gerente | Relatórios, aprovação de desconto, parâmetros da empresa |
| Administrador | Usuários, permissões, parâmetros globais |

## 5. Modelo de negócio

`produto_unico_multi_cliente`

Mesma base para 34 empresas, parametrizada. Consequência direta para os
vereditos: pedido que serve a um cliente só é **decisão de produto**, não
decisão técnica — vira customização paga, vira produto configurável, ou é
recusado. Nunca vai direto para o sprintx.

## 6. Objetivos de negócio vigentes

| Objetivo | Horizonte |
|----------|-----------|
| Reduzir o tempo de fechamento de pedido do vendedor | 2026 |
| Diminuir chamados de suporte sobre relatórios | 2026 |
| Reduzir exportação manual para planilha | primeiro semestre de 2026 |

## 7. Restrições que não se negociam

| Restrição | Natureza | Origem |
|-----------|----------|--------|
| Retenção fiscal de 5 anos dos documentos | regulatoria | legislação fiscal |
| Base única compartilhada entre as 34 empresas | tecnica | arquitetura multi-tenant |
| Janela de manutenção só fora do horário comercial | contratual | contrato de nível de serviço |

## 8. Quem decide

**Signatário:** Marcos Vieira — sócio e responsável pelo atendimento
**Provisório:** sim

Registrado como provisório porque a casa não tem papel de produto
formalizado. Foi apontado como quem, na prática, hoje diz não a um
cliente. Confirmar quando houver definição formal.

## 9. Zonas de risco

Do `PERFIL.md` do legadox.

| Zona | Por que é risco |
|------|-----------------|
| Cálculo de impostos no faturamento | Regra por estado, sem cobertura de teste |
| Fechamento de estoque | Rotina noturna, efeito em cascata |
| Tabela de preços e descontos | Compartilhada entre as 34 empresas |

## 10. Mapa de funcionalidades existentes

### Vendas

- **Pedido de venda** — lançamento, edição e cancelamento de pedido — `Vendas > Pedidos`
- **Aprovação de desconto** — desconto acima do limite vai para o gerente aprovar — `Vendas > Aprovações`
- **Consulta de preço e estoque** — consulta rápida durante o pedido — `Vendas > Consulta`
- **Análise gerencial de vendas** — totais por período, com agrupamento configurável por vendedor, filial ou linha de produto, e exportação — `Vendas > Relatorios > Analise gerencial`

### Faturamento

- **Faturamento de pedido** — gera documento e baixa estoque — `Faturamento > Faturar`
- **Devolução** — devolução total ou parcial — `Faturamento > Devolucoes`

### Estoque

- **Entrada de mercadoria** — `Estoque > Entradas`
- **Inventário** — contagem e ajuste — `Estoque > Inventario`

### Financeiro

- **Contas a receber** — títulos, baixa e renegociação — `Financeiro > Receber`
- **Extrato do cliente** — histórico de títulos por cliente — `Financeiro > Extrato`

### Cadastros

- **Clientes** — com campos de região, segmento e vendedor responsável — `Cadastros > Clientes`
- **Produtos** — com linha, marca e tabela de preço — `Cadastros > Produtos`
