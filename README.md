# theskill

> **PT** — Um compilado de skills de polimento de software: UI, prosa, código e commits. Uma única entrada, quatro sub-skills especializadas.
>
> **EN** — A bundled skill collection for polishing software deliverables: UI, prose, code, and commits. One entry point, four specialized sub-skills.

---

## 🇧🇷 Português

### O que é

`theskill` é uma meta-skill: um roteador que dispara em qualquer intenção de polimento e encaminha para a sub-skill certa. Mantém o inventário de skills enxuto (uma entrada só) sem sacrificar cobertura.

### As quatro sub-skills

| Sub-skill | Para que serve |
| --- | --- |
| **impeccable** | Polimento de interfaces front-end: sites, dashboards, componentes, design systems, tipografia, spacing, motion, acessibilidade, error states, empty states. |
| **stop-slop** | Remover padrões de escrita típicos de IA — "delve", "tapestry", travessões em demasia, hedge oco. Para quando o texto precisa parecer humano. |
| **code-impeccable** | Polimento de código sem mudar comportamento: nomes, dead code, estrutura, padrões idiomáticos, legibilidade. |
| **commit-craft** | Comunicação no git: mensagens de commit convencionais, descrições de PR, release notes, changelogs. |

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
│   ├── impeccable/SKILL.md
│   ├── stop-slop/SKILL.md
│   ├── code-impeccable/SKILL.md
│   └── commit-craft/SKILL.md
├── evals/evals.json               # casos de teste
└── scripts/                       # helpers compartilhados (futuro)
```

---

## 🇺🇸 English

### What it is

`theskill` is a meta-skill: a router that triggers on any polish-quality intent and dispatches to the right sub-skill. Keeps the skills inventory lean (one entry) without sacrificing coverage.

### The four sub-skills

| Sub-skill | What it does |
| --- | --- |
| **impeccable** | Frontend interface polish: websites, dashboards, components, design systems, typography, spacing, motion, accessibility, error states, empty states. |
| **stop-slop** | Remove AI writing patterns — "delve", "tapestry", em-dash overuse, hollow hedging. For when prose needs to sound human. |
| **code-impeccable** | Code polish without behavior change: naming, dead code, structure, idiomatic patterns, readability. |
| **commit-craft** | Git communications: conventional commit messages, PR descriptions, release notes, changelogs. |

### How to use

1. Install the skill in your ClawHub environment.
2. Ask things like "polish this landing page", "this README sounds like AI, fix it", "tighten up this function", "write a commit message for these changes".
3. The root skill routes automatically to the right sub-skill.

### Structure

(Same as above — see the tree in the Portuguese section.)

---

## License

MIT — use freely, attribution appreciated but not required.

## Contributing

PRs welcome. Each sub-skill is self-contained under `skills/<name>/`, so additions are easy: drop a new folder, add a `SKILL.md`, and update the routing table in the root `SKILL.md`.
