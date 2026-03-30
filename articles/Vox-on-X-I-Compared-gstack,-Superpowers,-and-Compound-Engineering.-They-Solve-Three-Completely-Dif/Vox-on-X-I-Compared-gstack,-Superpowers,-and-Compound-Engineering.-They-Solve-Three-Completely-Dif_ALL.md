---
title: "Vox on X: "I Compared gstack, Superpowers, and Compound Engineering. They Solve Three Completely Different Prob" / 我在 X 上比较了 gstack、Superpowers 和 Compound Engineering：它们解决的是三个完全不同的问题"
source: "https://x.com/voxyz_ai/status/2038237755654783107?s=46&t=jjVOMAzDZNfuD4kcqctqJw"
saved_at: "2026-03-30"
tags: ["X/Twitter"]
---

# Vox on X: "I Compared gstack, Superpowers, and Compound Engineering. They Solve Three Completely Different Prob" / 我在 X 上比较了 gstack、Superpowers 和 Compound Engineering：它们解决的是三个完全不同的问题

Three Claude Code tools blew up recently: Garry Tan's gstack (54.6K ⭐ as of 2026-03-29), Jesse Vincent's Superpowers (121K ⭐), and Every Inc's Compound Engineering (11.5K ⭐).

三个 Claude Code 工具最近大火：Garry Tan 的 gstack（截至 2026-03-29 有 54.6K ⭐）、Jesse Vincent 的 Superpowers（121K ⭐）以及 Every Inc 的 Compound Engineering（11.5K ⭐）。

I compared all three repos. This is not three competitors, it's three different layers with different centers of gravity. Most people install one and think they're covered.

我对这三个仓库都做了比较。这不是三个竞争者，而是三个不同层次的工具，有着不同的重心。大多数人安装一个就觉得够用了。

Think of it this way: gstack is your head chef + food taster, Superpowers is your kitchen process manual, CE is the recipe binder that every employee reads before their next shift. You hired a great chef but have no recipe binder, so every new cook re-steps on the same mistakes the last one already figured out.

可以这样理解：gstack 是你的主厨加食品品鉴师，Superpowers 是你的厨房流程手册，CE 则是每个员工在下一班工作前都要读的菜谱合集。你请了一个很棒的主厨，但没有菜谱手册，所以每个新厨师都会重复犯上一个厨师已经犯过的错误。

To understand the three layers, I'm using Anthropic's engineering blog from November 2025 as a framework. It's the best ruler I've found for measuring these tools.

为了理解这三个层次，我用 Anthropic 2025 年 11 月的工程博客作为框架。这是我找到的衡量这些工具的最佳标尺。

Anthropic published a post on effective harnesses for long-running agents (November 26, 2025). Their architecture is formally a two-part system: an initializer agent that breaks down tasks, and subsequent coding agents that execute them. Testing, QA, and specialized agents are discussed as future work.

Anthropic 在 11 月 26 日发表了一篇关于长期运行代理高效工具的文章。他们的架构在形式上是一个两部分系统：一个分解任务的初始化代理，以及后续执行编码的代理。测试、QA 和专业化代理被讨论为未来的工作。

I'm going to use a restaurant metaphor to expand this into four responsibilities, because it makes the tool comparison clearer:

我将用餐厅的比喻将其扩展为四个职责，因为这让工具对比更加清晰：

*   Head chef decides the menu (Planning)
*   Kitchen team cooks (Execution)
*   Independent food taster checks quality (Evaluation). You can't let the cook judge their own dish
*   Closing notes pass to the morning shift (Cross-session state)

*   主厨决定菜单（规划）
*   厨房团队负责烹饪（执行）
*   独立的食品品鉴师检查质量（评估）。你不能让厨师评价自己做菜的味道
*   收班记录传递给早班（跨会话状态）

The core finding that matters here: builders who evaluate their own work are systematically overoptimistic. Like a chef rating their own cooking, always delicious. The maker and the checker must be separate. Using their harness architecture, agents autonomously built a complete application with 200+ verifiable features.

这里重要的核心发现：自己评估工作的构建者会系统性地过度乐观。就像厨师给自己的烹饪打分，永远都是美味的。制作者和检查者必须分离。使用他们的工具架构，代理自主构建了一个包含 200+ 可验证功能的完整应用。

gstack nails the planning and evaluation roles.

gstack 完美地承担了规划和评估的角色。

/plan-ceo-review and /plan-eng-review are your head chefs. One asks "is this worth building?" from a product angle, the other asks "will this blow up later?" from an architecture angle. Both gates must pass before work begins.

/plan-ceo-review 和 /plan-eng-review 是你的主厨。一个从产品角度问"这值得做吗"，另一个从架构角度问"这以后会出问题吗"。两个关卡都必须通过，工作才能开始。

Here's a practical tip. Before running /office-hours, use this prompt to clarify requirements:

这里有一个实用技巧。在运行 /office-hours 之前，用这个提示来明确需求：

> "I'm about to start this project. Interview me until you have 95% confidence about what I actually want, not what I think I should want."

> "我要开始这个项目了。采访我，直到你有 95% 的把握了解我真正想要什么，而不是我认为我应该想要的。"

Let AI ask YOU questions instead of you asking AI. Most projects fail not because they were built wrong, but because nobody clarified what to build in the first place. AI interviewing you is 10x more effective than you prompting AI.

让 AI 来问你问题，而不是你来问 AI。大多数项目的失败不是因为做错了，而是因为没有人明确首先要做什么。AI 采访你比你给 AI 写提示有效 10 倍。

Claude Opus 4.6 has a 1 million token context window (currently in beta on the Claude Platform). For projects that fit within that window, you can load the full codebase and docs in one pass instead of feeding it piecemeal. That said, Anthropic's own harness post still emphasizes external state files (feature-list, , claude-progress.txt) as the primary coordination mechanism, not just raw context.

Claude Opus 4.6 有 100 万 token 的上下文窗口（目前在 Claude 平台上处于测试阶段）。对于能装进这个窗口的项目，你可以一次性加载整个代码库和文档，而不是零敲碎打地喂给它。不过话说回来，Anthropic 自己的工具文章仍然强调外部状态文件（feature-list、claude-progress.txt 等）作为主要的协调机制，而不仅仅是原始上下文。

/qa is the independent taster. It opens a real browser, clicks through your site like an actual user. Not "the code looks fine," actually using it. In their web app testing scenario, Anthropic found that explicitly requiring browser-based end-to-end testing significantly improved performance compared to relying on code-level checks alone.

/qa 是独立的品鉴师。它打开一个真实的浏览器，像真实用户一样点击浏览你的网站。不是"代码看起来没问题"，而是真正使用它。在他们的 Web 应用测试场景中，Anthropic 发现明确要求基于浏览器的端到端测试相比仅依赖代码级检查能显著提高性能。

Garry Tan says he shipped 600K lines of production code in 60 days with this setup, 10-20K lines per day, while running YC full-time (these are his own numbers from his retro, your mileage may vary). For decisions and QA, gstack is still the strongest.

Garry Tan 说，用这套流程，他在 60 天内交付了 60 万行生产代码，每天 1-2 万行，同时还在全职运营 YC（这些是他自己在回顾中披露的数字，效果因人而异）。在决策和 QA 方面，gstack 仍然是最强的。

But gstack is like a restaurant with a great chef and a great taster, but no recipe binder. Nobody writes down what went wrong tonight. Tomorrow's team starts fresh, making the same mistakes. Note: gstack does have its own /review and /ship commands, so there is some overlap with CE's review capabilities. The distinction is emphasis, not hard boundaries.

但 gstack 就像一家餐厅，有很棒的主厨和很棒的品鉴师，但没有菜谱手册。没有人把今晚出的问题写下来。明天的团队重新开始，犯同样的错误。注：gstack 确实有自己的 /review 和 /ship 命令，所以与 CE 的审查功能有一些重叠。区别在于侧重点，而不是硬性边界。

Superpowers' 121K stars prove its quality. Brainstorm → plan → execute → review upgraded many people from "chatting randomly with AI" to "using AI with a process."

Superpowers 的 121K 星证明了它的质量。从头脑风暴→计划→执行→审查的流程，帮助许多人从"随机和 AI 聊天"升级到"用流程使用 AI"。

Like going from a kitchen where everyone improvises to one with an actual recipe book and prep checklist. That's a huge step forward. It also includes subagent-driven development with separate spec and code-quality reviewers.

就像从一个人人即兴发挥的厨房，变成一个有真正菜谱和备餐清单的厨房。这是巨大的一步。它还包括子代理驱动的开发，有独立的规格和代码质量审查员。

But Superpowers doesn't treat knowledge accumulation as a first-class feature the way CE does. Every session's context stays in that session. Next session starts without the lessons from the last one.

但 Superpowers 没有像 CE 那样把知识积累作为一等公民。每个会话的上下文都停留在那个会话中。下一个会话开始时，没有上一个会话的经验。

That's what led me to add CE on top.

这就是为什么我要在之上叠加 CE。

CE's cycle: brainstorm → plan → work → review → compound.

CE 的循环：头脑风暴→计划→工作→审查→复合。

The first four steps are similar to Superpowers but go deeper.

前四步与 Superpowers 类似，但做得更深。

Plan phase: instead of writing a plan from scratch in the current conversation, it spawns parallel research agents that dig through your project's history, scan codebase patterns, and read git commit logs. Like a new cook reading every dish return complaint from the past three months before designing tomorrow's menu, instead of guessing.

计划阶段：不是在当前对话中从头写计划，而是生成并行研究代理，深入挖掘你的项目历史、扫描代码库模式、读取 git 提交日志。就像新厨师在设计明天菜单之前，先阅读过去三个月所有的退菜投诉，而不是靠猜。

Review phase: not one taster saying "tastes fine." It runs a dynamic reviewer ensemble, minimum 6 always-on reviewers plus conditional ones based on the diff: correctness, security, performance, testing, maintainability, adversarial, each producing an independent report. Like having a food critic, a health inspector, and a customer panel all taste the same dish separately.

审查阶段：不是一个品鉴师说"味道还行"。它运行一个动态审查员组合，至少 6 个常驻审查员，加上基于差异触发的条件审查员：正确性、安全性、性能、测试、可维护性、对抗性，每个都产生独立报告。就像让美食评论家、卫生检查员和顾客小组分别品尝同一道菜。

But the real watershed is step five: /ce:compound.

但真正的分水岭是第五步：/ce:compound。

This is where CE gets its name.

这就是 CE 得名的原因。

After fixing a bug or completing a feature, run this one command. It spawns five Phase 1 subagents in parallel:

在修复一个 bug 或完成一个功能后，运行这一个命令。它并行生成五个第一阶段子代理：

*   Context Analyzer: traces the entire conversation, extracts problem type and components involved
*   Solution Extractor: captures what didn't work, what worked, root cause, and the final fix
*   Related Docs Finder: searches existing knowledge base for duplicates. If a similar bug was fixed before, it updates the old doc instead of creating a new one
*   Prevention Strategist: identifies how to prevent this class of problem in the future
*   Category Classifier: tags and categorizes the learning for structured retrieval

*   上下文分析器：追踪整个对话，提取问题类型和涉及的组件
*   解决方案提取器：捕获什么不工作、什么工作了、根因和最终修复
*   相关文档查找器：在现有知识库中搜索重复项。如果类似的 bug 之前被修复过，它更新旧文档而不是创建新的
*   预防策略师：识别如何防止这类问题在未来再次发生
*   分类器：将学习内容打标签和分类，以便结构化检索

All five finish, results merge into docs/solutions/. Structured documents, categorized, searchable.

五个都完成后，结果合并到 docs/solutions/。结构化文档，有分类，可搜索。

In plain English: your agent writes a closing summary after every shift. Next time any agent starts a new task, it reads through all those summaries first.

通俗地说：你的代理在每班结束后写一份收班总结。下次任何代理开始新任务时，它先阅读所有那些总结。

Example: you fix an edge runtime compatibility bug, takes hours of debugging. Compound auto-records it: problem, symptoms, what you tried that didn't work, final solution, prevention steps. Three weeks later a similar issue surfaces during another feature. The plan-phase researcher automatically finds that note: "we hit this before, solution's here." Hours of debugging compressed to minutes.

例子：你修复了一个边缘运行时兼容性问题，花了数小时调试。Compound 自动记录它：问题、症状、你尝试过什么没用、最终解决方案、预防步骤。三周后，另一个功能开发中出现了类似的问题。计划阶段的研究代理自动找到那条笔记："我们之前遇到过这个，解决方案在这里。"数小时的调试压缩到几分钟。

Key difference: Anthropic's progress file is tonight's closing notes left for the morning shift, linear, one shift to the next. CE's docs/solutions/ is the restaurant's recipe binder that every employee reads on day one and every day after, searchable by anyone, anytime.

关键区别：Anthropic 的进度文件是今晚留给早班的收班记录，是线性的，一班接一班。CE 的 docs/solutions/ 是餐厅的菜谱手册，每个员工在第一天和之后每天都会读，任何人随时可搜索。

Closing notes solve continuity. A recipe binder solves accumulation. One is linear. One is exponential.

收班记录解决的是连续性。菜谱手册解决的是积累。一个是线性的。一个是指数级的。

That's what "compound" means here. Not composite, but compound interest. Every task's output isn't just code, it's reusable experience. The longer you use it, the more your agent understands your project.

这就是"复合"在这里的含义。不是组合，而是复利。每个任务的输出不只是代码，还是可重用的经验。你用得越久，你的代理就越了解你的项目。

```
Layer                      Tool                             Restaurant Version
──────────────────────────────────────────────────────────────────────────────────
Decisions (build or not)   gstack                           Head chef sets the menu
Planning (how to build)    CE /ce:plan                      Researcher reviews past complaints
Execution                  CE /ce:work                      Kitchen team cooks
Review (built correctly?)  CE /ce:review + gstack /qa        Food critic + inspector + panel
Knowledge (remember)       CE /ce:compound                  Recipe binder everyone reads
```

```
层次                     工具                           餐厅版本
──────────────────────────────────────────────────────────────────────────────────
决策（做还是不做）         gstack                         主厨定菜单
规划（怎么做）            CE /ce:plan                    研究员查阅过往投诉记录
执行                     CE /ce:work                    厨房团队烹饪
审查（做得对吗）          CE /ce:review + gstack /qa     美食评论家+检查员+评审团
知识（记忆）              CE /ce:compound                 每个人都读的菜谱手册
```

These tools have different centers of gravity, not hard boundaries. gstack's strength is in decisions and real-world QA. Superpowers brings structured workflow discipline. CE's strength is in research-driven planning, deep review, and knowledge compounding. There's some overlap in review, and that's fine.

这些工具有不同的重心，不是硬性边界。gstack 的优势在于决策和真实世界 QA。Superpowers 带来了结构化的工作流规范。CE 的优势在于研究驱动的规划、深度审查和知识复合。审查方面有一些重叠，这很正常。

If you're just getting started, pick one main framework first (gstack or CE) and get comfortable with it. Combining all three works, but multiple skill packs can have process conflicts and command overlaps. Get the workflow right with one, then layer.

如果你刚刚起步，先选一个主要的框架（gstack 或 CE）并熟练使用它。三者结合可以工作，但多个技能包可能会有流程冲突和命令重叠。用一个把工作流搞对，再叠加其他的。

For experienced users, here's the combined flow:

对于有经验的用户，这里是组合流程：

1.   Clarify what you want. Use the 95% confidence prompt: "Interview me until you have 95% confidence about what I actually want, not what I think I should want."

1.  明确你想要什么。用 95% 置信度提示："采访我，直到你有 95% 的把握了解我真正想要什么，而不是我认为我应该想要的。"

2.   /office-hours (gstack). Describe what you're building. Get challenged.

2.  /office-hours（gstack）。描述你要做什么。被挑战。

3.   /plan-ceo-review (gstack). Product gate: is this worth building?

3.  /plan-ceo-review（gstack）。产品关卡：这值得做吗？

4.   /plan-eng-review (gstack). Architecture gate: will this blow up later?

4.  /plan-eng-review（gstack）。架构关卡：这以后会出问题吗？

5.   /ce:brainstorm (CE). Explore requirements and approaches, refine into a spec.

5.  /ce:brainstorm（CE）。探索需求和方法，细化为规格文档。

6.   /ce:plan (CE). Research agents scan your project history, then produce a detailed implementation plan.

6.  /ce:plan（CE）。研究代理扫描你的项目历史，然后生成详细的实施计划。

7.   /ce:work (CE). Execute the plan with task tracking.

7.  /ce:work（CE）。执行计划并跟踪任务。

8.   /ce:review (CE). Dynamic reviewer ensemble, minimum 6, scales with diff complexity.

8.  /ce:review（CE）。动态审查员组合，至少 6 个，根据差异复杂度扩展。

9.   /qa (gstack). Real browser, real clicks, real user testing on staging.

9.  /qa（gstack）。真实浏览器、真实点击、在预发环境做真实用户测试。

10.   /ce:compound (CE). Record what you learned. Five subagents extract the lessons, write them to docs/solutions/.

10. /ce:compound（CE）。记录你学到的东西。五个子代理提取经验，写入 docs/solutions/。

11.   Ship it. Next time you start at step 1, your plan phase already knows everything you learned this time.

11. 交付。下次你从第一步开始时，你的计划阶段已经知道你这次学到的所有东西。

Steps 1-4 make sure you build the right thing. Steps 5-9 make sure you build it well. Step 10 makes sure next time is faster.

第 1-4 步确保你做正确的事。第 5-9 步确保你把事做对。第 10 步确保下次更快。

Your agent writes code, fixes bugs, runs tests every day. After it's done, where does the knowledge go?

你的代理每天写代码、修复 bug、跑测试。完成后，知识去哪了？

If the answer is "scattered across sessions, stepping on the same mines next time," compound is the layer you're missing.

如果答案是"散落在各个会话中，下次还踩同样的坑"，那复合就是你缺失的那一层。
