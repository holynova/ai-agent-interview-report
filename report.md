# 程序员面试 AI Agent 开发岗位：近 30 天题目与要求报告

生成日期：2026-07-09  
调研窗口：2026-06-09 至 2026-07-09  
调研方式：last30days v3.9.4，覆盖 Reddit、X、Hacker News、GitHub，并补充 WebSearch 来源。

原始数据文件：
`~/Documents/Last30Days/ai-agent-developer-interview-questions-and-requirements-for-programmer-roles-raw-v3.md`

交互版 HTML：
`index.html` 包含每道题的折叠式参考答案、搜索、分类筛选、展开全部和收起全部。答案已去掉重复模板，改为题目自身答案加少量具体回答要点和相关技术术语。

## 核心结论

AI Agent 开发岗位的面试重点已经从“会调 LLM API”转向“能把 agent 系统稳定、安全、可评估、可观测地跑到生产”。近 30 天的讨论和岗位材料显示，候选人需要同时证明三类能力：

1. 扎实的软件工程能力：Python、后端 API、异步、数据库、Docker、CI/CD、测试、云部署、可观测性。
2. LLM 应用工程能力：prompt、structured output、function calling、RAG、reranking、上下文管理、模型选择。
3. Agent 工程能力：LangGraph / CrewAI / AutoGen / OpenAI Agents SDK / MCP、工具调用、状态、记忆、多 agent 编排、evals、guardrails、成本控制、human-in-the-loop。

传统 DSA 没有完全消失，但不再是主战场。近期 r/LangChain 讨论显示，很多 Agentic AI / AI Engineer 面试仍会问基础字符串、数组、hash map 和简单逻辑题，但核心区分度来自系统设计、agentic system design、生产复盘、eval 和调试能力。

GitHub GH-600 Agentic AI Developer 认证是一个重要信号。官方考试域覆盖 agent architecture / SDLC、tool use、memory / state / execution、evaluation / error analysis / tuning、multi-agent coordination、guardrails / accountability。这与近期岗位和面试题高度一致。

## 面试流程画像

常见流程正在形成：

1. Recruiter / Hiring Manager screen：确认是否真正做过 LLM 或 agent 项目，是否上线到真实用户。
2. 技术 screen：通常 45-60 分钟，偏 reasoning，不一定现场写复杂算法。
3. AI assessment 或 take-home：常见为 2-4 小时，要求构建一个 RAG-plus-agent、小型工具调用 agent、agentic QA service，且必须带 eval。
4. 系统设计：设计客服 agent、SOC agent、多租户 external data QA、multi-agent workflow、agent observability。
5. Take-home walkthrough：解释架构、tradeoffs、失败模式、测试、成本、下一步改进。
6. Bar raiser / CTO / senior loop：问生产经验、业务约束、安全边界、成本控制、团队协作。

## 岗位要求分类

### 1. 软件工程基础

- Python 是最低门槛，TypeScript / Node 在 web agent 和 MCP 场景也常见。
- 后端 API、REST、async、队列、数据库建模、auth、multi-tenant SaaS。
- Docker、CI/CD、测试、Git、cloud deployment。
- 可观测性、日志、tracing、metrics、canary、rollback。

### 2. LLM 与 RAG

- Tokens、sampling、temperature、context window、structured output。
- Embedding、chunking、hybrid search、reranking、citation grounding。
- RAG hallucination control、retrieval eval、LLM-as-a-judge。
- 模型选择：大模型、小模型、SLM、router、成本和延迟权衡。

### 3. Agent 架构

- ReAct、planner-executor、graph workflow、state machine。
- LangGraph、LangChain、CrewAI、AutoGen、OpenAI Agents SDK、Pydantic AI。
- Single agent + tools 和 multi-agent swarm 的取舍。
- 状态、记忆、执行恢复、trajectory replay。

### 4. 工具调用与 MCP

- Function calling / tool calling schema 设计。
- Tool permission、sandbox、rate limit、retry、fallback。
- MCP server、MCP Inspector、tool discovery、tool environment interaction。
- Agent Firewall、工具安全边界、高风险操作 human approval。

### 5. Evals、Observability 与 LLMOps

- Final answer eval 不够，要评估 trajectory、tool choice、unnecessary steps、context adherence。
- LangSmith、Langfuse、OpenTelemetry、custom traces。
- Golden dataset、regression eval、online monitoring。
- 成本预算、token budget、termination condition、session-level spend tracking。

### 6. Guardrails 与安全

- Prompt injection、data exfiltration、越权工具调用。
- Policy layer、pre-tool guard、post-generation validation。
- Human-in-the-loop escalation。
- Audit logging、compliance、sensitive data handling。

## 高频具体题目池

### A. 基础定义与岗位理解

1. 什么是 AI agent？它和普通 LLM chain 的区别是什么？
2. 什么样的系统不应该做成 agent？
3. Agentic AI Engineer 和传统 ML Engineer 的区别是什么？
4. 一个 agent 系统除了 LLM 还需要哪些组件？
5. 什么时候用简单 workflow，什么时候用 autonomous agent？
6. 你做过哪个 LLM / agent 系统上线？真实用户规模是多少？
7. 你怎么解释“AI Engineering 是 10% AI、90% software”？
8. AI agent 的 autonomy boundary 怎么定义？
9. 一个系统“看起来像 agent”但其实不是 agent 的例子是什么？
10. 你如何向非技术 stakeholder 解释 agent 的风险？

### B. 系统设计与架构

11. 设计一个客服 agent，能查订单、退款、升级人工。
12. 设计一个 SOC 安全分析 agent，能读告警、查日志、建议处置。
13. 设计一个多租户 “answer over external data” 系统。
14. 设计一个 agentic QA service，要求调用 live APIs。
15. 什么时候使用 ReAct，什么时候使用 planner-executor？
16. 什么时候使用 LangGraph，什么时候用简单 chain？
17. 怎么防止 agent over-planning 或陷入循环？
18. 怎么设计 termination conditions？
19. 如何拆分 planner、executor、critic、tool agent？
20. 单 agent + 多工具和 multi-agent swarm 怎么取舍？
21. 什么时候 multi-agent 会带来更多复杂度而不是收益？
22. 如何设计长任务 agent 的 checkpoint 和 resume？
23. 如何处理用户输入不完整但 agent 必须继续的问题？
24. 如何设计一个 agent 的权限模型？
25. 如何做 model routing？

### C. RAG 与检索

26. 如何处理金融 RAG pipeline 的 hallucination？
27. 如何判断 RAG 检索失败是 embedding、chunking、reranking 还是 prompt 问题？
28. 什么时候用 vector search，什么时候用 keyword / hybrid search？
29. chunk size 和 overlap 怎么选？
30. 如何做 citation grounding？
31. 如何评估 retrieval quality？
32. 如何防止模型引用没有出现在 context 里的信息？
33. 如何设计 RAG 的 fallback 策略？
34. 如何处理 freshness 与缓存？
35. 如何让 RAG 支持权限隔离？
36. 如何处理多文档冲突？
37. 如何减少 context stuffing？

### D. 工具调用、MCP 与环境交互

38. 一个 tool schema 应该怎么设计？
39. 怎么处理 tool call 参数错误？
40. 怎么防止 agent 调错工具？
41. MCP server 在 agent 系统中解决什么问题？
42. 如何调试 MCP server？
43. 怎么给工具设置权限边界？
44. 工具调用失败要 retry、fallback 还是升级人工？
45. 怎么避免 “God Agent” 拿到过多工具导致可靠性下降？
46. 如何处理工具返回部分成功？
47. 如何在工具调用前做 policy check？
48. 如何记录工具调用审计日志？
49. 如何防止 agent 连续调用昂贵工具？

### E. Memory、State 与上下文

50. memory 和 state 的区别是什么？
51. LangGraph 里的 state 应该保存什么，不应该保存什么？
52. 长对话里怎么做 context management？
53. 什么时候需要长期记忆，什么时候只需要短期 state？
54. 怎么避免 memory 污染？
55. agent 执行中断后如何恢复？
56. 如何记录 trajectory 以便 replay 和 debug？
57. 如何处理用户偏好和业务事实的冲突？
58. 如何给 memory 设置 TTL 或信任级别？
59. 如何测试 memory 是否提高了质量？

### F. Evaluation 与 Observability

60. Agentic system 的 accuracy 怎么算？
61. 为什么 final answer accuracy 不够？
62. 如何做 trajectory evaluation？
63. 如何评估 tool selection quality？
64. 如何评估 unnecessary steps？
65. 如何设计 LLM-as-a-judge？
66. 如何构建 golden dataset？
67. 如何做 regression eval？
68. LangSmith / Langfuse / tracing 你怎么用？
69. 生产中发现 agent drift，你怎么定位？
70. 你会监控哪些指标：latency、cost、tool error、loop count、refusal、fallback？
71. 如何评估一个 agent 是否遵守安全边界？
72. 如何做线上 A/B 或 shadow eval？

### G. 安全、Guardrails 与合规

73. 如何防 prompt injection？
74. 用户要求越权操作时 agent 应该怎么做？
75. guardrail 应该放在 prompt、tool layer、policy layer 还是 post-processing？
76. 什么时候需要 human-in-the-loop？
77. 如何记录安全边界触发和人工升级？
78. 如何限制 agent 的文件、网络、数据库权限？
79. 如何防止敏感数据进入 prompt 或 logs？
80. 如何测试 agent firewall / policy enforcement？
81. 如何处理 tool output 中的恶意指令？
82. 如何设计审批流？

### H. 成本、性能与可靠性

83. 如何控制 multi-agent 系统成本？
84. 如何选择模型：大模型、小模型、SLM、router？
85. 哪些步骤可以 deterministic，哪些必须交给 LLM？
86. 怎么减少 token spend？
87. 怎么处理 rate limit？
88. 怎么做 caching？
89. agent 延迟过高时怎么优化？
90. tool call 或模型调用失败时怎么设计 retry policy？
91. 怎么做 canary release？
92. 怎么判断一个 agent 可以上生产？
93. 如何处理 runaway tool calls？
94. 如何处理 agent stuck in loop？

### I. Take-home 常见方向

95. 构建一个带 eval 的 RAG-plus-agent 小应用。
96. 构建一个能调用外部 API 的 agentic QA service。
97. 构建一个客服 / sales / support agent，并解释 handoff。
98. 给一个失败 agent trace，找出为什么循环或调错工具。
99. 给一个业务场景，选择 chain、workflow、single agent 或 multi-agent。
100. 为一个 agent 系统写 eval rubric 和测试集。
101. 设计一个安全工具调用层，限制高风险操作。
102. 展示一个 agent 项目，讲清楚 tradeoffs、失败模式、成本和监控。

## 回答框架

回答这类问题时，最稳的结构是：

1. 先定义边界：这个系统是否真的需要 agent。
2. 再讲架构：workflow / agent / graph / multi-agent 的选择。
3. 再讲失败模式：loop、tool error、hallucination、context drift、cost spike。
4. 再讲 eval：final output、trajectory、tool choice、safety、cost。
5. 再讲生产化：observability、guardrails、human escalation、rollback。

## 准备优先级

1. 准备两个真实项目故事：一个 RAG，另一个 tool-using agent。
2. 每个项目都写清楚：目标、架构、工具、状态、eval、失败、成本、监控、上线指标。
3. 手写一个最小 agent：不靠框架，实现 tool registry、planner loop、structured output、retry、trace。
4. 再用 LangGraph 或类似框架重做一遍，说明框架解决了什么问题，也带来了什么复杂度。
5. 做一份 eval harness：至少包括 golden cases、LLM judge rubric、trajectory inspection、regression test。

## 调研来源摘要

- last30days 引擎：18 个 Reddit threads、20 条 X posts、13 个 HN stories、13 个 GitHub items。
- WebSearch 补充：Reddit r/AI_Agents 42 题帖、AY Automate 2026 AI Engineer interview guide、Microsoft Learn GH-600 官方认证、GitHub Community GH-600 discussion、r/GithubCopilot GH-600 candidate thread、Agentic Engineering Jobs interview guide、Exponent LangChain interview guide、Dataford Adobe Agentic AI Engineer guide、近期 LangGraph / MCP / evals 岗位材料、LinkedIn 面试趋势帖。
