# Getting Started with Claude Skills Library

## Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/claude-skills-library ~/.claude-skills
```

### 2. Use a Skill

Tell Claude to read the skill:

```
Read: ~/.claude-skills/trading/technical-analysis/skill.yaml
```

Claude will now have specialized knowledge for that domain.

## Understanding Skill Structure

Each skill has 4 YAML files:

```
skill-name/
├── skill.yaml           # Identity, patterns, anti-patterns
├── sharp-edges.yaml     # Gotchas and warnings
├── validations.yaml     # Quality checks
└── collaboration.yaml   # How skills work together
```

### skill.yaml
- **identity**: Who the skill is (role, personality)
- **patterns**: Best practices with implementation details
- **anti_patterns**: What to avoid and why
- **handoffs**: When to delegate to other skills

### sharp-edges.yaml
- Common mistakes and how to avoid them
- Severity levels (critical, high, medium, low)
- Detection patterns for automatic warnings

### validations.yaml
- Automated checks for quality
- Conceptual validations (does the analysis include X?)
- Code validations (regex patterns)

### collaboration.yaml
- What this skill receives from others
- What this skill provides to others
- Common skill combinations and workflows

## Example Workflow

### Trading Analysis

1. Tell Claude to read the trading skills:
   ```
   Read these skills for trading analysis:
   - ~/.claude-skills/trading/technical-analysis/skill.yaml
   - ~/.claude-skills/trading/risk-management/skill.yaml
   - ~/.claude-skills/trading/pivot-trading/skill.yaml
   ```

2. Ask for analysis:
   ```
   Analyze BTC for potential entry based on IKAGI January pivots.
   Current pivots: Jan 1, 9, 23, 29
   Support: $70K-$72K
   Resistance: $96K-$103K
   ```

3. Claude will provide:
   - Multi-timeframe technical analysis
   - Position sizing calculation
   - Pivot-adjusted recommendations
   - Risk/reward assessment

## Tips

1. **Load relevant skills** before complex tasks
2. **Skills can call other skills** via handoffs
3. **Check sharp-edges** for common mistakes
4. **Use validations** as a checklist

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) for how to add skills.
