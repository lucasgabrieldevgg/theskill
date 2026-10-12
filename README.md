# theskill

> **PT** — Um compilado de skills de polimento de software: UI, prosa, código e commits. Quatro sub-skills especializadas sob um único roteador — duas importadas dos repositórios oficiais, duas autorais.
>
> **EN** — A bundled skill collection for polishing software deliverables: UI, prose, code, and commits. Four specialized sub-skills under a single router — two imported from official upstream repos, two original.

---

## 🇧🇷 Português

### O que é

`theskill` é uma meta-skill: um roteador que dispara em qualquer intenção de polimento e encaminha para a sub-skill certa. Mantém o inventário de skills enxuto (uma entrada só) sem sacrificar cobertura.

### As quatro sub-skills

| Sub-skill | Origem | Para que serve |
| --- | --- | --- |
| **impeccable** | [`pbakaus/impeccable`](https://github.com/pbakaus/impeccable) v4.5.2 (Apache 2.0) — por Paul Bakaus | Polimento de interfaces front-end: sites, dashboards, componentes, design systems, tipografia, spacing, motion, acessibilidade, error states, empty states. Inclui 45 arquivos de referência e scripts de browser automation. |
| **stop-slop** | [`hardikpandya/stop-slop`](https://github.com/hardikpandya/stop-slop) — por Hardik Pandya | Remover padrões de escrita típicos de IA: filler phrases, structures formulaicas, voice distante, em-dashes, hedges. Para quando o texto precisa parecer humano. |
| **code-impeccable** | Original neste repo | Polimento de código sem mudar comportamento: nomes, dead code, estrutura, padrões idiomáticos, legibilidade. |
| **commit-craft** | Original neste repo | Comunicação no git: mensagens de commit convencionais, descrições de PR, release notes, changelogs. |

### Como usar

1. Instale a skill no seu ambiente ClawHub.
2. Peça coisas como "polish this landing page", "this README sounds like AI, fix it", "tighten up this function", "write a commit message for these changes".
3. A skill raiz encaminha automaticamente para a sub-skill certa.

### Estrutura

```
theskill/
├── SKILL.md                       # raiz roteadora
├── README.md                      # este arquivo (bilíngue)
├── .gitignore
├── skills/
│   ├── impeccable/                # upstream: pbakaus/impeccable v4.5.2
│   │   ├── SKILL.md
│   │   ├── LICENSE.upstream        # Apache 2.0
│   │   ├── reference/              # 45 arquivos: adapt, audit, bolder, etc.
│   │   └── scripts/                # impeccable CLI, font-index, live-browser
│   ├── stop-slop/                 # upstream: hardikpandya/stop-slop
│   │   ├── SKILL.md
│   │   ├── LICENSE.upstream
│   │   ├── CHANGELOG.upstream.md
│   │   └── references/             # examples.md, phrases.md, structures.md
│   ├── code-impeccable/SKILL.md   # original
│   └── commit-craft/SKILL.md      # original
├── evals/evals.json               # casos de teste
└── scripts/                       # helpers compartilhados (futuro)
```

### Atribuição e licenciamento

- **impeccable**: mantida sob Apache 2.0, conforme [`skills/impeccable/LICENSE.upstream`](skills/impeccable/LICENSE.upstream). Crédito integral a Paul Bakaus. Repositório original: <https://github.com/pbakaus/impeccable>.
- **stop-slop**: mantida sob sua licença original, conforme [`skills/stop-slop/LICENSE.upstream`](skills/stop-slop/LICENSE.upstream). Crédito integral a Hardik Pandya. Repositório original: <https://github.com/hardikpandya/stop-slop>.
- **code-impeccable** e **commit-craft**: originais deste repo, sob a licença geral do `theskill` (MIT).

---

## 🇺🇸 English

### What it is

`theskill` is a meta-skill: a router that triggers on any polish-quality intent and dispatches to the right sub-skill. Keeps the skills inventory lean (one entry) without sacrificing coverage.

### The four sub-skills

| Sub-skill | Origin | What it does |
| --- | --- | --- |
| **impeccable** | [`pbakaus/impeccable`](https://github.com/pbakaus/impeccable) v4.5.2 (Apache 2.0) — by Paul Bakaus | Frontend interface polish: websites, dashboards, components, design systems, typography, spacing, motion, accessibility, error states, empty states. Ships with 45 reference files and browser-automation scripts. |
| **stop-slop** | [`hardikpandya/stop-slop`](https://github.com/hardikpandya/stop-slop) — by Hardik Pandya | Remove AI writing patterns: filler phrases, formulaic structures, narrator-from-a-distance voice, em-dashes, hollow hedging. For when prose needs to sound human. |
| **code-impeccable** | Original to this repo | Code polish without behavior change: naming, dead code, structure, idiomatic patterns, readability. |
| **commit-craft** | Original to this repo | Git communications: conventional commit messages, PR descriptions, release notes, changelogs. |

### How to use

1. Install the skill in your ClawHub environment.
2. Ask things like "polish this landing page", "this README sounds like AI, fix it", "tighten up this function", "write a commit message for these changes".
3. The root skill routes automatically to the right sub-skill.

### Attribution & licensing

- **impeccable**: kept under Apache 2.0, see [`skills/impeccable/LICENSE.upstream`](skills/impeccable/LICENSE.upstream). Full credit to Paul Bakaus. Upstream repo: <https://github.com/pbakaus/impeccable>.
- **stop-slop**: kept under its original license, see [`skills/stop-slop/LICENSE.upstream`](skills/stop-slop/LICENSE.upstream). Full credit to Hardik Pandya. Upstream repo: <https://github.com/hardikpandya/stop-slop>.
- **code-impeccable** and **commit-craft**: original to this repo, under the repo's overall MIT license.

---

## License

MIT for original content (`theskill` root, `code-impeccable`, `commit-craft`). Sub-skills `impeccable` and `stop-slop` retain their upstream licenses — see each sub-skill's `LICENSE.upstream`.

## Contributing

PRs welcome. Each sub-skill is self-contained under `skills/<name>/`. To add a new sub-skill: drop a new folder, add a `SKILL.md`, and update the routing table in the root `SKILL.md`.

To update `impeccable` or `stop-slop` from upstream:

```bash
# from repo root
git clone --depth 1 https://github.com/pbakaus/impeccable.git /tmp/impeccable-upstream
rm -rf skills/impeccable && mkdir skills/impeccable
cp -r /tmp/impeccable-upstream/.agent/skills/impeccable/. skills/impeccable/
cp /tmp/impeccable-upstream/LICENSE skills/impeccable/LICENSE.upstream

git clone --depth 1 https://github.com/hardikpandya/stop-slop.git /tmp/stop-slop-upstream
rm -rf skills/stop-slop && mkdir skills/stop-slop
cp /tmp/stop-slop-upstream/SKILL.md skills/stop-slop/
cp -r /tmp/stop-slop-upstream/references skills/stop-slop/references
cp /tmp/stop-slop-upstream/LICENSE skills/stop-slop/LICENSE.upstream
cp /tmp/stop-slop-upstream/CHANGELOG.md skills/stop-slop/CHANGELOG.upstream.md
```
