---
title: Quality Test
source_raw: RAW/test/quality-test.md
compiled_wiki_path: WIKI/architecture/quality-test.md
compiled_at: 2026-04-25T14:00:07.207Z
type: system-note
tags: [aiagentnerd, compiled, architecture, quality]
---

# Quality Test

## Summary
The system routes inference requests between two models based on task classification. `qwen/qwen-2.5-72b-instruct` serves as the default handler, while `moonshotai/kimi-k2.6` is reserved for advanced tasks such as `wiki_compile`. If Kimi returns a truncated response with `finishReason: length`, the request automatically falls back to Qwen to preserve output completeness.

## Key Concepts
- **Default model**: `qwen/qwen-2.5-72b-instruct` handles standard traffic
- **Advanced model**: `moonshotai/kimi-k2.6` is targeted at complex or long-context workloads
- **Explicit routing**: `wiki_compile` tasks are directed to Kimi
- **Truncation fallback**: Kimi responses cut short by length limits are retried with Qwen
- **Cost optimization**: Selective use of the advanced model reduces overall inference spend

## Details
Model routing evaluates the incoming task type to assign the appropriate backend. Routine operations hit the default Qwen endpoint, minimizing latency and cost for general queries. Advanced

## Source
- RAW: [[RAW/test/quality-test]]

## Related
- [[auto-test]]
- [[empty-test]]
- [[karpathy-llm-wiki-test]]
- [[backlink-test]]
- [[test-nginx]]
