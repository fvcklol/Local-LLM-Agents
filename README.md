# Local LLM Agents

Local LLM Agents is an open-source project that lets you run multiple LLM agents locally on your own device.

The idea is simple: instead of having one LLM do everything, there is a main LLM that handles the user's request and decides what needs to be done.

For simple questions, the main LLM answers directly.

For more complicated tasks, it can split the task between different LLMs, such as:

* **Planner** — plans what needs to be done
* **Coder** — writes the code
* **Tester** — tests the result
* **Reviewer** — checks the work
* **Main LLM** — manages everything and gives the final response

### Example

```text
User
 ↓
Main LLM
 ↓
Is it simple?
 ├── Yes → Answer
 │
 └── No
      ↓
    Planner
      ↓
   ┌──┴───┐
 Coder  Tester
   │       │
   └───┬───┘
       ↓
   Main LLM
       ↓
     User
```

The project is designed to run **locally and for free**, without requiring paid AI APIs.

## Goals

* Run LLMs locally
* Make it easy to create different agents
* Let agents work together
* Keep the system simple and customizable
* Avoid unnecessary API costs

## Status

🚧 **Work in progress**

More agents and features will be added over time.

## License

Open source.
