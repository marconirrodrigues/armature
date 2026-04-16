# Design Spec — Agent Engineering Framework v2.0

**Data:** 2026-04-16
**Status:** Aprovado pelo usuário
**Escopo:** Evolução do framework v1.4.1 → v2.0

---

## Visão Geral

Evolução do Agent Engineering Framework com foco em quatro melhorias:
1. Remover integração Multica para tornar o framework completamente agnóstico de ferramentas de gestão
2. Adicionar modo MIGRATE (4º modo de operação) para cobrir migrações de sistemas
3. Refinar linguagem do P3 (Discovery) para terminologia agnóstica de provider/IDE
4. Melhorar templates SPEC.md e MIGRATION.md com seções de maior valor

O framework permanece agnóstico a providers, modelos e IDEs — mas continua recomendando as melhores ferramentas para cada projeto via Fase 1.5.

---

## Requisitos Funcionais

- **RF-01:** Remover diretório `scripts/` (sync-to-multica.sh + MULTICA-SETUP.md) e todas as referências ao Multica no README.md
- **RF-02:** Adicionar modo MIGRATE na tabela de modos do FRAMEWORK.md com descrição, trigger e ação
- **RF-03:** Adicionar seção MIGRATE nas fases do FRAMEWORK.md com discovery específico (M1–M4) e adaptações de fase
- **RF-04:** Adicionar 3 novos princípios na Constituição (§28, §29, §30) relativos a migração
- **RF-05:** Atualizar P3 do Discovery — substituir termos Claude-específicos (hooks, skills, MCP) por termos genéricos (automações, extensões, integrações)
- **RF-06:** Reforçar critérios de qualidade na seção "Pesquisa proativa" da Fase 1.5 (o que significa "bem avaliado" no GitHub)
- **RF-07:** Adicionar seções "Premissas" e "Questões Abertas" no template SPEC.md
- **RF-08:** Criar template `templates/MIGRATION.md` com estrutura completa para projetos de migração
- **RF-09:** Atualizar `guia-completo.html` com os novos conceitos, modo MIGRATE e demais mudanças
- **RF-10:** Atualizar README.md refletindo v2.0, removendo referência a scripts/Multica, adicionando MIGRATE nos diferenciais

---

## Fora de Escopo

- Alterações nos templates existentes além de SPEC.md (PLAN, TASKS, AGENTS, BOUNDARIES, LESSONS, PROGRESS, ARCHITECTURE, GOLDEN-PRINCIPLES, PATTERNS, AGENTS-ROSTER, TASK-ROUTING, README de template)
- Mudanças nas Fases 2, 3 e 4 do FRAMEWORK.md além das referências ao novo modo
- Criação de novos modos além do MIGRATE
- Mudanças nas recomendações de ferramentas padrão (RTK, Caveman, MemPalace)

---

## Design Detalhado

### 1. Remoção do Multica

**O que remover:**
- `scripts/sync-to-multica.sh`
- `scripts/MULTICA-SETUP.md`
- Diretório `scripts/` (se ficar vazio)
- Referência a `scripts/` no README.md (seção Estrutura)
- Changelog v1.4.1 no README não precisa mencionar Multica

**Princípio mantido:** O framework gera artefatos (TASKS.md, AGENTS.md, patterns/) que qualquer ferramenta de gestão pode consumir — mas a integração é responsabilidade da ferramenta, não do framework.

---

### 2. Modo MIGRATE

**Trigger:** Projeto existente que precisa ser movido para nova stack, arquitetura, plataforma, banco de dados, ou estrutura — com o sistema atual ainda em operação.

**Entrada na tabela de modos:**

| Modo | Quando | Ação |
|------|--------|------|
| MIGRATE | Sistema existente precisa ser migrado | Analisa legado, define estratégia, gera estrutura + MIGRATION.md |

**Discovery específico do MIGRATE (após P1–P4 padrão):**

- **M1 — Legado:** "O que existe hoje? Stack atual, estado da documentação, tem testes, tem dono técnico disponível para consulta?"
  → Inferir: complexidade do legado, riscos ocultos, profundidade do mapeamento necessário.

- **M2 — Risco e continuidade:** "Zero-downtime é obrigatório? Há janela de manutenção disponível? Qual o impacto de uma interrupção?"
  → Inferir: estratégia de cutover, nível de cautela, necessidade de sistemas em paralelo.

- **M3 — Estratégia:** "Prefere migrar tudo de uma vez (big bang), substituir gradualmente (strangler fig), ou quer uma recomendação baseada no contexto?"
  → Inferir: complexidade do plano, fases necessárias, cronograma.

- **M4 — Dados (condicional):** "Há dados a migrar? Qual o volume, criticidade, e consistência durante a migração é obrigatória?"

**Resumo do Discovery para MIGRATE inclui campos adicionais:**
```
Sistema origem: [stack/plataforma] | Estado: [documentado|parcial|legado]
Estratégia: [big bang|strangler fig|paralela|a definir]
Zero-downtime: [sim|não|janela: X]
Dados: [sim|não|volume: X]
```

**Artefatos adicionais:** MIGRATION.md (obrigatório no modo MIGRATE)

---

### 3. Novos Princípios da Constituição (§28–§30)

**§28 — Mapear antes de migrar.** Sistema não documentado = risco não mapeado. O legado deve ser entendido antes de qualquer decisão de arquitetura da migração.

**§29 — Rollback é pré-requisito.** Nenhuma migração começa sem plano de reversão validado. Migração sem rollback é aposta, não engenharia.

**§30 — Paridade verificada, não assumida.** Cada feature do sistema origem deve ter critério de aceite verificável no sistema destino. Paridade nunca é inferida.

---

### 4. Atualização do P3

**Antes:**
```
P3 — Ecossistema: "Usa extensões no agente? (hooks, skills, MCP, memória) Quer recomendações?"
→ Inferir: integrações, oportunidades de ecossistema.
```

**Depois:**
```
P3 — Ecossistema: "Seu agente/IDE suporta extensões ou automações? (ex: plugins, automações, integrações externas, memória persistente) Quer recomendações?"
→ Inferir: ecossistema existente, oportunidades de integração, compatibilidade com ferramentas padrão.
```

---

### 5. Reforço dos Critérios de Qualidade na Fase 1.5

**Seção "Pesquisa proativa" — critérios "bem avaliado" tornam-se explícitos:**

Critérios de qualidade para incluir na recomendação:
- ⭐ Stars relevantes para o nicho (não absoluto — uma lib de nicho com 500 stars pode ser excelente)
- 📅 Atualização recente (commit nos últimos 6 meses)
- 🐛 Ratio issues abertas/fechadas saudável
- 📖 README e documentação claros
- 🔒 Sem dependências com vulnerabilidades conhecidas

---

### 6. Melhorias no SPEC.md

Adicionar duas seções após "Fora de Escopo":

**Premissas**
```markdown
## Premissas

<!-- O que assumimos como verdade para esta spec. Se uma premissa cair, revisar a spec. -->

- [ex: "API de pagamentos estará disponível no ambiente de staging"]
- [ex: "Volume máximo de 10k usuários simultâneos na v1"]
```

**Questões Abertas**
```markdown
## Questões Abertas

<!-- Decisões pendentes que afetam o escopo. Resolver antes de avançar. -->

| Questão | Impacto | Responsável | Prazo |
|---------|---------|-------------|-------|
| [questão] | [o que bloqueia] | [quem decide] | [data] |
```

---

### 7. Template MIGRATION.md

Novo arquivo `templates/MIGRATION.md` com as seguintes seções:

1. **Sistema Origem** — stack, estado da documentação, módulos principais, dependências críticas
2. **Escopo da Migração** — o que migra, o que fica, o que é descartado
3. **Estratégia** — abordagem escolhida (big bang / strangler fig / paralela) com justificativa
4. **Mapeamento Origem → Destino** — módulos, dados, integrações
5. **Plano de Dados** (condicional) — estratégia de migração de dados, validação de integridade
6. **Plano de Rollback** — triggers para reversão, passos, responsável, tempo estimado
7. **Checklist de Paridade** — features do sistema origem com critério de aceite verificável no destino
8. **Plano de Cutover** — fases, janela, go/no-go criteria, comunicação
9. **Critérios de Sucesso** — mensuráveis, com baseline do sistema origem para comparação

---

### 8. Atualização do guia-completo.html

Atualizar o HTML para refletir:
- Versão v2.0
- 4 modos de operação (incluindo MIGRATE)
- Remoção de referências ao Multica
- Novos princípios §28–§30
- P3 com linguagem agnóstica
- Template MIGRATION.md
- Changelog v2.0

---

## Critérios de Sucesso

1. `scripts/` removido, zero referências ao Multica em qualquer arquivo
2. FRAMEWORK.md contém modo MIGRATE com discovery M1–M4 e princípios §28–§30
3. P3 usa linguagem agnóstica (sem hooks/skills/MCP como termos primários)
4. `templates/MIGRATION.md` criado e referenciado na Fase 2 (Decisão de Artefatos)
5. `templates/SPEC.md` contém seções Premissas e Questões Abertas
6. `guia-completo.html` atualizado e consistente com v2.0
7. README.md atualizado com v2.0 e estrutura correta
8. Consistência cruzada: FRAMEWORK.md, README.md e templates sem contradições
