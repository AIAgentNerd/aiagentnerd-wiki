# Model Routing Fallback Patterns and Operational Resilience

## Summary
Task logs confirm that the AiAgentNerd/GoldieNerd routing layer assigns `wiki_compile` and advanced workloads to `moonshotai/kimi-k2.6`, while `qwen/qwen-2.5-72b-instruct` handles default traffic. However, Kimi exhibits intermittent empty-content failures via OpenRouter. The system demonstrates operational resilience by falling back to Qwen when Kimi returns empty content or truncates output (`finishReason: length`). Qwen serves as both the default gateway and the reliable safety net for failed specialist inference.

## Key Concepts
- **Task-Aware Routing**: The system classifies requests by task type (e.g., `wiki_compile`, `code`, `long_context`, `background`) and routes them to the secondary model; all untagged or unrecognized requests fall back to the primary model.
- **Specialist vs. Generalist**: Kimi K2.6 is the advanced model for complex compilation and long-context tasks; Qwen 2.5 72B Instruct is the generalist default and catch-all.
- **Empty-Content Failure Mode**: OpenRouter can return completely empty content for `moonshotai/kimi-k2.6` without raising a conventional HTTP error, requiring explicit response validation.
- **Length-Truncation Fallback**: When Kimi responses hit token limits (`finishReason: length`), the system automatically reissues the request to Qwen to preserve output completeness.
- **Graceful Degradation**: The architecture treats the secondary model as potentially unreliable and uses the primary model as a hot standby.

## Practical Use
- Route documentation compilation, code analysis, and long-context tasks to Kimi for higher capability.
- Use Qwen for standard traffic, low-latency queries, and all unrecognized task types.
- Validate every Kimi response for empty content before processing; if empty, retry via Qwen rather than surfacing a failure to the user.
- Monitor Kimi responses for `finishReason: length` to trigger immediate fallback and avoid delivering truncated artifacts.

## Implementation Notes
- **Primary Model**: `qwen/qwen-2.5-72b-instruct` — default route and universal fallback.
- **Secondary Model**: `moonshotai/kimi-k2.6` — invoked for `wiki_compile`, `code`, `long_context`, and `background` tasks.
- **Observed Failure**: `OpenRouter returned empty content for moonshotai/kimi-k2.6` — classify as a retryable fallback event, not a fatal error.
- **Fallback Triggers**:
  1. Empty content returned for Kimi.
  2. `finishReason: length` on Kimi response.
  3. Unrecognized or untagged task type (implicit default to Qwen).
- **Operational Logging**: Record fallback events distinctly to separate primary vs. secondary inference paths for cost tracking and quality analysis.

---
Promoted from system draft: 2026-04-25-2118-learning.md
Promoted at: 2026-04-25T14:29:35.903Z
