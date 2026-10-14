# Onion · Meta — plugin `onion-meta` do Sistema Onion 🧅

Meta-fábrica do Sistema Onion: cria comandos, agentes, skills, abstrações SDAAL e knowledge bases pelos templates do framework, audita o próprio framework (evolve, dissect) e absorve skills de terceiros com proveniência.

**Versão** `0.1.1` (derivada do conteúdo: anda quando o conteúdo anda) · **Licença** MIT · **Conformance** `bronze`

## Instalar

```
/plugin marketplace add marciocar/onion-plugins
/plugin install onion-meta@onion-plugins
```

Instalado ≠ habilitado: se os comandos não aparecerem, `/plugin enable onion-meta@onion-plugins` e reinicie o Claude Code (hooks só carregam em sessão nova).

```
# CLI, sem prompt
claude plugin marketplace add marciocar/onion-plugins && claude plugin install onion-meta@onion-plugins
```

## O que traz

| Componente | Quantidade |
|---|---|
| Comandos | 9 |
| Agentes | 3 |
| Skills | 0 |
| Hooks | 0 |

**Capacidades (Capability Contract):** provê `meta-factory`, `self-audit`, `skill-absorption`; requer `skill:onion-patterns`, `plugin:onion`.

## Comandos

Invocação: `/onion-meta:<comando>` (namespace do plugin).

| Comando | O que faz |
|---|---|
| `/onion-meta:absorb-skill` | Absorve uma skill de TERCEIRO na superfície Onion com segurança: importa → audita aderência (convenções de skill do core) → troca fontes/recursos externos por … |
| `/onion-meta:create-abstraction` | Geração de camada de abstração seguindo o padrão SDAAL. |
| `/onion-meta:create-agent-express` | Criar agente de forma rápida e simplificada. |
| `/onion-meta:create-agent` | Criação inteligente de agentes Claude Code com análise de contexto. |
| `/onion-meta:create-command` | Criação de novos comandos Claude Code com análise de contexto. |
| `/onion-meta:create-knowledge-base` | Gerar knowledge base estruturada em `docs/knowledge-base/<category>/`. |
| `/onion-meta:create-skill` | Orquestrador para criar, validar, otimizar e migrar Agent Skills via @agent-skills-specialist. |
| `/onion-meta:dissect` | Disseca uma ferramenta de terceiro em niveis selecionaveis (identidade, capacidade, mecanismo, transferibilidade, absorcao) e propoe absorver, costurar, parque… |
| `/onion-meta:evolve` | Auto-auditoria do Sistema Onion via orquestração (fan-out-and-synthesize) que produz um backlog priorizado, com evidência citada, de refatorações de modernizaç… |

## Agentes

| Agente | Especialidade |
|---|---|
| `@agent-creator-specialist` | Meta-especialista em criar agentes contextualizados e integrados ao ecossistema. |
| `@agent-skills-specialist` | Especialista em Agent Skills — formato aberto para estender capacidades de agentes IA. |
| `@command-creator-specialist` | Meta-especialista em criar Claude Code Commands (.md) contextualizados e integrados. |

## Requisitos

- Claude Code ≥ 2.1.239 (marketplace com `pluginRoot`); `bash`, `git`, `awk`; `python3` (motores KG e censos); `jq` opcional.
- Este plugin instala **capacidade** (read-only, atualizável pelo gerenciador). Não é adoção: para vendorizar o Onion num repo, o canal é `meta:adopt` (comando do core, não distribuído por plugin) no repositório-fonte.

## Proveniência

| Campo | Valor |
|---|---|
| Origem | `marciocar/onion-evolve` (repositório privado) |
| tree_sha (hash do conteúdo das fontes) | `2e7950d558ee` |

A origem identifica DE ONDE este artefato foi gerado; o canal público de instalação, issues e suporte é https://github.com/marciocar/onion-plugins. Ref e data do commit de origem estão em `.claude-plugin/provenance.json`.

Artefato GERADO por `assemble-plugin.sh` + `plugin-readme.sh` a partir da SSOT em `.claude/` do source. Não edite à mão: a próxima montagem sobrescreve.

## Comandos do core citados (não distribuídos neste plugin)

Estes comandos aparecem no texto sem a barra inicial porque pertencem ao core do Onion (meta-fábrica ou outra superfície) e **não** são instalados por este plugin: `meta:co-evolve`, `meta:co-relay`, `meta:forge`. Estão disponíveis num repo que adotou o Onion por vendorização (`.claude/` completo).

## Requer

Este plugin depende de: `onion` — instale antes (`/plugin install onion@onion-plugins`).

## Funciona melhor com

Comandos deste plugin citam: `onion-compliance`, `onion-engineering`, `onion-product`. Não é dependência — sem eles, essas menções apontam para comandos não instalados.

## Licença

MIT (texto integral em `LICENSE`, na raiz do plugin) — © Onion · Marcio Carvalho. Site: https://onionevolve.com · Issues e suporte: https://github.com/marciocar/onion-plugins
