# theskill

> **PT** — Um compilado de skills de polimento de software: UI, prosa, código, testes, commits e PR reviews. Seis sub-skills especializadas sob um único roteador — três importadas dos repositórios oficiais, três autorais.
>
> **EN** — A bundled skill collection for polishing software deliverables: UI, prose, code, tests, commits, and PR reviews. Six specialized sub-skills under a single router — three imported from official upstream repos, three original.

---

## 🇧🇷 Português

### O que é

`theskill` é uma meta-skill: um roteador que dispara em qualquer intenção de polimento e encaminha para a sub-skill certa. Mantém o inventário de skills enxuto (uma entrada só) sem sacrificar cobertura.

### As seis sub-skills

| Sub-skill | Origem | Para que serve |
| --- | --- | --- |
| **impeccable** | [`pbakaus/impeccable`](https://github.com/pbakaus/impeccable) v4.5.2 (Apache 2.0) — por Paul Bakaus | Polimento de interfaces front-end: sites, dashboards, componentes, design systems, tipografia, spacing, motion, acessibilidade. Inclui 45 arquivos de referência e scripts de browser automation. |
| **stop-slop** | [`hardikpandya/stop-slop`](https://github.com/hardikpandya/stop-slop) — por Hardik Pandya | Remover padrões de escrita típicos de IA: filler phrases, structures formulaicas, voice distante, em-dashes, hedges. |
| **code-impeccable** | Original neste repo | Polimento de código sem mudar comportamento: nomes, dead code, estrutura, padrões idiomáticos, legibilidade. |
| **code-review** | [`awesome-skills/code-review-skill`](https://github.com/awesome-skills/code-review-skill) (MIT) — por awesome-skills | Review de PRs: arquitetura, performance, segurança, qualidade, bugs comuns. Referências específicas para React/Vue/Angular/Svelte/Rust/TS/Go/Python/Java/C#/Swift/Kotlin/Dart/Zig e mais. |
| **test-craft** | Original neste repo | Polimento de testes — unit, integration, e2e, property-based: nomes, assertions precisas, edge cases, fixtures, isolamento, anti-flakiness, pirâmide de testes. |
| **commit-craft** | Original neste repo | Comunicação no git: conventional commits, PR descriptions, release notes, changelogs. |

### Como usar

1. Instale a skill no seu ambiente ClawHub.
2. Peça coisas como "polish this landing page", "this README sounds like AI, fix it", "tighten up this function", "review my PR", "are these tests any good", "write a commit message for these changes".
3. A skill raiz encaminha automaticamente para a sub-skill certa.

### Estrutura

```
theskill/
├── SKILL.md                       # raiz roteadora
├── README.md                      # este arquivo (bilíngue)
├── .gitignore
├── skills/
│   ├── impeccable/                # upstream: pbakaus/impeccable v4.5.2 (Apache 2.0)
│   │   ├── SKILL.md
│   │   ├── LICENSE.upstream
│   │   ├── reference/             # 45 arquivos: adapt, audit, bolder, etc.
│   │   └── scripts/               # impeccable CLI, font-index, live-browser
│   ├── stop-slop/                 # upstream: hardikpandya/stop-slop
│   │   ├── SKILL.md
│   │   ├── LICENSE.upstream
│   │   ├── CHANGELOG.upstream.md
│   │   └── references/            # examples.md, phrases.md, structures.md
│   ├── code-review/               # upstream: awesome-skills/code-review-skill (MIT)
│   │   ├── SKILL.md
│   │   ├── LICENSE.upstream
│   │   ├── reference/             # 30+ arquivos por linguagem: react, vue, rust, etc.
│   │   ├── assets/                # pr-review-template.md, review-checklist.md
│   │   └── scripts/               # pr-analyzer.py
│   ├── code-impeccable/SKILL.md   # original
│   ├── test-craft/SKILL.md        # original
│   └── commit-craft/SKILL.md      # original
├── evals/evals.json               # 6 casos de teste
└── scripts/                       # helpers compartilhados (futuro)
```

### Atribuição e licenciamento

- **impeccable**: Apache 2.0, ver [`skills/impeccable/LICENSE.upstream`](skills/impeccable/LICENSE.upstream). Crédito a Paul Bakaus. Repo: <https://github.com/pbakaus/impeccable>.
- **stop-slop**: licença original, ver [`skills/stop-slop/LICENSE.upstream`](skills/stop-slop/LICENSE.upstream). Crédito a Hardik Pandya. Repo: <https://github.com/hardikpandya/stop-slop>.
- **code-review**: MIT, ver [`skills/code-review/LICENSE.upstream`](skills/code-review/LICENSE.upstream). Crédito a awesome-skills. Repo: <https://github.com/awesome-skills/code-review-skill>.
- **code-impeccable**, **test-craft**, **commit-craft**: originais deste repo, sob MIT.

---

## 🇺🇸 English

### What it is

`theskill` is a meta-skill: a router that triggers on any polish-quality intent and dispatches to the right sub-skill. Keeps the skills inventory lean (one entry) without sacrificing coverage.

### The six sub-skills

| Sub-skill | Origin | What it does |
| --- | --- | --- |
| **impeccable** | [`pbakaus/impeccable`](https://github.com/pbakaus/impeccable) v4.5.2 (Apache 2.0) — by Paul Bakaus | Frontend interface polish: websites, dashboards, components, design systems, typography, spacing, motion, accessibility, error states, empty states. Ships with 45 reference files and browser-automation scripts. |
| **stop-slop** | [`hardikpandya/stop-slop`](https://github.com/hardikpandya/stop-slop) — by Hardik Pandya | Remove AI writing patterns: filler phrases, formulaic structures, narrator-from-a-distance voice, em-dashes, hollow hedging. |
| **code-impeccable** | Original to this repo | Code polish without behavior change: naming, dead code, structure, idiomatic patterns, readability. |
| **code-review** | [`awesome-skills/code-review-skill`](https://github.com/awesome-skills/code-review-skill) (MIT) — by awesome-skills | PR reviews: architecture, performance, security, code quality, common bugs. Language-specific references for React/Vue/Angular/Svelte/Rust/TS/Go/Python/Java/C#/Swift/Kotlin/Dart/Zig and more. |
| **test-craft** | Original to this repo | Test suite polish — unit, integration, e2e, property-based: naming, precise assertions, edge cases, fixtures, isolation, anti-flakiness, test pyramid. |
| **commit-craft** | Original to this repo | Git communications: conventional commit messages, PR descriptions, release notes, changelogs. |

### How to use

1. Install the skill in your ClawHub environment.
2. Ask things like "polish this landing page", "this README sounds like AI, fix it", "tighten up this function", "review my PR", "are these tests any good", "write a commit message for these changes".
3. The root skill routes automatically to the right sub-skill.

### Attribution & licensing

- **impeccable**: Apache 2.0, see [`skills/impeccable/LICENSE.upstream`](skills/impeccable/LICENSE.upstream). Full credit to Paul Bakaus. Upstream: <https://github.com/pbakaus/impeccable>.
- **stop-slop**: original license, see [`skills/stop-slop/LICENSE.upstream`](skills/stop-slop/LICENSE.upstream). Full credit to Hardik Pandya. Upstream: <https://github.com/hardikpandya/stop-slop>.
- **code-review**: MIT, see [`skills/code-review/LICENSE.upstream`](skills/code-review/LICENSE.upstream). Full credit to awesome-skills. Upstream: <https://github.com/awesome-skills/code-review-skill>.
- **code-impeccable**, **test-craft**, **commit-craft**: original to this repo, MIT.

---

## License

MIT for original content (`theskill` root, `code-impeccable`, `test-craft`, `commit-craft`). Sub-skills `impeccable`, `stop-slop`, and `code-review` retain their upstream licenses — see each sub-skill's `LICENSE.upstream`.

## Contributing

PRs welcome. Each sub-skill is self-contained under `skills/<name>/`. To add a new sub-skill: drop a new folder, add a `SKILL.md`, and update the routing table in the root `SKILL.md`.

To update the imported sub-skills from upstream:

```bash
# impeccable
git clone --depth 1 https://github.com/pbakaus/impeccable.git /tmp/impeccable-upstream
rm -rf skills/impeccable && mkdir skills/impeccable
cp -r /tmp/impeccable-upstream/.agent/skills/impeccable/. skills/impeccable/
cp /tmp/impeccable-upstream/LICENSE skills/impeccable/LICENSE.upstream

# stop-slop
git clone --depth 1 https://github.com/hardikpandya/stop-slop.git /tmp/stop-slop-upstream
rm -rf skills/stop-slop && mkdir skills/stop-slop
cp /tmp/stop-slop-upstream/SKILL.md skills/stop-slop/
cp -r /tmp/stop-slop-upstream/references skills/stop-slop/references
cp /tmp/stop-slop-upstream/LICENSE skills/stop-slop/LICENSE.upstream
cp /tmp/stop-slop-upstream/CHANGELOG.md skills/stop-slop/CHANGELOG.upstream.md

# code-review
git clone --depth 1 https://github.com/awesome-skills/code-review-skill.git /tmp/code-review-upstream
rm -rf skills/code-review && mkdir skills/code-review
cp /tmp/code-review-upstream/SKILL.md skills/code-review/
cp -r /tmp/code-review-upstream/reference skills/code-review/reference
cp -r /tmp/code-review-upstream/assets skills/code-review/assets
cp -r /tmp/code-review-upstream/scripts skills/code-review/scripts
cp /tmp/code-review-upstream/LICENSE skills/code-review/LICENSE.upstream
```
