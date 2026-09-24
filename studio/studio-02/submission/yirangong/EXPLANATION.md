Team: <>  Members: <yg2990, Yiran Gong, >

## What we ran
*Specify the exact commands, flags, and model provider ID used for your runs.*
I used pi, to login in and connect to my chatgpt plus account. And switched model to openai-codex/gpt-5.6-luna by command (/model). 

First downloaded the benchmark dataset "BABILong" package. It contains examples that are 256k/512k/1M tokens long. Also builds a 768K token long bucket from the 1M token bucket. From each bucket (256k, 512k, 768k) 5 items are sampled, and built into a subset dataset.  

Each item is like "Long passage + question → model’s answer → compare with correct answer"

## What degraded in Part A
*Identify the specific context window bucket where accuracy first dropped and provide the real accuracy numbers from your Part A runs.*


| bucket | correct/n | accuracy | mean real input tokens | total cost |
| --- | --- | --- | --- | --- |
| 256k | 3/5 | 60% | 241,397 | $0.2425 |
| 512k | 3/5 | 60% | 483,862 | $0.9699 |
| 768k | 3/5 | 60% | 765,939 | $1.5347 |

All accuracy are the same. 


## What fixed it in Part B
*Describe whether Isolate, Targeted summary, or both fixed the degradation, and provide the before and after accuracy numbers.*

Instead of asking the model to read a super long document, in this section, we split each long item into 96K-token chunks. 

To mitigate the degradation of long context, two strategies are used here : Isolate and Targeted summary. 

A visual of the process: 
300K-token document
        ↓ split
[96K] [96K] [96K] [12K]
        ↓
short report [Isolate] or ~200-token summary from each chunk [Targeted summary]
        ↓
one final answer

Results: 
Isolate: in creased accuracy in 256k bucket (80%) and 768k bucket (80%), no change comparing to the baseline in 512k bucket. On aevrage, there's an increase of performance. 

Targeted summary: performed below baseline (60%). For the 256k and 512k bucket, accuracy is at 20%, and there's a slight increase at 768k bucket where accuracy reaches 40%. 


## What memory got right/wrong in Part C
*Analyze what decisions or information the persistent-memory run got right or wrong compared to the memoryless baseline.*

In session 1, the agent made some decisions and kept them in decisions.md. In session 2, there is an unrelated Fibonacchi task. 

In Session 3, another fresh agent session was asked to recall the three decisions from Session 1.

With memory, the agent correctly recognized the tasks from session 1, and ignored the irrelevant information from session 2. So its recall result was 3/3.

The memoryless baseline was given the same question but did not have access to decisions.md or the earlier conversation. It answered: “I can’t determine that from the files available in the current directory.” Therefore, it recalled 0/3 decisions.

This section therefore shows that the agent's memory means a set of instructions can be used across different sessions. 

## What remains unknown
*List any open questions, unexpected anomalies, or unresolved issues from your runs.*

The baseline data only calculates the accuracy from 5 subsets. The result might not be representative. 

I don't know why there's a shift in the x axis in the 3 buckets, in part b. 


## Who did what
*Each team member must list their UNI or GitHub ID and write exactly one paragraph describing their own individual contribution without using full names.*

[yg2990, yirangong88: Wrote everything independently]
