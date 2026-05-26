# FinStack Skills

> "The best quant strategies don't die in production because of bad math. They die because nobody stress-tested the assumptions, nobody audited the backtest, and nobody asked 'what kills this trade?'" — Every PM who lost money on a crowded factor.

Wall Street runs on review committees, risk sign-offs, and red teams. A strategy doesn't touch live capital until a research director evaluates the thesis, a backtest auditor checks for bias, a model-risk officer signs the governance review, a portfolio risk manager sizes the exposure, and a red team tries to kill it. That's five specialists, five meetings, five bottlenecks — and that's before the trade even goes on.

**FinStack Skills is that entire institutional review pipeline, automated.** A suite of AI specialists that interrogate your strategy the way a $10B fund's investment committee would — before you risk a single dollar.

---

## Inspiration

FinStack Skills is heavily inspired by [garrytan/gstack](https://github.com/garrytan/gstack), which turns Claude Code into a virtual engineering team (CEO, designer, eng manager, QA lead, release engineer). FinStack Skills does the same thing for **institutional finance** — turning your AI coding agent into a virtual investment committee.

*   `gstack` asks: _"Does this code ship?"_
*   `finstack-skills` asks: _"Does this strategy survive?"_

---

## Who This Is For
- **Quant researchers** — get institutional-grade review before your PM sees the backtest.
- **Portfolio managers** — systematic risk review on every new strategy or position change.
- **Risk teams** — automated SR 11-7 model governance without the 6-week manual review cycle.
- **Fund allocators** — red-team a third-party thesis before allocating capital.
- **Solo traders going institutional** — the review process you'd get at Citadel, without the headcount.

---

## Repository Structure

The skills are organized into a core cross-cutting review pipeline and three industry-specific verticals:

```
finstack-skills/
├── skills/
│   ├── core/                           # Cross-cutting institutional review pipeline
│   │   ├── quant-research-director/    # Economic thesis & validation design
│   │   ├── backtest-auditor/           # Forensic bias & leakage check
│   │   ├── model-risk-officer/         # SR 11-7 model risk governance
│   │   ├── portfolio-risk-manager/     # Sizing, drawdowns & tail risk (VaR/ES)
│   │   └── quant-red-team/             # Adversarial stress-testing & kill criteria
│   │
│   ├── hedge-funds/                    # Vertical: Signal speed, execution & alternative data
│   │   ├── alpha-decay-monitor/        # Half-life decay curves & AUM capacity
│   │   ├── execution-optimizer/        # TCM audits, spread crossing & borrow rates
│   │   └── alternative-data-auditor/   # Point-in-time integrity & MNPI legal compliance
│   │
│   ├── asset-managers/                 # Vertical: Purity, mandates & tracking error
│   │   ├── factor-decomposer/          # Fama-French systematic attribution & style drift
│   │   ├── benchmark-tracking-auditor/ # Active Share & UCITS 5/10/40 concentration limits
│   │   └── esg-mandate-reviewer/       # Carbon intensity (WACI) & exclusion checking
│   │
│   └── investment-banks/               # Vertical: Macro stress-testing & regulatory safety
│       ├── ccar-stress-tester/         # CCAR/DFAST macro stress shock replays
│       ├── counterparty-risk-officer/  # Peak Exposure, wrong-way risk & CVA adjustments
│       └── algorithmic-trader-validator/ # SEC Rule 15c3-5 checks & infinite loop throttles
│
├── docs/
│   ├── institutional-framework.md      # Detailed banking/asset management standards
│   └── skill-map.md                    # Full skill-to-role responsibility matrix
│
├── examples/
│   └── backtest-review.md              # In-depth multi-stage review walkthrough
│
└── README.md
```

---

## Quick Start

1. Clone `finstack-skills` into your AI agent's local skills directory (e.g. `~/.claude/skills/finstack-skills` or vendor it directly).
2. Invoke the **Core Review Pipeline** on any strategy description or research notebook:
   - Run `/quant-research-director` to review your economic thesis.
   - Run `/backtest-auditor` to audit your backtest for target leaks.
   - Run `/model-risk-officer` to check SR 11-7 model compliance.
   - Run `/portfolio-risk-manager` to size positions and calculate stressed Expected Shortfall.
   - Run `/quant-red-team` to attempt to kill the strategy before deployment.

3. Invoke **Vertical-Specific Specialties** as required:
   - *Hedge Funds:* Run `/alpha-decay-monitor` or `/execution-optimizer`.
   - *Asset Managers:* Run `/factor-decomposer` or `/benchmark-tracking-auditor`.
   - *Investment Banks:* Run `/ccar-stress-tester` or `/algorithmic-trader-validator`.

---

## The Core Review Pipeline

The core skills are designed to run as a sequential process, mirroring an institutional investment committee:

$$\text{Research Evaluation} \longrightarrow \text{Forensic Audit} \longrightarrow \text{Model Governance} \longrightarrow \text{Portfolio Sizing} \longrightarrow \text{Adversarial Stress}$$

Each specialist passes their output to the next. Nothing goes to live trading without running the gauntlet.

---

## Credits

Architecture inspired by Y Combinator CEO Garry Tan's [gstack](https://github.com/garrytan/gstack) — which proved that AI agents work best when they have **roles and processes, not just prompts.** `gstack` turned Claude Code into a virtual engineering team. `finstack-skills` turns your AI coder into a virtual investment committee.

---

## License

MIT