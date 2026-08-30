<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/bittencourtthulio/prodx/main/.github/assets/banner-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/bittencourtthulio/prodx/main/.github/assets/banner-light.svg">
  <img alt="prodx — a camada de produto do metodo Expx" src="https://raw.githubusercontent.com/bittencourtthulio/prodx/main/.github/assets/banner-light.svg" width="100%">
</picture>

<p>
  <img alt="harness: Claude Code" src="https://raw.githubusercontent.com/bittencourtthulio/prodx/main/.github/assets/badge-claude.svg">
  <img alt="harness: OpenCode" src="https://raw.githubusercontent.com/bittencourtthulio/prodx/main/.github/assets/badge-opencode.svg">
  <img alt="vereditos: 4, tres encerram" src="https://raw.githubusercontent.com/bittencourtthulio/prodx/main/.github/assets/badge-vereditos.svg">
  <img alt="assinatura: humana" src="https://raw.githubusercontent.com/bittencourtthulio/prodx/main/.github/assets/badge-assinatura.svg">
  <img alt="schema expx v1" src="https://raw.githubusercontent.com/bittencourtthulio/prodx/main/.github/assets/badge-schema.svg">
  <img alt="docs pt-BR" src="https://raw.githubusercontent.com/bittencourtthulio/prodx/main/.github/assets/badge-lang.svg">
  <img alt="licenca MIT" src="https://raw.githubusercontent.com/bittencourtthulio/prodx/main/.github/assets/badge-license.svg">
</p>

<p>
  <a href="https://bittencourtthulio.github.io/expxdev/#prodx"><strong>📘 Documentação do método</strong></a>
  &nbsp;·&nbsp;
  <a href="https://bittencourtthulio.github.io/expxdev/#prodx">Gatilhos e vereditos</a>
  &nbsp;·&nbsp;
  <a href="https://bittencourtthulio.github.io/expxdev/#ecossistema">O ecossistema</a>
  &nbsp;·&nbsp;
  <a href="https://bittencourtthulio.github.io/expxdev/#schema">Contratos</a>
</p>

<strong>A camada de produto do método Expx</strong> — decide se o pedido<br>
vira trabalho, para <a href="https://claude.com/claude-code">Claude Code</a> e <a href="https://opencode.ai">OpenCode</a>.

</div>

`prodx` fica entre o pedido do cliente e o planejamento técnico. Recebe um pedido cru — de cliente, de suporte, de dentro de casa — tria em segundos, verifica se o que foi pedido já existe, e emite um veredito com evidência. Ele responde a pergunta que nenhuma skill irmã faz: **vale fazer isso?**

> **Ele não assina.**
> O prodx recomenda com evidência, e com força. Quem assina é uma pessoa. Nenhum trabalho segue para a `sprintx` ou a `runx` sem o campo de assinatura preenchido, e a skill nunca preenche esse campo por conta própria.

---

## O ecossistema Expx

O método Expx é um conjunto de skills que se compõem, instaladas e mantidas pelo CLI [`expxdev`](https://github.com/bittencourtthulio/expxdev).

| Peça | Papel | Relação com a `prodx` |
|---|---|---|
| **[expxdev](https://github.com/bittencourtthulio/expxdev)** | o CLI: instala, atualiza e diagnostica o ecossistema, e sobe o painel de operação | é quem instala esta skill (`npx expxdev init`) |
| **[buildx](https://github.com/bittencourtthulio/buildx)** | orquestra um projeto inteiro, da descrição ao sistema pronto | invoca a `prodx` duas vezes: no B1 em modo greenfield (P0 e P3 pulados, veredito auto-assinado com `provisorio:true`) e no B6 como auditor do construído; é dependência obrigatória dele |
| **[sprintx](https://github.com/bittencourtthulio/sprintx)** | **Build** — feature nova, F1…F6 | recebe o `BRIEFING.md` assinado como entrada da F1; o plano referencia o `PD-ID` de origem |
| **[runx](https://github.com/bittencourtthulio/runx)** | **Run** — ocorrência em produção, E1…E5 | caminho mais comum: o `BRIEFING.md` vira o `00-OCORRENCIA.md`, já com o tipo classificado |
| **[legadox](https://github.com/bittencourtthulio/legadox)** | **camada** de segurança para código legado | as zonas de risco do `PERFIL.md` viram o gatilho G6 da triagem |
| **[stackx](https://github.com/bittencourtthulio/stackx)** | **camada** de convenções do repositório | fonte independente: convenção técnica não entra em veredito de produto |
| **[mergex](https://github.com/bittencourtthulio/mergex)** | entrega: branch, commit por task, PR e pacote de QA | a jusante: o `PD-ID` acompanha o trabalho até a descrição do PR |
| **[memox](https://github.com/bittencourtthulio/MemoX)** | **camada** de memória do projeto | indexa o `INDICE.md` e os vereditos; é ele que faz a verificação de existência melhorar com o tempo |
| **prodx** *(este repositório)* | **camada** de produto: decide **se** há trabalho | — |

**Camadas** (`prodx`, `memox`, `stackx`, `legadox`) sozinhas não fazem nada — elas modificam o comportamento da `sprintx` e da `runx`. Sem `docs/produto/` construído, nada muda: as irmãs se comportam como se comportariam sem esta skill.

A `prodx` é a única que roda **antes** de todas as outras: ela decide *se* existe trabalho; as demais tratam de *como* fazê-lo. A `buildx` é o caminho inverso: é a única peça que **depende** de outras — sem `prodx`, `sprintx` e `mergex` instaladas, ela não roda.

Detalhes do ecossistema inteiro no [README do expxdev](https://github.com/bittencourtthulio/expxdev).

---

## O problema do trabalho bem feito que não deveria existir

O ecossistema Expx já é bom em fazer trabalho direito. A `sprintx` planeja features com rigor, a `runx` trata ocorrências com disciplina, a `legadox` protege o código legado, a `mergex` entrega, a `memox` lembra.

Todos eles assumem que **o trabalho certo já foi escolhido**.

A sprintx planeja com rigor uma feature que não deveria existir. A runx corrige com disciplina um bug que era comportamento intencional. A legadox protege o código de uma mudança que ninguém pediu.

Numa software house esse é o desperdício mais caro que existe — mais caro que bug, porque bug pelo menos aparece. Trabalho desnecessário bem executado passa em todos os testes, entra em produção, e ninguém nunca descobre que não deveria ter sido feito.

O prodx é o portão que falta.

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/bittencourtthulio/prodx/main/assets/prodx-fluxo-dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/bittencourtthulio/prodx/main/assets/prodx-fluxo.svg">
  <img alt="Fluxo do prodx: o chamado entra pela esquerda e passa pela triagem. Sem gatilho disparado, segue pelo caminho curto direto ao veredito. Com gatilho, entra na avaliacao completa, que percorre entendimento do pedido, verificacao de existencia e avaliacao. Ambos os caminhos chegam aos quatro vereditos: ja existe, nao fazer e fazer outra coisa encerram o pedido; fazer segue adiante. Todo veredito passa pelo portao da assinatura humana, e so depois dele o briefing sai para o runx e para o sprintx." src="https://raw.githubusercontent.com/bittencourtthulio/prodx/main/assets/prodx-fluxo.svg" width="100%">
</picture>

## A realidade: o pedido vai do suporte direto ao dev

Nesta casa não existe papel de produto formalizado. O chamado chega no suporte e vai para o desenvolvedor, que normalmente tem outros na fila.

Isso governa todo o desenho da skill:

- **Quem roda o prodx é o próprio dev**, entre um chamado e outro. Um processo de cinco etapas por ticket não sobrevive a isso.
- **A skill é o processo que não existe**, não a ferramenta de um processo existente. Por isso ela roda em modo didático: está ensinando um método que ninguém no time pratica ainda.
- **Não há quem assine hoje.** A skill ajuda a estabelecer isso em vez de presumir que já está resolvido.

---

## A triagem, e por que a maioria dos chamados não deve passar por processo nenhum

A maioria dos chamados de uma software house é trivial: rótulo errado, campo desalinhado, dúvida de uso, erro óbvio.

Rodar avaliação de produto nisso é burocracia, e burocracia é contornada na segunda semana.

Por isso todo pedido começa pela **triagem**: oito gatilhos, resposta sim ou não, poucos segundos, **sem criar pasta nenhuma**. Nenhum gatilho disparou, o pedido sai com veredito imediato e uma linha no índice.

| # | Gatilho |
|---|---------|
| G1 | Pedido do tipo novo, ou pede tela, relatório ou fluxo novo |
| G2 | O pedido descreve uma solução, não um problema |
| G3 | O pedido serve a um cliente só, num produto multi-cliente |
| G4 | O pedido cheira a algo que já existe no sistema |
| G5 | Chegou rotulado como bug mas descreve regra de negócio |
| G6 | Toca zona de risco declarada no `PERFIL.md` da legadox |
| G7 | O mesmo pedido já foi recusado antes |
| G8 | O esforço aparente é maior que alguns dias |

A regra de proporcionalidade vale nos dois sentidos: **proibido** rodar avaliação completa em pedido trivial, e **proibido** pular a avaliação quando um gatilho disparou.

A triagem é a diferença entre uma ferramenta que o dev usa e uma que ele contorna.

## Os quatro vereditos — três deles encerram o pedido

| Veredito | O que acontece |
|----------|----------------|
| **`ja_existe`** | O sistema já faz. Sai um texto para o cliente explicando onde e como, na linguagem dele. **Encerra.** |
| **`nao_fazer`** | Com o motivo registrado, datado e falseável. Quando o pedido voltar, a avaliação já está feita. **Encerra.** |
| **`fazer_outra_coisa`** | O problema real reformulado, quase sempre menor e diferente do pedido. **Encerra o pedido original.** |
| `fazer` | E aí, e só aí, sai o briefing. |

Três dos quatro caminhos terminam sem gerar uma linha de código. Essa é a razão de o prodx existir.

O caso mais comum é o `ja_existe`: cliente pede "relatório de vendas por região" e o sistema tem isso há três anos numa tela que ninguém achou. A verificação de existência é a etapa mais valiosa e a mais ignorada.

## O indicador: a taxa de pedidos que não viram trabalho

**Se tudo que entra sai como "fazer", o prodx é burocracia** e será pulado na segunda semana.

O índice registra a proporção, e a skill a reporta quando perguntada sobre o estado:

```
Pedidos registrados: 48
Via triagem: 37 (77%)
Via avaliacao completa: 11 (23%)
Nao viraram trabalho: 19 (40%)
```

A última linha é o critério honesto de utilidade da skill. A segunda é o indicador de atrito: acima de 50% na avaliação completa, os gatilhos estão largos demais.

---

## Compatibilidade

`prodx` funciona em **Claude Code** e em **OpenCode**, a partir da mesma fonte. A skill fica **apenas** em `.claude/skills/` nos dois harnesses — o OpenCode lê `.claude/skills/*/SKILL.md` nativamente, e duplicar a árvore causaria colisão de nome. Só os comandos existem nas duas pastas, porque cada harness lê a sua:

| | Claude Code | OpenCode |
|---|---|---|
| Skill (projeto) | `.claude/skills/prodx/` | a mesma pasta, lida nativamente |
| Comandos (projeto) | `.claude/commands/` | `.opencode/commands/` |
| Skill (global) | `~/.claude/skills/prodx/` | a mesma pasta |
| Comandos (global) | `~/.claude/commands/` | `~/.config/opencode/command/` |

O `AGENTS.md` na raiz instrui o agente a acionar a skill nos pontos certos, em qualquer harness.

O prodx **não tem hook e não tem motor**: ele não executa nada, só lê o repositório e escreve markdown. Sem dependência externa, sem rede, sem runtime.

---

## Instalação

### Pelo CLI do método (recomendado)

O [`expxdev`](https://github.com/bittencourtthulio/expxdev) instala o prodx por completo — a skill, os seis comandos nas duas pastas e o `AGENTS.md`:

```bash
npx expxdev init --skills runx,prodx
```

O CLI trata o prodx como **camada**: sozinho ele não gera trabalho nenhum, então precisa vir acompanhado de `sprintx` ou `runx`. Ele avisa se você pedir só a camada, mas nunca impede.

Com `sprintx` ou `runx` na mesma seleção, o CLI sinaliza a integração disponível: é o `BRIEFING.md` assinado que entra como F1 da sprintx ou como `00-OCORRENCIA.md` da runx.

### Claude Code (manual)

```bash
cp -r .claude/skills/prodx        <projeto>/.claude/skills/
cp    .claude/commands/prodx*.md  <projeto>/.claude/commands/
cp    AGENTS.md                   <projeto>/
```

### OpenCode

```bash
cp -r .claude/skills/prodx          <projeto>/.claude/skills/
cp    .opencode/commands/prodx*.md  <projeto>/.opencode/commands/
cp    AGENTS.md                     <projeto>/
```

Não crie `.opencode/skills/`: nomes de skill precisam ser únicos entre todas as localizações.

### Verificação

Dentro do harness, `/prodx`. Sem `docs/produto/PRODUTO.md`, ele conduz à criação; com ele, mostra os pedidos abertos, o estágio de cada um e a proporção entre triagem e avaliação completa.

---

## Uso

### O jeito mais simples

Cole o chamado e deixe a skill triar:

```
/prodx-triar o cliente quer um botao de exportar para Excel na tela de pedidos
```

### Comandos

| Comando | Função |
|---------|--------|
| `/prodx` | Roteador: estado, pedidos abertos e indicadores |
| `/prodx-produto` | P1: cria ou atualiza o `PRODUTO.md` |
| `/prodx-triar` | P0: triagem de um chamado recém-chegado |
| `/prodx-avaliar` | P2 a P5: avaliação completa, do entendimento ao veredito |
| `/prodx-existe` | P3 isolada: consulta rápida — isso já existe? |
| `/prodx-briefing` | Gera o briefing de um veredito assinado |

### Os estágios

| Estágio | Nome | Saída | Quando roda |
|---|---|---|---|
| P0 | Triagem | linha no `INDICE.md` | todo pedido |
| P1 | Contexto de produto | `docs/produto/PRODUTO.md` | uma vez, atualizado sob demanda |
| P2 | Entendimento do pedido | `01-pedido.md` | avaliação completa |
| P3 | Verificação de existência | `02-existencia.md` | avaliação completa |
| P4 | Avaliação | `03-avaliacao.md` | quando não for EXISTE |
| P5 | Veredito e briefing | `VEREDITO.md`, `BRIEFING.md` | avaliação completa |

---

## O PRODUTO.md

Sem ele a skill vira genérica, e qualquer IA responderia igual. O `docs/produto/PRODUTO.md` é montado uma vez, atualizado sob demanda, e é o que faz o prodx conhecer **este** produto.

Duas seções fazem quase todo o trabalho:

- **O que o produto deliberadamente NÃO é.** É ela que sustenta a recusa de pedido fora de escopo. Vale mais que a descrição do que o produto é.
- **Quem decide.** O campo do signatário nunca fica vazio, nem como não determinado. Como não existe papel de produto na casa, a skill provoca a definição: pergunta quem, na prática, hoje diria não a um cliente, e registra essa pessoa como signatária provisória.

Ninguém assinando é o mesmo que o prodx não existir: os vereditos viram sugestão que ninguém encampa.

Nada de invenção: o que não for verificável vira `NAO DETERMINADO` e entra em `docs/produto/LACUNAS.md`.

---

## Integração com as outras skills

| Skill | Relação |
|-------|---------|
| **runx** | O caminho mais comum, porque hoje o pedido chega pelo suporte. O briefing vira o `00-OCORRENCIA.md`, com o tipo classificado e o comportamento intencional já verificado. Pedido aprovado na triagem entrega um briefing de uma linha. |
| **sprintx** | Recebe o briefing como entrada da F1. O plano referencia o `PD-ID` de origem. |
| **memox** | Indexa o índice e os vereditos. É ele que faz a verificação de existência melhorar com o tempo. |
| **legadox** | Quando existir `PERFIL.md`, as zonas de risco viram o gatilho G6. |

Os prompts de integração estão em [`docs/integracao/`](docs/integracao/). Nenhum deles altera comportamento quando o prodx não está instalado — o aviso de trabalho sem veredito assinado é aviso, nunca bloqueio.

**A ausência de qualquer skill irmã nunca bloqueia o prodx.**

---

## O que o prodx NÃO faz

- **Não assina.** Ele recomenda com evidência, e com força; quem assina é uma pessoa. Esta é a diferença mais importante em relação às skills irmãs: dizer "não" a um cliente tem consequência comercial, e cliente que ouve não e não deveria ter ouvido é cliente perdido.
- **Não planeja implementação.** Isso é sprintx e runx.
- **Não estima esforço.** Isso é a F3.5 da sprintx, e depende do plano.
- **Não fala com o cliente.** Ele produz o texto; quem envia é o atendimento.
- **Não substitui conversa.** Quando a informação não está em lugar nenhum, ele diz o que perguntar a quem, em vez de supor.

---

## Estrutura em disco

Tudo que o prodx produz no projeto:

```
docs/produto/
  PRODUTO.md
  LACUNAS.md
  INDICE.md                append-only, uma linha por pedido
  pedidos/
    <PD-ID>-<slug>/        criada apenas em avaliacao completa
      01-pedido.md
      02-existencia.md
      03-avaliacao.md
      VEREDITO.md
      BRIEFING.md          so quando o veredito for fazer
```

Pedido que passa na triagem não gera pasta. Pedido recusado **nunca é apagado**: a avaliação é ativo permanente e vale para a próxima vez.

Todos os arquivos usam o frontmatter **expx-schema v1**: chaves em `snake_case` sem acento, enums minúsculos sem acento, datas em ISO, chave nunca omitida.

---

## Estrutura do repositório

```
.claude/
  skills/prodx/
    SKILL.md                    identidade, estagios, as 12 regras invioláveis
    DECISOES-DA-SKILL.md        as decisões de desenho e as alternativas descartadas
    references/                 roteiro detalhado de cada estágio, P0 a P5
    references/integracao/      como o briefing chega na runx, na sprintx e na memox
    assets/TEMPLATE-*.md        formato de cada artefato produzido
  commands/prodx*.md            os seis comandos do Claude Code
.opencode/
  commands/prodx*.md            os mesmos seis, conteúdo idêntico, no formato do OpenCode
docs/integracao/                os patches para colar em cada skill irmã
exemplos/                       triagem, vereditos e briefing sobre um ERP de software house
assets/                         diagrama de fluxo do README
.github/assets/                 banner e badges do README
AGENTS.md                       instruções de acionamento para o agente
```

O `SKILL.md` é a porta de entrada e fica enxuto. O detalhe operacional mora no `reference` correspondente, lido **só quando a etapa chega** — mantendo o contexto pequeno.

---

## Exemplos

Em [`exemplos/`](exemplos/), todos sobre um ERP de software house:

- [`triagem.exemplo.md`](exemplos/triagem.exemplo.md) — três chamados passando direto, em poucas linhas, sem gerar pasta
- [`veredito-ja-existe.exemplo.md`](exemplos/veredito-ja-existe.exemplo.md) — relatório pedido que já existe numa tela pouco conhecida
- [`veredito-nao-fazer.exemplo.md`](exemplos/veredito-nao-fazer.exemplo.md) — pedido de cliente único num produto multi-cliente, recusado com motivo que continua válido
- [`briefing.exemplo.md`](exemplos/briefing.exemplo.md) — escopo mínimo bem menor que o pedido
- [`PRODUTO.exemplo.md`](exemplos/PRODUTO.exemplo.md) — o contexto de produto que sustenta os três anteriores

---

## Licença

MIT. Veja [LICENSE](LICENSE).

---

## Como contribuir

Abra uma issue descrevendo o caso concreto — o pedido, o veredito que saiu e o que deveria ter saído — antes de abrir um PR grande.

Contribuição mais útil, em ordem:

1. **Gatilho que faltou** — um pedido que passou direto na triagem e deveria ter ido para avaliação completa. Falso negativo de triagem é o defeito mais caro desta skill: ele deixa passar exatamente o trabalho que o prodx existe para barrar.
2. **Atrito observado** — um pedido trivial que a triagem mandou para avaliação completa. Gatilho largo demais treina o dev a pular a skill inteira.
3. **Existência não detectada** — uma funcionalidade que já existia e o P3 não achou, com o lugar onde ela estava.
