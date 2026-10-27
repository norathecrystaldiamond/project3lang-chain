# project3lang-chain
# 🤖 LangGraph 智能体状态机实战 (LangGraph State Machine Agent)

## 📖 项目简介

本项目是 AI 提效工具的**底层内核演进版本**。
在经历了单文件 `while` 循环的“屎山”折磨后，本项目采用 **LangGraph** 框架，将 AI Agent 的逻辑重构为**有向图（Graph）状态机**。通过定义明确的节点（Node）与条件边（Edge），实现了大模型思考、工具调用与流程控制的高度解耦。

## ✨ 核心架构与亮点

1. **状态机编排 (StateGraph)**：不再使用死循环，而是定义了 `AgentState` 来维护全局上下文。流程流转由图表严格管控，杜绝死循环风险。
2. **条件路由 (Conditional Edges)**：大模型思考后，程序会根据大模型的意图（是否调用了工具）自动决定下一步走向，实现动态任务编排。
3. **自定义节点扩展**：在原有的 `agent` (思考) 和 `tools` (执行) 节点之外，项目额外引入了 `translate` (后处理) 节点，展示了图架构极佳的扩展性。

### 🗺️ 节点流转图 (Graph Workflow)

```text
       [ 🚩 起点: START ]
               │
               ▼
       [ 🧠 思考节点: agent ]
               │
      (条件判断: 是否调用工具?)
               │
       ┌───────┴───────┐
       ▼ (是)          ▼ (否)
 [ 🛠️ 工具: tools ]  [ 🚧 后处理: translate ]
       │               │
       │ (循环)        │ (结束)
       └───────┐       ▼
               │  [ 🏁 终点: END ]
               ▼
         (回到思考节点)

🛠️ 环境依赖
本项目为纯 Python 命令行应用，无需前端与数据库。

bash
# 安装 LangGraph 与 LangChain 依赖
pip install langgraph langchain-openai
💻 快速运行指令
确保同级目录下存在测试文件 daily_log.txt（流水账内容）。

确保 graph_report.py 中已填入你的 DEEPSEEK_API_KEY。

在终端执行以下指令：

bash
python graph_report.py
