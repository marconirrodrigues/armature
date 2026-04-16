# Agent Engineering Framework v2.0 — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Evoluir o framework de v1.4.1 para v2.0 removendo a integração Multica, adicionando o modo MIGRATE com template dedicado, refinando a linguagem do P3 para agnóstico de provider/IDE, melhorando o SPEC.md e atualizando o guia HTML.

**Architecture:** Todas as mudanças são em arquivos de documentação (Markdown + HTML). Sem dependências de código. Mudanças independentes entre si, salvo Task 4 (MIGRATE no FRAMEWORK.md) que depende que §28–§30 já estejam na Constituição (Task 3). As demais tasks podem ser feitas em qualquer ordem.

**Tech Stack:** Markdown, HTML

---

## Mapa de Arquivos

| Arquivo | Operação | Tasks |
|---------|----------|-------|
| `scripts/sync-to-multica.sh` | Deletar | T1 |
| `scripts/MULTICA-SETUP.md` | Deletar | T1 |
| `agent-engineering-framework/FRAMEWORK.md` | Modificar | T2, T3, T4 |
| `agent-engineering-framework/templates/SPEC.md` | Modificar | T5 |
| `agent-engineering-framework/templates/MIGRATION.md` | Criar | T6 |
| `agent-engineering-framework/README.md` | Modificar | T7 |
| `agent-engineering-framework/guia-completo.html` | Modificar | T8 |

---

## Dependências entre Tasks

```
T1 (Remove Multica) ──────────────────────────────► T7 (README)
T2 (FRAMEWORK P3 + 1.5) ──────────────────────────► commit independente
T3 (FRAMEWORK §28-§30) ──────► T4 (FRAMEWORK MIGRATE) ► commit
T5 (SPEC.md) ──────────────────────────────────────► commit independente
T6 (MIGRATION.md) ─────────────────────────────────► commit independente
T8 (HTML) ──────────── depende de T1-T7 completos ──► último commit
```

---

### Task 1: Remover integração Multica

**Files:**
- Delete: `agent-engineering-framework/scripts/sync-to-multica.sh`
- Delete: `agent-engineering-framework/scripts/MULTICA-SETUP.md`
- Modify: `agent-engineering-framework/README.md` (remover referência a `scripts/`)

- [ ] **Step 1: Verificar o que existe antes de deletar**

```bash
ls agent-engineering-framework/scripts/
```
Expected output:
```
MULTICA-SETUP.md  sync-to-multica.sh
```

- [ ] **Step 2: Deletar os arquivos Multica**

```bash
rm agent-engineering-framework/scripts/sync-to-multica.sh
rm agent-engineering-framework/scripts/MULTICA-SETUP.md
rmdir agent-engineering-framework/scripts/
```

- [ ] **Step 3: Verificar remoção**

```bash
ls agent-engineering-framework/scripts/ 2>&1
```
Expected: `ls: cannot access 'agent-engineering-framework/scripts/': No such file or directory`

- [ ] **Step 4: Verificar referências ao Multica no README**

```bash
grep -n -i "multica\|scripts/" agent-engineering-framework/README.md
```
Expected: linhas que mencionam `scripts/` na seção Estrutura e possivelmente no changelog.

- [ ] **Step 5: Atualizar README.md — remover linha `scripts/` da Estrutura**

No arquivo `agent-engineering-framework/README.md`, localizar a seção `## Estrutura` e remover a linha:
```
├── scripts/              ← Integração Multica
```

- [ ] **Step 6: Confirmar que não há mais referências ao Multica no README**

```bash
grep -n -i "multica\|scripts/" agent-engineering-framework/README.md
```
Expected: sem output (zero matches)

- [ ] **Step 7: Commit**

```bash
git add -A
git commit -m "chore: remove Multica integration scripts and references"
```

---

### Task 2: Atualizar FRAMEWORK.md — P3 e critérios da Fase 1.5

**Files:**
- Modify: `agent-engineering-framework/FRAMEWORK.md` (linha 84 — P3; linhas 137–140 — Pesquisa proativa)

- [ ] **Step 1: Verificar estado atual do P3**

```bash
grep -n "P3" agent-engineering-framework/FRAMEWORK.md
```
Expected: linha com `P3 — Ecossistema: "Usa extensões no agente? (hooks, skills, MCP, memória) Quer recomendações?"`

- [ ] **Step 2: Verificar estado atual da seção Pesquisa proativa**

```bash
grep -n -A 3 "Pesquisa proativa" agent-engineering-framework/FRAMEWORK.md
```
Expected: `Pesquisar no GitHub ferramentas relevantes filtrando por: relevância à stack, stars/atividade recente, compatibilidade com agente.`

- [ ] **Step 3: Atualizar P3 — substituir linguagem Claude-específica por termos genéricos**

Localizar no `FRAMEWORK.md`:
```
**P3 — Ecossistema:** "Usa extensões no agente? (hooks, skills, MCP, memória) Quer recomendações?"
→ Inferir: integrações, oportunidades de ecossistema.
```

Substituir por:
```
**P3 — Ecossistema:** "Seu agente/IDE suporta extensões ou automações? (ex: plugins, automações, integrações externas, memória persistente) Quer recomendações?"
→ Inferir: ecossistema existente, oportunidades de integração, compatibilidade com ferramentas padrão.
```

- [ ] **Step 4: Atualizar seção "Pesquisa proativa" — tornar critérios de qualidade explícitos**

Localizar:
```
### Pesquisa proativa
Pesquisar no GitHub ferramentas relevantes filtrando por: relevância à stack, stars/atividade recente, compatibilidade com agente.

Categorias: hooks/automações, skills da stack, quality gates, agente revisor, automação workflow.
```

Substituir por:
```
### Pesquisa proativa
Pesquisar no GitHub ferramentas relevantes para o projeto. Incluir apenas ferramentas que atendam **todos** os critérios:
- ⭐ Stars relevantes para o nicho (contexto importa — 500 stars em lib especializada pode ser excelente)
- 📅 Commit recente (últimos 6 meses)
- 🐛 Ratio issues abertas/fechadas saudável (não abandonado)
- 📖 README e documentação claros
- 🔒 Sem vulnerabilidades conhecidas nas dependências

Categorias: automações/plugins p/ o agente usado, quality gates da stack, agente revisor, ferramentas de workflow.
```

- [ ] **Step 5: Verificar as mudanças**

```bash
grep -n -A 2 "P3" agent-engineering-framework/FRAMEWORK.md
grep -n -A 8 "Pesquisa proativa" agent-engineering-framework/FRAMEWORK.md
```
Expected: novo texto sem "hooks", "skills", "MCP" como termos primários; critérios de qualidade explícitos.

- [ ] **Step 6: Commit**

```bash
git add agent-engineering-framework/FRAMEWORK.md
git commit -m "refactor: update P3 to provider-agnostic language and explicit quality criteria"
```

---

### Task 3: Adicionar §28–§30 na Constituição do FRAMEWORK.md

**Files:**
- Modify: `agent-engineering-framework/FRAMEWORK.md` (seção CONSTITUIÇÃO, após §27)

- [ ] **Step 1: Verificar estado atual — onde termina a Constituição**

```bash
grep -n "§2[0-9]" agent-engineering-framework/FRAMEWORK.md
```
Expected: ver até §27 (`Após gerar artefatos → verificação de consistência...`)

- [ ] **Step 2: Localizar linha exata de §27 para inserção após ela**

```bash
grep -n "§27\|verificação de consistência" agent-engineering-framework/FRAMEWORK.md
```

- [ ] **Step 3: Adicionar §28–§30 na subseção "Comportamentos obrigatórios do agente"**

Localizar o bloco que termina com:
```
27. Após gerar artefatos → verificação de consistência: referências cruzadas, nomes, constraints enforced.
```

Adicionar imediatamente após:
```

### Migração
28. **Mapear antes de migrar.** Sistema não documentado = risco não mapeado. O legado deve ser entendido antes de qualquer decisão de arquitetura da migração.
29. **Rollback é pré-requisito.** Nenhuma migração começa sem plano de reversão validado. Migração sem rollback é aposta, não engenharia.
30. **Paridade verificada, não assumida.** Cada feature do sistema origem tem critério de aceite verificável no destino. Paridade nunca é inferida.
```

- [ ] **Step 4: Verificar inserção**

```bash
grep -n "§28\|§29\|§30\|Migração" agent-engineering-framework/FRAMEWORK.md
```
Expected: 4 matches — subseção "Migração" + §28, §29, §30

- [ ] **Step 5: Commit**

```bash
git add agent-engineering-framework/FRAMEWORK.md
git commit -m "feat: add migration principles §28-§30 to framework constitution"
```

---

### Task 4: Adicionar modo MIGRATE ao FRAMEWORK.md

**Files:**
- Modify: `agent-engineering-framework/FRAMEWORK.md` (tabela de modos + nova seção MIGRATE)

**Pré-requisito:** Task 3 concluída (§28–§30 na Constituição)

- [ ] **Step 1: Verificar tabela de modos atual**

```bash
grep -n -A 6 "MODO DE OPERAÇÃO" agent-engineering-framework/FRAMEWORK.md
```
Expected: tabela com Bootstrap, Retrofit, Evolve

- [ ] **Step 2: Atualizar tabela de modos — adicionar linha MIGRATE**

Localizar:
```
| EVOLVE | Já usa framework | Relê artefatos, atualiza |
```

Substituir por:
```
| EVOLVE | Já usa framework | Relê artefatos, atualiza |
| MIGRATE | Sistema existente precisa ser migrado | Analisa legado, define estratégia, gera estrutura + MIGRATION.md |
```

- [ ] **Step 3: Verificar atualização da tabela**

```bash
grep -n "MIGRATE" agent-engineering-framework/FRAMEWORK.md
```
Expected: pelo menos 1 match na tabela de modos

- [ ] **Step 4: Adicionar seção MIGRATE após a seção EVOLVE**

Localizar o bloco EVOLVE que termina com:
```
3. **Propor** — 📝 atualizar, ➕ adicionar, 🗑️ remover, 🔌 ferramentas. Confirmar.
```

Adicionar imediatamente após (antes do `---` que separa da próxima fase):

```

### MIGRATE
1. **Entender o legado** — Existe documentação? Testes? Dono técnico disponível? Qual o estado de saúde?
2. **Avaliar risco** — Zero-downtime obrigatório? Janela de manutenção? Impacto de interrupção?
3. **Discovery adaptado** — P1–P4 padrão + perguntas específicas de migração:

**M1 — Legado:** "O que existe hoje? Stack atual, estado da documentação, tem testes, tem dono técnico disponível para consulta?"
→ Inferir: complexidade do legado, riscos ocultos, profundidade do mapeamento necessário.

**M2 — Risco e continuidade:** "Zero-downtime é obrigatório? Há janela de manutenção disponível? Qual o impacto de uma interrupção?"
→ Inferir: estratégia de cutover, nível de cautela, necessidade de sistemas em paralelo.

**M3 — Estratégia:** "Prefere migrar tudo de uma vez (big bang), substituir gradualmente (strangler fig), ou quer uma recomendação baseada no contexto?"
→ Inferir: complexidade do plano, fases necessárias, cronograma.

**M4 — Dados (condicional — se há migração de dados):** "Qual o volume, criticidade, e consistência durante a migração é obrigatória?"

**Resumo MIGRATE inclui campos adicionais:**
```
Sistema origem: [stack/plataforma] | Estado: [documentado|parcial|legado]
Estratégia: [big bang|strangler fig|paralela|a definir]
Zero-downtime: [sim|não|janela: X]
Dados: [sim|não|volume: X]
```

4. **Artefato adicional obrigatório** — `MIGRATION.md` (template em `templates/MIGRATION.md`)
```

- [ ] **Step 5: Verificar seção MIGRATE completa**

```bash
grep -n "M1\|M2\|M3\|M4\|MIGRATION.md\|strangler" agent-engineering-framework/FRAMEWORK.md
```
Expected: matches para M1, M2, M3, M4 e referência ao MIGRATION.md

- [ ] **Step 6: Verificar que MIGRATION.md está na Fase 2 — Decisão de Artefatos**

```bash
grep -n "MIGRATION\|Condição\|Sempre\|Usa agente" agent-engineering-framework/FRAMEWORK.md | head -20
```
Se `MIGRATION.md` não aparecer na tabela de artefatos da Fase 2, adicionar a linha:
```
| Modo MIGRATE | MIGRATION.md |
```
na tabela de regras de inclusão da Fase 2.

- [ ] **Step 7: Commit**

```bash
git add agent-engineering-framework/FRAMEWORK.md
git commit -m "feat: add MIGRATE mode with M1-M4 discovery and MIGRATION.md artifact"
```

---

### Task 5: Atualizar template SPEC.md

**Files:**
- Modify: `agent-engineering-framework/templates/SPEC.md`

- [ ] **Step 1: Verificar estado atual do SPEC.md**

```bash
cat agent-engineering-framework/templates/SPEC.md
```
Expected: seções Visão Geral, Usuários e Personas, Requisitos Funcionais, Requisitos Não-Funcionais, Fora de Escopo, Critérios de Sucesso.

- [ ] **Step 2: Adicionar seções "Premissas" e "Questões Abertas" após "Fora de Escopo"**

Localizar:
```
## Fora de Escopo

- [O que NÃO faz nesta versão]

## Critérios de Sucesso
```

Substituir por:
```
## Fora de Escopo

- [O que NÃO faz nesta versão]

## Premissas

<!-- O que assumimos como verdade para esta spec. Se uma premissa cair, revisar a spec. -->

- [ex: "API de pagamentos estará disponível no ambiente de staging"]
- [ex: "Volume máximo de 10k usuários simultâneos na v1"]

## Questões Abertas

<!-- Decisões pendentes que afetam o escopo. Resolver antes de avançar. -->

| Questão | Impacto | Responsável | Prazo |
|---------|---------|-------------|-------|
| [questão] | [o que bloqueia] | [quem decide] | [data] |

## Critérios de Sucesso
```

- [ ] **Step 3: Verificar alteração**

```bash
grep -n "Premissas\|Questões Abertas" agent-engineering-framework/templates/SPEC.md
```
Expected: 2 matches com as novas seções

- [ ] **Step 4: Commit**

```bash
git add agent-engineering-framework/templates/SPEC.md
git commit -m "feat: add Premissas and Questões Abertas sections to SPEC.md template"
```

---

### Task 6: Criar template MIGRATION.md

**Files:**
- Create: `agent-engineering-framework/templates/MIGRATION.md`

- [ ] **Step 1: Verificar que o arquivo ainda não existe**

```bash
ls agent-engineering-framework/templates/MIGRATION.md 2>&1
```
Expected: `ls: cannot access '...': No such file or directory`

- [ ] **Step 2: Criar o arquivo MIGRATION.md**

Criar `agent-engineering-framework/templates/MIGRATION.md` com o conteúdo:

```markdown
# Migração — [Nome do Projeto]

<!-- Artefato obrigatório no modo MIGRATE. Mapeia origem → destino, define estratégia e garante rollback e paridade. §28, §29, §30 -->

## Sistema Origem

- **Stack atual:** [linguagem, framework, banco, infra]
- **Estado da documentação:** [completo | parcial | ausente | legado não documentado]
- **Cobertura de testes:** [% ou "sem testes"]
- **Módulos principais:** [liste os módulos/serviços existentes]
- **Dependências críticas:** [integrações externas, serviços que dependem deste sistema]
- **Dono técnico:** [quem conhece o sistema atual e pode ser consultado]

## Escopo da Migração

- **O que migra:** [o que será movido para o sistema destino]
- **O que permanece:** [o que continua no sistema origem após a migração]
- **O que é descartado:** [funcionalidades que não serão migradas e por quê]

## Estratégia

<!-- §28: mapear antes de migrar. Escolha baseada no contexto do projeto. -->

**Abordagem escolhida:** [Big bang | Strangler fig | Execução paralela | Migração faseada]

**Justificativa:** [por que esta abordagem dado o contexto: risco, prazo, zero-downtime, volume de dados]

**Alternativa descartada:** [X, porque Y]

## Mapeamento Origem → Destino

| Módulo/Componente (Origem) | Equivalente (Destino) | Observações |
|----------------------------|----------------------|-------------|
| [módulo] | [novo módulo] | [mudanças, simplificações, breaking changes] |
| [módulo] | [novo módulo] | |

### Mapeamento de Dados (preencher se há migração de dados)

| Tabela/Entidade (Origem) | Tabela/Entidade (Destino) | Transformações necessárias |
|--------------------------|--------------------------|---------------------------|
| [tabela] | [tabela] | [ex: normalização, renomeação, split] |

## Plano de Rollback

<!-- §29: rollback é pré-requisito. Este plano deve ser validado ANTES de iniciar a migração. -->

**Trigger para reversão:** [critério que ativa o rollback — ex: taxa de erro > X%, tempo de resposta > Xms, dado corrompido detectado]

**Passos do rollback:**
1. [passo concreto — ex: redirecionar tráfego de volta para sistema origem]
2. [passo concreto — ex: restaurar snapshot do banco de dados de [data]]
3. [passo concreto — ex: notificar stakeholders]

**Responsável:** [quem executa o rollback]
**Tempo estimado de reversão:** [ex: "< 15 minutos"]
**Janela para rollback:** [ex: "primeiras 48h após cutover"]

## Checklist de Paridade de Features

<!-- §30: paridade verificada, não assumida. Uma linha por feature do sistema origem. -->

| Feature | Critério de aceite no destino | Verificado? |
|---------|-------------------------------|-------------|
| [feature] | [como testar que equivalente funciona] | ⬜ |
| [feature] | [como testar] | ⬜ |

## Plano de Cutover

**Estratégia de cutover:** [big bang em janela | gradual por % de tráfego | por segmento de usuários]

**Go/No-go criteria:**
- [ ] [ex: todos os testes de paridade passando]
- [ ] [ex: performance do sistema destino validada em carga]
- [ ] [ex: plano de rollback testado em staging]
- [ ] [ex: stakeholders comunicados]

**Fase 1 — Pré-cutover:**
- [ação concreta, responsável, prazo]

**Fase 2 — Cutover:**
- [ação concreta, responsável, janela de tempo]

**Fase 3 — Pós-cutover (monitoramento):**
- [o que monitorar, por quanto tempo, critério de sucesso]

## Critérios de Sucesso

<!-- Mensuráveis. Comparar com baseline do sistema origem. -->

| Métrica | Baseline (Origem) | Meta (Destino) | Prazo |
|---------|-------------------|----------------|-------|
| [ex: tempo de resposta p95] | [valor atual] | [valor alvo] | [data] |
| [ex: taxa de erro] | [valor atual] | [valor alvo] | [data] |
| [ex: cobertura de testes] | [valor atual] | [valor alvo] | [data] |

**Definição de "migração concluída":** [critério objetivo e verificável]
```

- [ ] **Step 3: Verificar arquivo criado**

```bash
grep -n "Sistema Origem\|Rollback\|Paridade\|Cutover" agent-engineering-framework/templates/MIGRATION.md
```
Expected: 4 matches — uma para cada seção principal

- [ ] **Step 4: Commit**

```bash
git add agent-engineering-framework/templates/MIGRATION.md
git commit -m "feat: add MIGRATION.md template for MIGRATE mode"
```

---

### Task 7: Atualizar README.md para v2.0

**Files:**
- Modify: `agent-engineering-framework/README.md`

- [ ] **Step 1: Verificar estado atual do README**

```bash
cat agent-engineering-framework/README.md
```
Expected: versão v1.4.1, 3 modos (Bootstrap, Retrofit, Evolve), referência a `scripts/` na estrutura.

- [ ] **Step 2: Atualizar versão no título**

Localizar:
```
# Agent Engineering Framework
```
(e a linha do badge/versão abaixo)

Substituir `v1.4.1` por `v2.0` em todos os locais onde aparece no README.

- [ ] **Step 3: Atualizar tabela de modos — adicionar MIGRATE**

Localizar na seção Diferenciais ou Quick Start a menção a "3 modos":
```
- **3 modos** — Bootstrap, Retrofit, Evolve
```

Substituir por:
```
- **4 modos** — Bootstrap, Retrofit, Evolve, Migrate
```

- [ ] **Step 4: Atualizar seção Estrutura — remover scripts/**

Verificar se já foi removida na Task 1. Se não:

Localizar:
```
├── scripts/              ← Integração Multica
```
Remover essa linha.

- [ ] **Step 5: Adicionar MIGRATION.md na seção Estrutura**

Localizar a seção `## Estrutura` e adicionar `MIGRATION.md` na lista de templates:
```
│   ├── SPEC.md  PLAN.md  TASKS.md  AGENTS.md
│   ├── BOUNDARIES.md  LESSONS.md  PROGRESS.md
│   ├── ARCHITECTURE.md  GOLDEN-PRINCIPLES.md
│   ├── PATTERNS.md  AGENTS-ROSTER.md  TASK-ROUTING.md
│   └── README.md
```
Substituir por:
```
│   ├── SPEC.md  PLAN.md  TASKS.md  AGENTS.md
│   ├── BOUNDARIES.md  LESSONS.md  PROGRESS.md
│   ├── ARCHITECTURE.md  GOLDEN-PRINCIPLES.md
│   ├── PATTERNS.md  AGENTS-ROSTER.md  TASK-ROUTING.md
│   ├── MIGRATION.md
│   └── README.md
```

- [ ] **Step 6: Adicionar changelog v2.0**

Localizar a seção `## v1.4.1 — Changelog` e adicionar acima dela:

```markdown
## v2.0 — Changelog

- **Modo MIGRATE** — 4º modo de operação para migrações de sistemas (qualquer tipo: stack, banco, cloud, arquitetura). Discovery específico M1–M4, template MIGRATION.md dedicado.
- **Template MIGRATION.md** — Artefato exclusivo do modo MIGRATE: mapeamento origem→destino, estratégia, rollback, checklist de paridade, plano de cutover, critérios de sucesso.
- **Princípios §28–§30** — Constituição expandida com 3 princípios de migração: mapear antes de migrar, rollback como pré-requisito, paridade verificada.
- **P3 agnóstico** — Linguagem do Discovery P3 atualizada para termos genéricos (plugins, automações, integrações) — funciona com qualquer provider/IDE/modelo.
- **Critérios de qualidade explícitos** — Fase 1.5 "Pesquisa proativa" com 5 critérios objetivos para ferramentas recomendadas.
- **SPEC.md melhorado** — Novas seções Premissas e Questões Abertas.
- **Remoção do Multica** — Framework 100% agnóstico de ferramenta de gestão. Os artefatos gerados integram com qualquer ferramenta.

```

- [ ] **Step 7: Verificar consistência do README**

```bash
grep -n "Multica\|scripts/\|v1.4.1\|3 modos" agent-engineering-framework/README.md
```
Expected: zero matches (todas as referências antigas removidas)

- [ ] **Step 8: Commit**

```bash
git add agent-engineering-framework/README.md
git commit -m "docs: update README to v2.0 with MIGRATE mode and changelog"
```

---

### Task 8: Atualizar guia-completo.html para v2.0

**Files:**
- Modify: `agent-engineering-framework/guia-completo.html`

**Pré-requisito:** Tasks 1–7 concluídas (o guia deve refletir o estado final do framework)

- [ ] **Step 1: Atualizar versão no hero e footer**

Localizar:
```html
<div class="hero-eyebrow">Agent Engineering Framework — v1.0</div>
```
Substituir por:
```html
<div class="hero-eyebrow">Agent Engineering Framework — v2.0</div>
```

Localizar no footer:
```html
<p><strong>Agent Engineering Framework</strong> — v1.0 — Abril 2026</p>
```
Substituir por:
```html
<p><strong>Agent Engineering Framework</strong> — v2.0 — Abril 2026</p>
```

- [ ] **Step 2: Atualizar hero subtitle — mencionar 4 modos**

Localizar:
```html
<p class="hero-sub">Um framework progressivo em 3 camadas que unifica Spec-Driven Development, Harness Engineering e Orchestration Engineering em um sistema coerente.</p>
```
Substituir por:
```html
<p class="hero-sub">Um framework progressivo em 3 camadas e 4 modos de operação que unifica Spec-Driven Development, Harness Engineering e Orchestration Engineering em um sistema coerente — agnóstico a provider, modelo e IDE.</p>
```

- [ ] **Step 3: Adicionar MIGRATE à tabela "Quando ativar cada tier" (seção 02 — O Modelo)**

Localizar a tabela de cenários (seção `id="modelo"`):
```html
<tr><td>Legacy modernization</td><td style="color:var(--tier2)">Tier 1+2</td><td>Spec captura lógica perdida, harness enforce padrões novos</td></tr>
```
Adicionar linha após ela:
```html
<tr><td>Migração de sistema (stack, banco, cloud, arquitetura)</td><td style="color:var(--tier2)">Tier 1+2</td><td>Mode MIGRATE: mapeia legado, define estratégia, garante rollback e paridade</td></tr>
```

- [ ] **Step 4: Adicionar seção "Os 4 Modos de Operação" na seção de Implementação (seção 07)**

Localizar na seção `id="implementacao"` o `<h3>Como evoluir entre Tiers</h3>`. Adicionar antes dele:

```html
<h3>Os 4 modos de operação</h3>

<table>
  <tr><th>Modo</th><th>Quando usar</th><th>Artefato especial</th></tr>
  <tr><td><strong>Bootstrap</strong></td><td>Projeto novo, do zero</td><td>—</td></tr>
  <tr><td><strong>Retrofit</strong></td><td>Projeto existente que adota o framework</td><td>—</td></tr>
  <tr><td><strong>Evolve</strong></td><td>Projeto que já usa o framework e precisa iterar</td><td>—</td></tr>
  <tr><td><strong>Migrate</strong></td><td>Sistema existente precisa ser migrado (stack, banco, cloud, arquitetura)</td><td><code>MIGRATION.md</code></td></tr>
</table>

<div class="callout tip">
  <div class="callout-label">Modo Migrate</div>
  <p>O modo Migrate tem discovery específico (M1–M4) para mapear o legado, definir estratégia (big bang, strangler fig, execução paralela) e garantir que 3 princípios sejam respeitados: <strong>mapear antes de migrar</strong>, <strong>rollback como pré-requisito</strong> e <strong>paridade verificada</strong> — nunca assumida.</p>
</div>
```

- [ ] **Step 5: Atualizar file tree — adicionar MIGRATION.md (seção 06 — Estrutura de Arquivos)**

Localizar no file-tree:
```html
├── <span class="file t1">TASKS.md</span>             <span class="desc">← Tier 1: Tarefas ordenadas com critérios</span>
```

Adicionar linha após:
```html
├── <span class="file t1">MIGRATION.md</span>         <span class="desc">← Modo Migrate: mapeamento, estratégia, rollback, paridade, cutover</span>
```

- [ ] **Step 6: Adicionar anti-pattern de migração na tabela de Anti-Patterns (seção 09)**

Localizar na tabela de anti-patterns:
```html
<tr>
  <td><strong>Tudo no prompt, nada no repo</strong></td>
```
Adicionar antes dessa linha:
```html
<tr>
  <td><strong>Migrar sem mapear o legado</strong></td>
  <td>Sistema não documentado = risco não mapeado. Surpresas em produção durante cutover podem causar rollbacks não planejados.</td>
  <td>Mode MIGRATE: discovery M1 mapeia o legado antes de qualquer decisão técnica.</td>
</tr>
<tr>
  <td><strong>Migração sem plano de rollback</strong></td>
  <td>Sem reversão definida, qualquer problema vira incidente. A pressão para "continuar" cresce mesmo quando dever-se-ia parar.</td>
  <td>§29: rollback é pré-requisito, não opcional. Validar antes de iniciar a migração.</td>
</tr>
```

- [ ] **Step 7: Verificar versão atualizada em todos os locais**

```bash
grep -n "v1\.0\|v1\.4\|Multica" agent-engineering-framework/guia-completo.html
```
Expected: zero matches

- [ ] **Step 8: Verificar que MIGRATE aparece no HTML**

```bash
grep -n "MIGRATE\|Migrate\|migrate" agent-engineering-framework/guia-completo.html
```
Expected: pelo menos 5 matches (tabela de modos, callout, anti-patterns)

- [ ] **Step 9: Commit**

```bash
git add agent-engineering-framework/guia-completo.html
git commit -m "docs: update guia-completo.html to v2.0 with MIGRATE mode and new concepts"
```

---

### Task 9: Verificação de consistência final

**Files:** Todos os arquivos modificados (leitura apenas)

- [ ] **Step 1: Verificar zero referências ao Multica em todo o framework**

```bash
grep -rn -i "multica" agent-engineering-framework/
```
Expected: zero matches

- [ ] **Step 2: Verificar que MIGRATE aparece consistentemente em FRAMEWORK.md, README.md e HTML**

```bash
grep -rn "MIGRATE\|Migrate" agent-engineering-framework/FRAMEWORK.md agent-engineering-framework/README.md agent-engineering-framework/guia-completo.html
```
Expected: matches nos 3 arquivos

- [ ] **Step 3: Verificar que MIGRATION.md é referenciado no FRAMEWORK.md**

```bash
grep -n "MIGRATION.md" agent-engineering-framework/FRAMEWORK.md
```
Expected: pelo menos 1 match (na Fase 2 — Decisão de Artefatos e/ou na seção MIGRATE)

- [ ] **Step 4: Verificar que §28–§30 existem na Constituição**

```bash
grep -n "§28\|§29\|§30" agent-engineering-framework/FRAMEWORK.md
```
Expected: 3 matches

- [ ] **Step 5: Verificar que P3 não usa mais termos Claude-específicos como primários**

```bash
grep -n "P3" agent-engineering-framework/FRAMEWORK.md
```
Expected: texto com "plugins, automações, integrações" — sem "hooks, skills, MCP" como termos primários

- [ ] **Step 6: Verificar templates criados e modificados**

```bash
grep -n "Premissas\|Questões Abertas" agent-engineering-framework/templates/SPEC.md
grep -n "Rollback\|Paridade\|Cutover" agent-engineering-framework/templates/MIGRATION.md
```
Expected: matches nos dois arquivos

- [ ] **Step 7: Commit de fechamento (se houver ajustes finais)**

```bash
git add -A
git commit -m "chore: framework v2.0 consistency fixes"
```

---

## Resumo das Mudanças

| # | Arquivo | Tipo | Descrição |
|---|---------|------|-----------|
| T1 | `scripts/` | Delete | Remove integração Multica |
| T2 | `FRAMEWORK.md` | Modify | P3 agnóstico + critérios de qualidade Fase 1.5 |
| T3 | `FRAMEWORK.md` | Modify | Princípios §28–§30 na Constituição |
| T4 | `FRAMEWORK.md` | Modify | Modo MIGRATE completo (tabela + seção + M1–M4) |
| T5 | `templates/SPEC.md` | Modify | Premissas + Questões Abertas |
| T6 | `templates/MIGRATION.md` | Create | Template completo para modo MIGRATE |
| T7 | `README.md` | Modify | v2.0, changelog, MIGRATE nos diferenciais |
| T8 | `guia-completo.html` | Modify | v2.0, seção MIGRATE, anti-patterns, file tree |
| T9 | Todos | Verify | Consistência cruzada |
