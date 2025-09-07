---
allowed-tools: Task, WebFetch, mcp__firecrawl__firecrawl_scrape, mcp__firecrawl__firecrawl_search, mcp__firecrawl__firecrawl_crawl, mcp__firecrawl__firecrawl_check_crawl_status, Read, Bash(ls:*), Bash(grep:*), Bash(find:*)
argument-hint: [agent-name] [test-task]
description: Evaluate sub-agent performance and effectiveness
model: claude-3-5-sonnet-20241022
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

**2. Review Agent Configuration**
Analyze the agent configuration at @.claude/subagents/$1.md if it exists.

**3. Execute Test**
Run the agent against the provided test task and observe:
- Task completion success
- Tool usage patterns
- Response quality
- Execution efficiency

## Current Context
- Available agents: !`ls -la .claude/subagents/ 2>/dev/null || echo "No agents directory found"`
- Working directory: !`pwd`
- Project structure: !`find . -type f -name "*.md" -path "*/.claude/*" 2>/dev/null | head -10`

## Output Format

Generate a detailed evaluation report in markdown:

```markdown
# Agent Evaluation Report: $1

## Test Scenario
**Task**: $2
**Timestamp**: [Current timestamp]
**Model Used**: [Model the agent used]
**Execution Environment**: [Claude Code version, OS]

## Performance Analysis

### Task Completion
- **Status**: [Complete/Partial/Failed]
- **Accuracy**: [High/Medium/Low with explanation]
- **Execution Time**: [Time taken]
- **Number of Attempts**: [If retry was needed]

### Tool Usage
- **Tools Called**: [List of tools used with counts]
- **Efficiency**: [Rating with explanation]
- **Appropriateness**: [Were the right tools used?]
- **Unnecessary Calls**: [Any redundant tool usage]

### Output Quality
- **Clarity**: [Rating 1-10 with examples]
- **Completeness**: [Rating 1-10 with gaps identified]
- **Correctness**: [Rating 1-10 with any errors noted]
- **Format Compliance**: [Did it follow expected format?]

## Strengths Identified
1. [Specific strength with example from execution]
2. [Another strength with evidence]
3. [Additional positive observations]

## Areas for Improvement
1. [Specific issue with recommendation]
   - **Issue**: [Description]
   - **Impact**: [How it affected performance]
   - **Solution**: [Suggested fix]

2. [Another area with suggested fix]
   - **Issue**: [Description]
   - **Impact**: [How it affected performance]
   - **Solution**: [Suggested fix]

## Tool Usage Patterns
- **Most Used Tools**: [List with frequency]
- **Tool Chain Efficiency**: [How well tools were sequenced]
- **Missing Tool Usage**: [Tools that should have been used]

## Error Analysis
- **Errors Encountered**: [List any errors]
- **Recovery Actions**: [How errors were handled]
- **Error Prevention**: [Suggestions to avoid errors]

## Optimization Recommendations

### Immediate (Can implement now)
1. [Quick fix with specific code/config change]
2. [Another immediate improvement]

### Short-term (1-2 weeks)
1. [Enhancement requiring modest effort]
2. [Another short-term improvement]

### Long-term (Strategic)
1. [Major enhancement or redesign]
2. [Strategic improvement]


## Specific Examples

### Success Case
```
[Show a specific example where the agent performed well]
```

### Failure/Suboptimal Case
```
[Show a specific example where improvement is needed]
```

## Configuration Recommendations

### Current Configuration Issues
[Any problems with the current agent configuration]

### Suggested Configuration
```markdown
[Provide improved configuration snippet if needed]
```

## Testing Edge Cases

### Edge Cases Tested
1. [Edge case 1]: [Result]
2. [Edge case 2]: [Result]

### Untested Scenarios
1. [Scenario that should be tested]
2. [Another important test case]

## Final Assessment

### Scoring Matrix
| Metric | Score | Weight | Weighted Score |
|--------|-------|--------|----------------|
| Task Completion | X/10 | 30% | X.X |
| Output Quality | X/10 | 25% | X.X |
| Tool Efficiency | X/10 | 20% | X.X |
| Error Handling | X/10 | 15% | X.X |
| Speed | X/10 | 10% | X.X |
| **Total** | | | **X.X/10** |

### Recommendation
- **Status**: [Production Ready / Needs Refinement / Major Rework Needed]
- **Confidence Level**: [High/Medium/Low]
- **Primary Action**: [Most important next step]

### Best Use Cases
1. [Scenario where this agent excels]
2. [Another good use case]

### Limitations
1. [Known limitation or constraint]
2. [Another limitation to be aware of]

## Appendix

### Full Execution Log
[Option to include detailed execution trace if needed]

### Related Agents
- [List other agents that might be relevant]

### Documentation References
- [Links to relevant documentation]
```

## Error Handling

If the agent `$1` doesn't exist or the task is unclear:
1. List available agents in the `.claude/subagents/` directory
2. Suggest clarification for the test task
3. Provide guidance on creating the agent if it doesn't exist

## Notes

- This evaluation focuses on objective metrics and actionable improvements
- Consider running multiple test tasks for comprehensive evaluation
- Document any assumptions made during evaluation
- Include both quantitative metrics and qualitative observations