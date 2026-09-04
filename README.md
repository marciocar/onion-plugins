# onion-plugins — Marketplace público do Sistema Onion 🧅

Instale o Onion (ou verticais) como **plugin do Claude Code** — capacidade read-only, atualizável
pelo gerenciador de plugins. **Não** é adoção/vendorização (esse é outro canal, `/meta:adopt`).

## Instalar

```
/plugin marketplace add marciocar/onion-plugins
/plugin install onion@onion-plugins
```

`onion` é o núcleo operacional (orquestrador + skills core + runtime + motores KG-SSOT + SDAAL +
doutrina) — é ele que traz a ENTRADA: `/onion:warm-up`, `/onion:catch-up`, `/onion:onion`. Verticais de
domínio (engineering, product, compliance, design, docs, testing) e o `onion-work-tools` são plugins
adicionais no mesmo marketplace.

**Instalado ≠ habilitado.** Se `/onion:warm-up` ou `/onion:catch-up` não aparecerem na sessão:
`claude plugin enable onion@onion-plugins` e reinicie o Claude Code (hooks só carregam em sessão nova).

**Atualizar:** `claude plugin marketplace update onion-plugins && claude plugin update onion@onion-plugins` —
a versão de cada plugin é derivada do conteúdo (anda quando o conteúdo anda).

## Atualizar

```
/plugin marketplace update onion-plugins
```

## O que NÃO vem aqui (por desenho — moat)

A meta-fábrica (gerar novos comandos/verticais/adotantes) e os grafos privados do core ficam no
repositório-fonte. Aqui está a **capacidade operacional**; o seu grafo de conhecimento é **seu**
(KG-SSOT-First: o plugin traz o motor, você constrói o SSOT).

---
🧅 Gerado do source por `materialize-marketplace-repo.sh` (Sistema Onion).
