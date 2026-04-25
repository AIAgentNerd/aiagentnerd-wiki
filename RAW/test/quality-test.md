Model routing is a system where different models are used.

In our system:
- qwen/qwen-2.5-72b-instruct = default
- moonshotai/kimi-k2.6 = advanced tasks

We route wiki_compile to Kimi.

Sometimes Kimi truncates responses (finishReason: length).
Fallback goes to Qwen.

Costs can be optimized this way.

---
## Compiled Wiki
- WIKI: [[WIKI/architecture/quality-test]]
- Last compiled: 2026-04-25T14:00:07.207Z
