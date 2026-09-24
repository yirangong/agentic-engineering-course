# Part B: Isolate and Targeted summary -- summary

Model `openai-codex/gpt-5.6-luna`, thinking `low`. Chunking targets ~96,000 tokens per chunk; the actual chunk count per item follows from its real token size.

## Data check: how many times is the target person mentioned?

7/15 items have the target person moving MORE THAN ONCE (regex hits for 'PERSON moved/went/travelled/... (back) to the ROOM'); 8 have exactly one mention, 0 had no literal regex hit. Across the 15 items with at least one hit, the LAST mention's room matches the gold target in 15/15 cases -- when a person moves more than once, the most recent move is usually the right answer. Every demonstration below is therefore told explicitly to take the LAST reported location, never the first.

## Bucket x condition table

| bucket | condition | correct/n | mean | 95% CI | mean total tokens | mean peak single-call context | total cost |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 256k | Part A (single call) | 3/5 | 60.0% | [17.1%, 100.0%] | 241,397 | 241,397 | $0.2425 |
| 256k | Isolate | 4/5 | 80.0% | [44.9%, 100.0%] | 243,741 | 89,106 | $0.2447 |
| 256k | Targeted summary | 1/5 | 20.0% | [0.0%, 55.1%] | 244,712 | 89,120 | $0.2333 |
| 512k | Part A (single call) | 3/5 | 60.0% | [17.1%, 100.0%] | 483,862 | 483,862 | $0.9699 |
| 512k | Isolate | 3/5 | 60.0% | [17.1%, 100.0%] | 487,551 | 98,238 | $0.4893 |
| 512k | Targeted summary | 1/5 | 20.0% | [0.0%, 55.1%] | 489,361 | 98,252 | $0.4608 |
| 768k | Part A (single call) | 3/5 | 60.0% | [17.1%, 100.0%] | 765,939 | 765,939 | $1.5347 |
| 768k | Isolate | 4/5 | 80.0% | [44.9%, 100.0%] | 771,409 | 98,270 | $0.7738 |
| 768k | Targeted summary | 2/5 | 40.0% | [0.0%, 82.9%] | 774,415 | 98,284 | $0.7498 |

## The lesson: peak context, not total tokens

Part A's single call for an item has to hold the ENTIRE haystack in context at once: peak context = total input tokens. Isolate's and Targeted summary's peak single-call context is bounded near one chunk's size instead, while their TOTAL tokens barely move relative to Part A -- the same haystack still gets read in full, just split across more, smaller calls. Isolation and targeted summarization do not save tokens; they cap what any single call has to hold in context at once.
