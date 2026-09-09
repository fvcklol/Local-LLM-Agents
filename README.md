# 🧠 Local LLM Agents

> **A fully local multi-agent AI system where specialized LLMs work together to solve complex tasks.**

**Local LLM Agents** is an open-source project designed to run AI agents directly on your own machine.

Instead of using a single LLM for everything, the system uses a **Main LLM** as an orchestrator. Every user request goes through the Main LLM, which decides whether it can answer the request itself or whether the task should be delegated to specialized agents.

## 🤖 Architecture

```text
                         ┌─────────────────┐
                         │      USER       │
                         └────────┬────────┘
                                  │
                                  ▼
                    ┌─────────────────────────┐
                    │       MAIN LLM          │
                    │      Orchestrator       │
                    │                         │
                    │ Understands the request │
                    │ and decides what to do   │
                    └────────────┬────────────┘
                                 │
                    ┌────────────┴────────────┐
                    │                         │
              Simple Request            Complex Request
                    │                         │
                    ▼                         ▼
             ┌─────────────┐        ┌─────────────────┐
             │ Main LLM    │        │   Planner LLM   │
             │ Responds    │        │  Breaks task    │
             └─────────────┘        │   into steps    │
                                    └────────┬────────┘
                                             │
                              ┌──────────────┼──────────────┐
                              │              │              │
                              ▼              ▼              ▼
                       ┌───────────┐  ┌───────────┐  ┌───────────┐
                       │ Coder LLM │  │ Tester LLM │  │ Other LLM │
                       │           │  │           │  │  Agents   │
                       └─────┬─────┘  └─────┬─────┘  └─────┬─────┘
                             │              │              │
                             └──────────────┼──────────────┘
                                            ▼
                                  ┌──────────────────┐
                                  │   Main LLM       │
                                  │ Reviews Results  │
                                  │ & Coordinates    │
                                  └────────┬─────────┘
                                           │
                                           ▼
                                    ┌─────────────┐
                                    │    USER     │
                                    │   Response  │
                                    └─────────────┘
```

## 🧩 How It Works

Every request starts with the **Main LLM**.

### 1. User sends a request

For example:

> "What is the capital of France?"

The Main LLM determines that this is a simple question and answers it directly.

```text
User
 ↓
Main LLM
 ↓
Simple question
 ↓
Answer
```

### 2. Complex requests are delegated

For example:

> "Build me a Python application that monitors my files and sends notifications when they change."

The Main LLM recognizes that this requires multiple steps.

Instead of trying to do everything itself, it sends the task to the **Planner LLM**.

```text
User
 ↓
Main LLM
 ↓
Complex task
 ↓
Planner LLM
```

### 3. Planner breaks the task down

The Planner LLM creates a structured plan.

```text
Task
 │
 ├── 1. Design application
 ├── 2. Write Python code
 ├── 3. Implement file monitoring
 ├── 4. Implement notifications
 ├── 5. Test the application
 └── 6. Fix discovered issues
```

### 4. Specialized agents execute the work

Different agents can handle different parts of the task.

**Coder LLM**

Writes and modifies code.

**Tester LLM**

Tests the generated code and looks for errors.

**Planner LLM**

Breaks complex problems into smaller tasks and coordinates the workflow.

**Main LLM**

Acts as the central orchestrator, deciding what happens next and producing the final response.

Additional specialized agents can be added as the project grows.

## 🔄 Agent Workflow

A complex task can therefore follow a workflow like:

```text
USER
 │
 ▼
MAIN LLM
 │
 ▼
PLANNER LLM
 │
 ├──────► CODER LLM
 │              │
 │              ▼
 │         Generated Code
 │              │
 │              ▼
 └──────► TESTER LLM
                │
          ┌─────┴─────┐
          │           │
        PASS         FAIL
          │           │
          │           ▼
          │      CODER LLM
          │           │
          │           ▼
          │      Fixed Code
          │
          ▼
      MAIN LLM
          │
          ▼
        USER
```

This allows agents to **specialize instead of forcing one model to perform every role**.

## 🏠 Fully Local

The goal of this project is to keep the entire agent system running locally.

```text
┌───────────────────────────────────────────┐
│              YOUR COMPUTER               │
│                                           │
│  ┌─────────────┐                          │
│  │  Main LLM   │                          │
│  └──────┬──────┘                          │
│         │                                  │
│  ┌──────┴─────────────────────────────┐   │
│  │                                    │   │
│  ▼          ▼           ▼             ▼   │
│ Planner   Coder       Tester       Other │
│   LLM       LLM         LLM        Agents│
│                                           │
└───────────────────────────────────────────┘
```

No expensive cloud AI API is required by the architecture.

Your models run on **your hardware**, giving you control over the models, data, and agent system.

## ✨ Key Features

* 🧠 **Central Main LLM** — Handles every incoming request.
* 🎯 **Intelligent routing** — Simple requests can be answered directly.
* 🧩 **Task decomposition** — Complex requests are passed to a Planner LLM.
* 💻 **Specialized coding agent** — Handles software development tasks.
* 🧪 **Testing agent** — Tests generated work and detects problems.
* 🔄 **Agent collaboration** — Agents can pass results between each other.
* 🏠 **Local execution** — Designed for local LLMs.
* 🆓 **Open source** — Free to modify and extend.
* 🔐 **Privacy focused** — Data can remain entirely on your machine.
* ➕ **Extensible** — Add new specialized agents for new tasks.

## 🧠 Why Multiple LLMs?

A single LLM can perform many different tasks, but specialized agents allow the system to separate responsibilities.

Instead of:

```text
One LLM
   │
   ├── Planning
   ├── Coding
   ├── Testing
   ├── Research
   └── Everything else
```

The system aims for:

```text
                 MAIN LLM
                /    |    \
               /     |     \
          Planner  Coder  Research
              │      │       │
              └──────┼───────┘
                     │
                   Tester
```

Each agent can have its own **model, system prompt, tools, context, and responsibilities**.

## 🚧 Project Status

This project is currently under development.

The architecture is designed to evolve into a flexible local AI framework where new agents can be added without rebuilding the entire system.

### Planned Agents

* [x] Main / Orchestrator LLM
* [ ] Planner LLM
* [ ] Coder LLM
* [ ] Tester LLM
* [ ] Researcher LLM
* [ ] Reviewer LLM
* [ ] Documentation LLM
* [ ] Custom user-defined agents

## 🎯 Vision

The long-term goal is to create a **local AI workforce** where different AI agents collaborate to solve problems.

Instead of asking one AI to do everything:

> **One AI coordinates.
> Specialized AIs execute.
> The system works together.**

## 🤝 Contributing

Contributions are welcome!

If you want to create a new agent, improve the orchestration system, optimize local inference, or experiment with new workflows, feel free to contribute.

1. Fork the repository
2. Create a branch
3. Make your changes
4. Test your changes
5. Open a Pull Request

## ⭐ Support

If you like the project, consider giving it a ⭐ on GitHub.

It helps the project get discovered by other developers interested in **local LLMs and multi-agent AI systems**.

---

<p align="center">
  <b>🧠 One system. Multiple agents. Completely local.</b>
</p>
