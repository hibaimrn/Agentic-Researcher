# Agentic Researcher

A model-driven research agent where the LLM decides every step: what to search for, which findings matter, and when you have enough to write a comprehensive report.

## Overview

Agentic Researcher is a fully autonomous agent for conducting thorough research on complex topics. Unlike rigid workflows, this agent uses its own judgment at every step—deciding what to search for, how to refine queries based on results, when to resolve contradictions, and when coverage is sufficient to write a report.

The agent produces well-structured, cited research reports with an executive summary, themed sections, and a sources list.

## Features

- **True Autonomy**: Agent decides strategy, not following a fixed workflow
- **Smart Searching**: Focuses on targeted queries, refines based on results
- **Contradiction Resolution**: Detects conflicting sources and searches again
- **Note-Taking System**: Saves findings as it goes; grounded reports only
- **Quality Report Generation**: 
  - Executive summary
  - Themed sections organized by insight
  - Conclusion
  - Sources section with URLs
- **Real-Time Trace**: Watch the agent think, search, and build its case
- **Export Options**: Copy or download as Markdown
- **Step Budget Management**: Operates within configurable token/step budget

## How It Works

```
Agent's self-directed process:

1. [Think] "I need to understand X, Y, and Z for this topic"
2. [Search] Perform focused query on one aspect
3. [Save] Extract key finding as a note with source
4. [Assess] "Do I have enough? Or are there gaps?"
5. [Search] Refine query based on findings
6. [Detect] "These sources conflict — need to resolve"
7. [Search] Query to clarify contradiction
8. [Repeat] Until coverage is sufficient
9. [Read] Pull all notes into context
10. [Write] Generate comprehensive report
```

The agent controls this loop—no human intervention needed.

## Getting Started

### Requirements

- OpenAI API key (for gpt-4o or gpt-4o-mini)
- Modern web browser
- Internet connection for web research

### Usage

1. **Load the HTML** in your browser
2. **Enter your OpenAI API key** (sent to OpenAI only, not stored)
3. **Set your research goal**:
   - Example: "Compare current approaches to evaluating RAG pipelines and recommend one for a small team"
   - Be specific about what you want to learn
4. **Configure**:
   - **Model**: gpt-4o (recommended) or gpt-4o-mini (cheaper)
   - **Step budget**: 10 (quick), 15 (standard), 25 (thorough)
5. **Click "Deploy agent"**
6. **Watch the trace** as the agent researches
7. **Read the report** on the right as it's generated

### Configuration

| Option | Default | Purpose |
|--------|---------|---------|
| Model | gpt-4o | LLM for decision-making and writing |
| Step budget | 15 | Max reasoning steps |
| Use web search | Yes | Agent can search for information |

## Understanding the Interface

**Left Panel (Configuration + Trace)**:
- Configuration inputs at top
- Agent trace below showing:
  - `thinking`: Agent's reasoning about next steps
  - `tool: web_search`: Queries executed
  - `result`: Snippet of search results
  - `tool: save_note`: Findings being saved
  - `tool: read_notes`: Agent reviewing accumulated findings
  - `error`: Any issues encountered
  - `final`: Report delivery and stats

**Right Panel (Report)**:
- Live rendering of the final Markdown report
- Includes sections, lists, tables, blockquotes
- Print-ready formatting

## Report Structure

The agent generates reports with:

```markdown
# [Topic Title]

## Executive Summary
High-level overview of key findings and recommendations.

## [Themed Section 1]
Findings organized by topic or insight.

## [Themed Section 2]
Further exploration of related aspects.

## Conclusion
Summary of what was learned and recommendations.

## Sources
URLs with titles of sources used.
```

## Example Research Goals

✅ **Good**:
- "Compare RAG evaluation frameworks: RAGAS, TruLens, LangSmith. Which is best for startup teams?"
- "What are the latest approaches to AI safety oversight? Summarize evals, red-teaming, and constitutional AI."
- "Analyze market size and growth trends for AI in legal tech."

❌ **Too Vague**:
- "Tell me about AI"
- "Research machine learning"
- "What's new in AI?"

✅ **Realistic**:
- "How do leading LLM inference optimization techniques (quantization, distillation, KV-cache) compare on latency and accuracy?"
- "What frameworks exist for LLM alignment evals and how do they work?"

## Tips for Best Results

1. **Specific Angle**: Include the use case or decision you're trying to make
2. **Time Sensitivity**: Mention if you need cutting-edge (past 6 months) info
3. **Scope**: Define what's in scope and what's not
4. **Expertise Level**: Mention if the audience is engineers, execs, or general
5. **Length**: Don't worry—agent adapts to budget

### Example: Strong vs. Weak Brief

**Weak**:
```
Research goal: Compare AI safety approaches
Step budget: 15
```

**Strong**:
```
Research goal: Compare LLM safety evaluation frameworks 
(RAGAS, TruLens, Constitutional AI evals) with focus on 
which are practical for a 5-person AI startup team. 
Consider cost, ease of setup, and reliability.
Step budget: 20
```

The stronger brief guides the agent's strategy and saves steps.

## Cost

Approximate costs per research run:
- **Quick** (gpt-4o-mini, 10 steps): ~$0.15–0.35
- **Standard** (gpt-4o, 15 steps): ~$0.50–1.20
- **Thorough** (gpt-4o, 25 steps): ~$1.00–2.50

*Varies by complexity and number of searches.*

## Architecture

**Frontend**: Single-file HTML/CSS/JavaScript

**Integrations**:
- OpenAI Chat API (gpt-4o, gpt-4o-mini)
- Web search via Perplexity API
- Marked.js for Markdown rendering

**Agent Toolset**:
- `web_search(query)` - Search the web for information
- `save_note(note, source)` - Record a finding with source attribution
- `read_notes()` - Review all accumulated findings
- `write_report(markdown)` - Deliver the final report

## Advanced Behavior

### Contradiction Detection
If the agent encounters conflicting claims:
1. It notes the contradiction
2. It searches again with refined query
3. It updates notes with clarification
4. It documents the disagreement in the report

### Query Refinement
The agent learns from search results:
- Initial broad search → "I need more specific info on X"
- Refined search → "Now I understand the landscape"
- Gap detection → "I'm missing info on Y, let me search"

### Coverage Assessment
The agent decides when to stop searching:
- ✅ "I have enough to write a report"
- ⏳ "I'm missing comparative data, need one more search"
- ⚠️ "Budget running low, time to synthesize"

## Privacy & Security

- **API keys**: Sent only to OpenAI; not stored or logged
- **Browser-based**: All computation happens client-side
- **No tracking**: No analytics or telemetry
- **Session-scoped**: Content cleared on refresh
- **HTTPS recommended**: Use secure connection for API key

## Limitations

- Reports reflect web search results (quality depends on sources)
- Agent won't invent statistics or sources
- Long timeouts on some searches (retries automatically)
- No access to paywalled academic papers
- No real-time data updates (searches are point-in-time)

## Typical Usage Patterns

### Pattern 1: Due Diligence Research
```
Goal: Evaluate 3 new AI safety platforms for safety benchmarking
Budget: 20 steps
Expected output: Comparison matrix, pros/cons, recommendation
```

### Pattern 2: Landscape Scan
```
Goal: What are the top frameworks and tools for LLM evaluation in 2024?
Budget: 15 steps
Expected output: List of options, key differences, where each shines
```

### Pattern 3: Deep Dive
```
Goal: How does Constitutional AI work? What are its strengths and limitations compared to RLHF?
Budget: 25 steps
Expected output: Technical explanation, comparison, when to use each
```

## Error Handling

| Issue | Behavior | Mitigation |
|-------|----------|-----------|
| Invalid API key | Clear error immediately | Re-enter key |
| Search timeout | Agent retries or skips | Disable search, retry |
| Step budget exhausted | Delivers report from notes so far | Increase budget |
| Contradictory sources | Agent searches to resolve | Noted in report |
| No relevant results | Agent adapts query | Try different angle |

## Future Enhancements

- [ ] Multi-agent research (parallel searches)
- [ ] Access to academic paper abstracts
- [ ] Citation formatting (APA, Chicago, etc.)
- [ ] Report templates for specific use cases
- [ ] Interactive follow-up questions during research
- [ ] Comparison tables generated automatically
- [ ] Fact-checking against known sources

## License

MIT

## Contributing & Feedback

Found an issue? Have a suggestion? Open an issue or PR.
