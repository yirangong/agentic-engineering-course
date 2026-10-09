# Studio 05: Build a Tool Server

```text
  +-------------------+        +---------------------+
  | your MCP server   | <----> | Codex, gpt-5.6-luna |
  | over your data    |        | uses your tools     |
  +---------+---------+        +----------+----------+
            |                             |
            v                             v
   direct calls refuse            headless runs and an
   "delete all data"              evaluation, before and after
```

Build an MCP server over local data you own, connect it to an agent in Codex, make sure your code stops "delete all data", and measure how reliably the agent uses your tools. There is no starter code: the domain, the language, the SDK and the design are yours. You are graded on four checkpoints and your explanation, 10 points in all.

- [Assignment instructions](instruction/Studio_Instruction.md)
- [Grading rubric](instruction/GRADING_RUBRIC.md)
- [Submission folder and explanation template](submission/README.md)
