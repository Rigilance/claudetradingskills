# Contributing to Claude Skills Library

## How to Add a New Skill

### 1. Create the Skill Directory

```bash
mkdir -p skills-library/category/skill-name
```

### 2. Create the 4 Required Files

#### skill.yaml (required)

```yaml
id: skill-name
name: Human Readable Name
version: "1.0.0"
category: category-name
tags: [tag1, tag2]

identity:
  role: Expert Role
  personality: |
    Description of the skill's expertise and approach.

core_principles:
  - Principle 1
  - Principle 2

patterns:
  - name: Pattern Name
    when_to_use: When to apply this pattern
    implementation: |
      Step by step implementation details

anti_patterns:
  - name: Anti-Pattern Name
    why_bad: Why this is problematic
    what_to_do_instead: Better approach

handoffs:
  - trigger: "keyword|phrase"
    to: other-skill
    context: "Context for handoff"
```

#### sharp-edges.yaml (required)

```yaml
sharp_edges:
  - id: unique-id
    summary: Brief description
    severity: critical|high|medium|low
    situation: When this occurs
    why: Why it's problematic
    solution: How to fix/avoid
    symptoms:
      - "Warning sign 1"
      - "Warning sign 2"
    detection_pattern: "regex|pattern|keywords"
```

#### validations.yaml (required)

```yaml
validations:
  - id: validation-id
    name: Validation Name
    severity: critical|high|medium|low
    type: conceptual|regex
    check: "What is being validated"
    indicators:
      - "Sign of failure 1"
    message: "Error message"
    fix_action: "How to fix"
```

#### collaboration.yaml (required)

```yaml
skill_id: skill-name
collaboration_version: "1.0"

receives_from:
  - skill: other-skill
    receives: ["data1", "data2"]
    provides: "What this skill adds"

provides_to:
  - skill: another-skill
    provides: ["output1", "output2"]

delegation_triggers:
  - trigger: "keywords"
    delegate_to: other-skill
    context: "Why delegating"

common_combinations:
  - name: Workflow Name
    skills: [skill1, skill2]
    workflow: |
      Step by step workflow
```

### 3. Test Your Skill

1. Read the skill in Claude
2. Test various prompts
3. Verify patterns work as expected
4. Check handoffs trigger correctly

### 4. Submit PR

1. Fork the repository
2. Create a branch
3. Add your skill
4. Submit pull request

## Quality Guidelines

- **Concise**: Only include non-obvious information
- **Actionable**: Patterns should be implementable
- **Complete**: All 4 files required
- **Tested**: Verify skill works before PR
