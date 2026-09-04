# 🧅 onion-plugins — o Sistema Onion como plugins do Claude Code

O **Onion** é um framework operacional para desenvolvimento com IA: workflows faseados e retomáveis (produto → engenharia → compliance), um grafo de conhecimento como fonte de verdade em runtime (KG-SSOT), guardas determinísticas por hook e abstrações de provider (SDAAL). Este marketplace entrega essa **capacidade** como plugins instaláveis e atualizáveis pelo gerenciador de plugins — sem vendorizar nada no seu repositório.

Fonte: https://github.com/marciocar/onion-evolve · Site: https://onionevolve.com · Licença: MIT

## Quick start

```
/plugin marketplace add marciocar/onion-plugins
/plugin install onion@onion-plugins
```

Reinicie o Claude Code depois de instalar (hooks só carregam em sessão nova). Comece por `/onion:warm-up` (contexto do projeto) ou `/onion:catch-up` (onde você parou); `/onion:onion` orienta o que fazer a seguir.

```
# equivalente por CLI, sem prompts
claude plugin marketplace add marciocar/onion-plugins && claude plugin install onion@onion-plugins --yes
```

**Instalado ≠ habilitado.** Se os comandos `/onion:*` não aparecerem: `/plugin enable onion@onion-plugins` e reinicie.

## Plugins

| Plugin | Categoria | Versão | Comandos | Agentes | Skills | Hooks | O que traz |
|---|---|---|---|---|---|---|---|
| [`onion`](plugins/onion/README.md) | core | `0.1.164` | 4 | 1 | 5 | 2 | Nucleo operacional do Sistema Onion: o orquestrador mestre (skill onion) + skills core (language-standards, p… |
| [`onion-compliance`](plugins/onion-compliance/README.md) | vertical | `0.1.19` | 1 | 5 | 1 | 0 | Vertical de compliance do Onion: documentacao de conformidade como spec-as-code (ISO 27001/22301, SOC2, PMBOK… |
| [`onion-design`](plugins/onion-design/README.md) | vertical | `0.1.22` | 3 | 3 | 0 | 0 | Vertical de design do Onion: identidade visual como spec-as-code (tokens W3C/DTCG), gate WCAG e materializaca… |
| [`onion-docs`](plugins/onion-docs/README.md) | vertical | `0.1.23` | 10 | 5 | 0 | 0 | Vertical de documentacao do Onion: contexto de negocio/tecnico como spec-as-code, C4 (Context/Container/Compo… |
| [`onion-engineering`](plugins/onion-engineering/README.md) | vertical | `0.1.86` | 17 | 16 | 1 | 0 | Vertical de engenharia do Onion: fluxo faseado plan→start→work→pre-pr→pr→pr-update (GitFlow + sessoes persist… |
| [`onion-product`](plugins/onion-product/README.md) | vertical | `0.1.43` | 21 | 12 | 1 | 0 | Vertical de produto do Onion: descoberta a backlog (collect→refine→spec→feature), decomposicao de tasks agnos… |
| [`onion-testing`](plugins/onion-testing/README.md) | vertical | `0.1.18` | 4 | 3 | 0 | 0 | Vertical de testes/QA do Onion: geracao e execucao de testes (unit/integration/e2e) com deteccao de framework… |
| [`onion-work-tools`](plugins/onion-work-tools/README.md) | tools | `0.1.146` | 16 | 1 | 4 | 0 | Ferramentas de trabalho cross-cutting do Onion (nao meta-fabrica): knowledge-graph (kg + radar soberano), dia… |

Instale só o que precisa: `onion` é o núcleo (obrigatório: orquestrador, motores KG, guardas, runtime); cada vertical acrescenta comandos e agentes de um domínio; `onion-work-tools` traz os utilitários de trabalho (censo, backlog, freshness). Cada plugin tem o seu README com o catálogo completo.

```
/plugin install onion-engineering@onion-plugins
/plugin install onion-product@onion-plugins
```

## Manter em dia

| Ação | Slash | CLI |
|---|---|---|
| Atualizar o marketplace | `/plugin marketplace update onion-plugins` | `claude plugin marketplace update onion-plugins` |
| Atualizar um plugin | `/plugin update onion@onion-plugins` | `claude plugin update onion@onion-plugins` |
| Habilitar / desabilitar | `/plugin enable onion@onion-plugins` · `/plugin disable onion@onion-plugins` | `claude plugin enable …` · `claude plugin disable …` |
| Remover | `/plugin uninstall onion@onion-plugins` | `claude plugin uninstall onion@onion-plugins` |
| Listar | `/plugin list` · `/plugin marketplace list` | `claude plugin list --json` |
| Validar (dev) | `/plugin validate ./plugins/onion` | `claude plugin validate ./plugins/onion --strict` |

**Política de versão.** A versão de cada plugin é **derivada do conteúdo** (`0.1.<N>`, N = commits que tocaram as fontes canônicas): ela anda exatamente quando o conteúdo anda, e o `plugin update` — que compara versões, não conteúdo — enxerga a mudança. A entrada do marketplace não repete a versão: o `plugin.json` é a autoridade (recomendação oficial).

## Requisitos

- Claude Code ≥ 2.1.239 (marketplace com `pluginRoot`).
- `bash`, `git`, `awk`; `python3` para os motores de grafo e censos; `jq` opcional.
- Os hooks são scripts locais e determinísticos; podem vetar uma ação com `exit 2` (é a capacidade que só o Claude Code oferece). Nenhum envia dados para fora.

## O que este canal é — e o que não é

- **É** instalação de capacidade: read-only, versionada, atualizável, removível. Os seus grafos de conhecimento são **seus** (o plugin traz o motor; você constrói o SSOT).
- **Não é** adoção/vendorização: para ter o Onion dentro do repositório (customizável, com co-evolução), o canal é `/meta:adopt` no repositório-fonte.
- **Não vem** a meta-fábrica (gerar novos comandos/verticais/adotantes) nem os grafos privados do core — por desenho (moat).

## Estrutura de cada plugin

```
plugins/<nome>/
├── .claude-plugin/
│   ├── plugin.json        # manifesto (name, version derivada, description, keywords, license)
│   ├── capability.json    # Capability Contract: provides / requires / loads
│   └── provenance.json    # repository + ref + tree_sha do conteúdo (content-addressed)
├── commands/  agents/  skills/  hooks/   # o que o plugin expõe (namespace /<nome>:<comando>)
├── kb/  utils/  validation/              # doutrina e motores embarcados (quando aplicável)
└── README.md                             # catálogo gerado do próprio plugin
```

## Contribuir e reportar

Issues e sinais em https://github.com/marciocar/onion-evolve (o source). Os plugins aqui são **artefatos gerados** do source por `materialize-marketplace-repo.sh` — PRs de conteúdo vão para o source, não para este repositório.

## Licença

MIT — © Onion · Marcio Carvalho.

---
🧅 Gerado do source por `materialize-marketplace-repo.sh` + `marketplace-readme.sh` (Sistema Onion). Não edite à mão: a próxima materialização sobrescreve.
