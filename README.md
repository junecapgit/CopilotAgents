# Copilot Agent Pack

This repository contains a set of custom GitHub Copilot agent definitions for software delivery, architecture, code review, testing, and sprint planning.

The agents are written as `.agent.md` files with frontmatter that defines the agent name, purpose, tool access, and downstream agents it can coordinate with. The prompts themselves are opinionated toward pragmatic execution: minimal changes, explicit validation, production safety, and concise handoffs.

## What Is Included

This pack currently includes agents in four broad groups:

- Generic engineering agents for cross-stack implementation and architecture work
- C# agents for review, implementation, architecture, and test writing
- Java agents for review, implementation, architecture, and test writing
- Delivery planning agents for sprint decomposition and Scrum execution

## Agent Catalog

| Agent | Focus | Best Used For |
| --- | --- | --- |
| `generic-senior-software-engineer` | Cross-stack implementation | Feature work, bug fixes, refactoring, production-safe changes |
| `generic-senior-software-architect` | Cross-stack architecture | System design, modernization, service boundaries, tradeoff analysis |
| `csharp-senior-software-engineer` | C# implementation | .NET features, refactors, defect fixes, engineering execution |
| `csharp-senior-software-architect` | C# architecture | .NET system design, architectural review, maintainability strategy |
| `csharp-code-review` | C# review | PR review, regression and risk analysis, missing test identification |
| `csharp-test-writer` | C# testing | xUnit, Moq, ASP.NET Core integration and regression tests |
| `java-sr-software-engineer` | Java implementation | Java and Spring feature work, refactors, bug fixes |
| `java-senior-software-architect` | Java architecture | Java and Spring architecture, boundary design, modernization |
| `java-code-review` | Java review | Review of Java code changes for correctness, risk, and coverage gaps |
| `java-test-writer` | Java testing | JUnit 5, Mockito, Spring slice and integration tests |
| `agile-sprint-planner` | Sprint decomposition | Breaking initiatives into sprint-sized stories, tasks, and risk-aware plans |
| `scrum-master` | Delivery orchestration | Sprint planning, backlog refinement, sequencing, blockers, re-planning |
| `azure-ms-engineer` | Azure engineering | Azure infrastructure, deployment workflows, diagnostics, security, reliability, and cost-aware cloud changes |

## Design Principles

Most agents in this repo follow the same structure:

1. Frontmatter metadata for discovery and routing
2. Clear constraints describing what the agent must not do
3. Explicit responsibilities and priorities
4. A defined working approach or review process
5. A fixed output format for consistent responses
6. Inter-agent coordination rules and a handoff template

That consistency is intentional. It makes the agents easier to compose, easier to maintain, and more predictable when used in a larger workflow.

## File Layout

```text
agents/
  agile-sprint-planner.agent.md
  azure-ms-engineer.agent.md
  csharp-code-review.agent.md
  csharp-senior-software-architect.agent.md
  csharp-senior-software-engineer.agent.md
  csharp-test-writer.agent.md
  generic-senior-software-architect.agent.md
  generic-senior-software-engineer.agent.md
  java-code-review.agent.md
  java-senior-software-architect.agent.md
  java-sr-software-engineer.agent.md
  java-test-writer.agent.md
  scrum-master.agent.md
```

## How To Use

Use these agents when you want Copilot to operate with a more specialized role and response contract than the default general-purpose assistant.

Typical usage pattern:

1. Choose the agent that best matches the task.
2. Provide clear scope, constraints, and validation expectations.
3. Let the agent inspect the relevant files and produce the requested work.
4. If needed, use the handoff packet format to pass work to a downstream specialist agent.

Examples:

- Use `java-code-review` to review a Java PR for regressions, concurrency issues, and missing tests.
- Use `csharp-test-writer` after a .NET bug fix to add targeted regression coverage.
- Use `generic-senior-software-architect` to evaluate service boundaries before a refactor.
- Use `agile-sprint-planner` to turn a feature brief into a sprint-ready backlog.

## Authoring Pattern

Each `.agent.md` file typically includes these frontmatter fields:

- `name`: The agent identifier
- `description`: Short guidance on when to use the agent
- `argument-hint`: What the user should provide as input
- `tools`: Tool classes the agent is expected to use
- `agents`: Other agents it can coordinate with

After the frontmatter, the body defines the agent's operating rules and expected output.

## Extending The Pack

When adding a new agent, keep the existing conventions unless there is a good reason to diverge:

1. Give the agent a narrow, outcome-oriented role.
2. State hard constraints up front.
3. Define priorities in the order they should be applied.
4. Standardize the output format so results are easy to consume.
5. Add downstream agent coordination only where it is genuinely useful.

## Recommended Next Step

If this repository is going to be published, the next highest-value improvement is to add one or two concrete usage examples per agent so new users can pick the right specialist faster.
