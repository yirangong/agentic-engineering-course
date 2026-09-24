# Part A: BABILong qa1, accuracy vs context length

Single-message delivery, compaction disabled, exact-match scoring.

| bucket | n | mean | 95% CI | mean real input tokens |
| --- | --- | --- | --- | --- |
| 256k | 5 | 60.0% | [17.1%, 100.0%] | 241,397 |
| 512k | 5 | 60.0% | [17.1%, 100.0%] | 483,862 |
| 768k | 5 | 60.0% | [17.1%, 100.0%] | 765,939 |

The 768K bucket has no native BABILong equivalent: it is built by truncating 1M-bucket items to 768,000 tokens and keeping only those whose qa1 supporting fact survives truncation. Surviving needles never sit past about 80 percent of the original document, so that bucket is structurally somewhat easier than an unbiased sample of the same length; any decline it shows is, if anything, an understatement.
