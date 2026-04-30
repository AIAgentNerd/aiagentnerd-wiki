---
title: Quality Test
source_raw: RAW/test/quality-test.md
compiled_wiki_path: WIKI/architecture/quality-test.md
compiled_at: 2026-04-25T14:01:41.704Z
type: system-note
tags: [aiagentnerd, compiled, architecture, quality]
---

# Quality Test

## Summary
The system implements model routing to direct requests to the most appropriate LLM based on task characteristics. Qwen 2.5 72B Instruct serves as the default model, while MoonshotAI Kimi K2.6 handles advanced tasks such as `wiki_compile`. A fallback to Qwen triggers when Kimi truncates responses due to length limits.

## Key Concepts
- **Default routing**: Standard requests are handled by `qwen/qwen-2.5-72b-instruct`
- **Advanced routing**: Complex or long-context tasks, including `wiki_compile`, are routed to `moonshotai/kimi-k2.6`
- **Truncation fallback**: Responses cut short with `finishReason: length` on Kimi automatically fall back to Qwen
- **Cost control**: Routing expensive calls selectively to Kimi optimizes overall inference costs

## Details
Tasks classified as advanced or requiring extended context are assigned to Kimi K2.6. However, Kimi occasionally truncates outputs when it exceeds its generation limit. The system detects this via `finishReason: length` and reissues the request to Qwen 2.5 72B Instruct as a fallback. This ensures task completion without permanently defaulting to the more expensive or heavier model for all operations.

## Practical Notes
- Monitor logs for `finishReason: length` to track Kimi truncation frequency
- Verify fallback Qwen completions maintain acceptable quality for `wiki_compile` outputs
- Periodically review the advanced task classification list to ensure cost-effective routing

## Source
- RAW: [[RAW/test/quality-test]]

## Related
- [[auto-test]]
- [[empty-test]]
- [[karpathy-llm-wiki-test]]
- [[backlink-test]]
- [[test-nginx]]
