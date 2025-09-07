---
allowed-tools: Task, Write, Read, Glob, Grep, WebFetch, mcp__firecrawl__firecrawl_scrape, mcp__firecrawl__firecrawl_search, Bash(date:*), Bash(mkdir:*)
argument-hint: [agent-name] [test-task]
description: Evaluate sub-agent performance and effectiveness
model: claude-sonnet-4-20250514
---

# Agent Eval

Evaluate the performance and effectiveness of sub-agent `$1` by running it against the following task:

## Test Task

$2

## Instructions

**1. Fetch Latest Documentation**
Scrape the latest Claude Code sub-agent documentation:

- Sub-agent feature: https://docs.anthropic.com/en/docs/claude-code/sub-agents
- Available tools: https://docs.anthropic.com/en/docs/claude-code/settings#tools-available-to-claude

**2. Execute Test**
Run the agent against the provided test task and observe:

- Task completion success
- Tool usage patterns
- Response quality
- Execution efficiency

**3. Review Agent Configuration**
After completing the test, analyze the agent configuration at @.claude/subagents/$1.md to understand design choices and identify potential improvements.

**4. Save Evaluation Report**

- Create directory if needed: `mkdir -p .claude/evaluations/`
- Save report with timestamp: `.claude/evaluations/$1-$(date +%Y%m%d-%H%M%S).md`

## Output Format

Generate a concise evaluation report in markdown:

````markdown
# Agent Evaluation Report: $1

## Test Execution Summary

**Task**: $2
**Date**: $(date +%Y-%m-%d\ %H:%M:%S)
**Status**: [✅ PASS | ⚠️ NEEDS IMPROVEMENT | ❌ FAIL]
**Execution Time**: [Time taken]
**Overall Score**: [XX%]

## Metrics Score

| Metric          | Score   | Weight | Description                                     |
| --------------- | ------- | ------ | ----------------------------------------------- |
| Task Completion | XX%     | 30%    | Did the agent complete the requested task?      |
| Accuracy        | XX%     | 25%    | Was the output correct and error-free?          |
| Efficiency      | XX%     | 20%    | Tool usage and time efficiency                  |
| Error Handling  | XX%     | 15%    | How well were errors managed?                   |
| Code Quality    | XX%     | 10%    | If code generated, does it follow standards?    |
| **Total**       | **XX%** | 100%   | **[PASS >80% / NEEDS WORK 60-80% / FAIL <60%]** |

## Strengths

✅ **What Worked Well:**

- [Specific strength with evidence from execution]
- [Another positive observation with example]

## Issues & Recommendations

⚠️ **What Needs Improvement:**

### Issue 1: [Brief description]

- **Impact**: [How it affected the task]
- **Fix**: [Specific action to resolve]
- **Config Update** (if needed): `[exact config change]`

### Issue 2: [Brief description]

- **Impact**: [How it affected the task]
- **Fix**: [Specific action to resolve]

## Evidence

### Example Output

```text
[Key example showing agent's actual output]
```
````

### Tool Usage

- **Tools Used**: [List with counts, e.g., Read (3x), Write (1x)]
- **Efficiency Notes**: [Any redundant or missing tool usage]

```

## Next Steps
Based on this evaluation:
1. [Primary action item based on score]
2. [Secondary recommendation if applicable]
```
