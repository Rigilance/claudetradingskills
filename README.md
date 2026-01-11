# Claude Skills Library

> **Production-grade skills for Claude** | Zero cost, works offline, full MCP integration

**150+ specialized skills** for Claude Code, Claude Desktop, and terminal workflows. Battle-tested patterns, sharp-edge warnings, automated validations, and cross-skill collaboration.

## Why This Skills Library?

Most AI prompts are just text files. This library provides **production-grade knowledge systems** with 4 specialized YAML files per skill:

```
trading/technical-analysis/
├── skill.yaml           # Identity, patterns, anti-patterns, handoffs
├── sharp-edges.yaml     # Gotchas with detection patterns
├── validations.yaml     # Automated quality checks
└── collaboration.yaml   # How skills work together
```

### What Makes These Skills Different

| Feature | Regular Prompts | This Library |
|---------|----------------|--------------|
| **Patterns** | Generic advice | Battle-tested implementation code |
| **Anti-patterns** | None | "Don't do this because..." with alternatives |
| **Sharp Edges** | None | Gotchas with automatic detection |
| **Validations** | None | Regex patterns that catch mistakes |
| **Collaboration** | None | Skills delegate to each other |
| **Severity Levels** | None | Critical, high, medium, low |

---

## Quick Start

### Installation

**Option 1: Direct Clone**
```bash
# In your project directory
git clone https://github.com/Rigilance/claudetradingskills.git .claude-skills
```

**Option 2: Git Submodule (Recommended)**
```bash
# Better for version control - links the skills library as a submodule
git submodule add https://github.com/Rigilance/claudetradingskills.git .claude-skills
```

The submodule approach is recommended because it:
- Tracks specific versions of the skills library
- Keeps the skills library updated across projects
- Maintains clean separation between your project and the skills

### Usage with Claude

Tell Claude to read a skill:
```
Read: ~/.claude-skills/trading/technical-analysis/skill.yaml
```

Claude now has specialist knowledge - ask it to analyze charts, identify patterns, or build trading strategies!

---

## The 4-File Skill System

### 1. `skill.yaml` - Identity & Patterns

Defines who the skill is and how it works:

```yaml
id: technical-analysis
name: Technical Analysis Specialist
version: "1.0.0"

identity:
  role: Technical Analysis Expert
  personality: |
    You've analyzed thousands of charts across multiple asset classes.
    You understand that TA is probabilistic, not predictive. You focus
    on risk/reward setups and always define invalidation levels.

patterns:
  - name: Multi-Timeframe Analysis
    when_to_use: Any directional trade setup
    implementation: |
      1. Higher timeframe: Identify trend direction
      2. Middle timeframe: Find key levels
      3. Lower timeframe: Entry trigger

anti_patterns:
  - name: Indicator Overload
    why_bad: More indicators ≠ better analysis. Creates analysis paralysis.
    what_to_do_instead: Use 2-3 complementary indicators maximum.

handoffs:
  - trigger: "risk management|position sizing"
    to: risk-management
    context: "Trade setup identified, need sizing"
```

### 2. `sharp-edges.yaml` - Gotchas & Warnings

Things that bite you in production:

```yaml
sharp_edges:
  - id: trading-against-trend
    summary: Fighting the dominant trend
    severity: high
    situation: Taking counter-trend trades in strong momentum
    why: |
      Counter-trend trades have lower probability.
      "The trend is your friend until the bend at the end."
    solution: |
      ## Before Counter-Trend Trades:
      - Is there clear divergence on multiple timeframes?
      - Is price at a major structural level?
      - Is there volume confirmation?
      
      If not, wait for trend to weaken first.
    symptoms:
      - "I think this is oversold"
      - "It can't go higher/lower"
      - Multiple stop-outs in a row
    detection_pattern: "oversold|overbought|can't go|due for"
```

### 3. `validations.yaml` - Automated Checks

Catch mistakes before they cost money:

```yaml
validations:
  - id: no-stop-loss
    name: Missing Stop Loss
    severity: critical
    type: conceptual
    check: "Every trade must have a defined stop loss"
    indicators:
      - "No stop mentioned"
      - "Will add stop later"
      - "Mental stop"
    message: "No stop loss defined - this is gambling, not trading."
    fix_action: "Define exact stop loss price BEFORE entry."

  - id: risk-reward-ratio
    name: Poor Risk/Reward
    severity: high
    type: conceptual
    check: "Risk/reward should be at least 1:2"
    indicators:
      - "Small target"
      - "Wide stop"
    message: "Risk/reward ratio below 1:2"
    fix_action: "Adjust entry, stop, or target to achieve minimum 1:2 R:R"
```

### 4. `collaboration.yaml` - Skill Teamwork

How skills work together:

```yaml
receives_from:
  - skill: market-regime
    context: "Current market conditions"
    receives:
      - "Trend vs range identification"
      - "Volatility regime"
    provides: "Appropriate TA strategy selection"

delegation_triggers:
  - trigger: "position size|how much"
    delegate_to: risk-management
    pattern: sequential
    context: "Calculate position size for setup"

  - trigger: "news|fundamentals|earnings"
    delegate_to: fundamental-analysis
    pattern: parallel
    context: "Validate TA with fundamentals"

common_combinations:
  - name: Complete Trade Analysis
    skills:
      - technical-analysis
      - risk-management
      - market-regime
      - trade-execution
    workflow: |
      1. Identify market regime (market-regime)
      2. Find high-probability setup (technical-analysis)
      3. Calculate position size (risk-management)
      4. Plan execution (trade-execution)
```

---

## Skill Categories

| Category | Skills | Description |
|----------|--------|-------------|
| **trading** | 15 | Technical analysis, risk management, execution |
| **crypto** | 12 | DeFi, on-chain analysis, market structure |
| **ai-agents** | 18 | Autonomous agents, browser automation, voice |
| **backend** | 20 | APIs, microservices, databases, caching |
| **frontend** | 15 | React, Next.js, state management, performance |
| **devops** | 18 | CI/CD, Docker, K8s, observability |
| **security** | 12 | Auth, OWASP, compliance, privacy |
| **data** | 14 | ETL, analytics, visualization, ML pipelines |
| **marketing** | 10 | Content, SEO, growth, viral strategies |
| **product** | 8 | PM, analytics, A/B testing, roadmapping |
| **finance** | 10 | Quant, derivatives, portfolio management |
| **startup** | 8 | MVP, fundraising, growth, founder mode |

---

## Trading-Focused Skills

Since you work with IKAGI market reports, here are particularly relevant skills:

### Core Trading Skills
- `trading/technical-analysis` - Chart patterns, indicators, multi-timeframe
- `trading/risk-management` - Position sizing, drawdown management
- `trading/market-regime` - Trend vs range identification
- `trading/pivot-trading` - Time-based pivot strategies
- `trading/trade-execution` - Entry/exit optimization

### Crypto-Specific Skills
- `crypto/btc-analysis` - Bitcoin-specific patterns and cycles
- `crypto/eth-analysis` - Ethereum ecosystem dynamics
- `crypto/defi-yields` - DeFi strategy analysis
- `crypto/on-chain` - On-chain metrics interpretation
- `crypto/market-structure` - Crypto market microstructure

### Market Analysis Skills
- `finance/macro-analysis` - Fed, rates, economic indicators
- `finance/correlation-trading` - Cross-asset correlations
- `finance/volatility` - VIX, options-based signals

---

## Documentation

- **[SKILLS_DIRECTORY.md](SKILLS_DIRECTORY.md)** - Complete list of all skills
- **[GETTING_STARTED.md](GETTING_STARTED.md)** - Detailed usage guide
- **[CONTRIBUTING.md](CONTRIBUTING.md)** - How to add or improve skills
- **[SKILL_TEMPLATE.md](SKILL_TEMPLATE.md)** - Template for creating new skills

---

## Example Usage

### Trading Analysis Workflow

```
User: Analyze BTC for a potential long entry

Claude: [Reads technical-analysis skill]
        [Reads risk-management skill]
        
Based on the IKAGI pivot dates and current structure:

**Multi-Timeframe Analysis:**
- Weekly: Range-bound between $70K-$103K
- Daily: Testing support at $91K
- 4H: Potential bullish divergence forming

**Setup:**
- Entry: $91,500 (on confirmation candle)
- Stop: $89,200 (below structure)
- Target 1: $96,000 (1:2 R:R)
- Target 2: $103,000 (resistance)

**Position Size:** 
- 1% risk = $XX at current account size
- Risk per trade: $2,300

**Validation:**
✓ Aligns with Jan 9 pivot date
✓ Above major $70-72K support
✓ Risk/reward meets 1:2 minimum
```

---

## License

MIT License - Free to use, modify, and distribute.

## Contributing

Pull requests welcome! See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.
