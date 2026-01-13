# Incorporating Large Language Models into the Computer Science Curriculum at BYU.

This repository includes an analysis of how to prepare students to develop skills that will equip them to complete in an environment where most industry programmers use LLMs in their workflow.

Mark Clement experimented with using claude to create a voting system (front end, back end and database) in 30 minutes. He then tried using Gemini. After 4 hours he gave up. Claude installs everything for you, Gemini gives you instructions on how to install things yourself. There were version problems and it seemed like students would have a difficult time using Gemini. Eric Ringger indicated that his research indicates that Claude is a long way ahead of Gemini, Chat, Copilot in pair programming capabilities. Our recommendation is that we introduce students to the best platform available rather than pinching a penny and providing student with a difficult to use framework.

> [!NOTE]
>
> `LEE` It would be helpful to define what we mean by `Claude`. Are we talking about the LLM? The Agent architecture `Claude Code`, and IDE that uses Claude `Cursor` or `VS Code` with the Claude extension? This is going to be important as we introduce students so that they don't get lost in the hype and myriad of solutions.

> [!NOTE]
>
> `LEE` Do we understand the pricing model? For example, GitHub provides a generous education usage of Copilot that allows you to use whatever LLM you want underneath its agent workflow. This allows you to switch to the model that perform best for a specific task. Google has Antigravity (basically windsurf), with a free tier, which with their new Gemini 3 models has been highly rated. It looks like Cursor has a 1 year education plan, but after that it is $20/month.

This document includes:

1. [Recommendation](BYU_CS_Claude_Integration_Recommendation.md)
2. [Implementation Plan](BYU_CS_Implementation_Plan.md)
3. [An example project in CS 260](CS260_Assignment_Example_with_Claude.md)

The tools to multiply human output by a factor of five are already here. They require only a willingness to stop thinking of AI as an assistant and start treating it as a workforce. The programmers who make that mental leap first won't just be more productive. They'll be playing an entirely different game — and everyone else will still be typing. [Boris Cherny, creator of Claude code](https://venturebeat.com/technology/the-creator-of-claude-code-just-revealed-his-workflow-and-developers-are)

AI IDE Comparison (2026)

| Tool                 | Monthly Pricing          | Student / Educator Tier                  | Available LLMs                                      | Best Superpower                                                                                      |
| -------------------- | ------------------------ | ---------------------------------------- | --------------------------------------------------- | ---------------------------------------------------------------------------------------------------- |
| Antigravity (Google) | $0 (Preview) / $20 (Pro) | 1 Year Free Pro (via Google AI Student)  | Gemini 3 Pro/Flash, Claude 4.5 Sonnet/Opus, GPT-OSS | Mission Control: Runs multiple agents in parallel; has a built-in AI-controlled browser for testing. |
| Cursor (Anysphere)   | $20 (Pro)                | 1 Year Free Pro (via SheerID)            | Claude 4.5 Sonnet, GPT-5.2, Cursor-Small            | Tab / Composer: Best flow state; the AI predicts your next edit before you even type it.             |
| Windsurf (Codeium)   | $15 (Pro)                | Varies (Free for many university emails) | Claude 4.5 Sonnet, GPT-5.2, Codeium SWE-1           | Cascade Engine: Best at understanding massive monorepos with thousands of files.                     |
| GitHub Copilot       | $10 (Indiv)              | Forever Free (GitHub Global Campus)      | Claude 3.5/4.5 Sonnet, GPT-4o/5.2, Gemini 1.5/3 Pro | Ecosystem: Deepest integration with GitHub PRs, Actions, and Issues.                                 |
