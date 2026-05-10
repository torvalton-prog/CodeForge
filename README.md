以下是英文版 `README.md`，直接用于 GitHub 仓库：

```markdown
<h1 align="center">⚡ CodeForge</h1>

<p align="center">
  <em>Autonomous Refactoring & Migration Agent for Large-Scale Legacy Systems</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue.svg" alt="Python">
  <img src="https://img.shields.io/badge/Async-asyncio-purple.svg" alt="Async">
  <img src="https://img.shields.io/badge/Token%20Usage-80M%2B-red.svg" alt="Token Usage">
  <img src="https://img.shields.io/badge/License-MIT-green.svg" alt="License">
</p>

---

## 📖 Overview

**CodeForge** is an LLM‑powered autonomous coding agent designed to solve the enormous cost, high risk, and low efficiency of migrating or refactoring large legacy systems (100k+ lines of code, thousands of files).

In a single task it naturally consumes **80–120 million tokens**, making it a textbook example of dense, long‑context, long‑chain reasoning coupled with massive tool‑use. By maintaining a persistent, full‑repository context and a closed‑loop "generate‑test‑repair" workflow, CodeForge achieves true hands‑off, high‑reliability, repository‑scale transformations.

---

## 🎯 Core Problems Solved

1. **Manual refactoring is astronomically expensive and fragile**  
   Cross‑file dependencies are tangled, manual rewrites take months, and subtle behavioral regressions are nearly impossible to avoid.

2. **Context fragmentation causes logical inconsistency**  
   Conventional AI assistants can only see a handful of files at a time, losing the global picture and producing interface mismatches, dead code, and other side‑effects.

3. **Testing and repair are not closed‑loop**  
   Hand‑written regression tests provide incomplete coverage, and debugging failures is so costly that quality spirals out of control.

CodeForge was engineered from the ground up to eliminate all three pain points.

---

## 🧠 Core Workflow

CodeForge follows a strict multi‑stage, long‑chain autonomous pipeline that **never drops context**:

```
Requirements Analysis → Planning → File‑by‑File Reconstruction & Verification → 
Full Regression Testing → Security & Performance Review
```

Each stage in detail:

1. **Requirements Analysis**  
   Loads the entire codebase, identifies migration constraints, modernization needs, and risk hotspots, then persists a requirement context.

2. **Planning**  
   Builds a phased refactoring order, dependency matrix, testing strategy, and rollback rules.

3. **File‑by‑File Reconstruction & Instant Verification**  
   Processes every file in dependency order through a tight inner loop:  
   `read original → LLM rewrite → write new → auto‑generate tests → run tests → on failure, backtrack & repair (up to 3 retries)`

4. **Full Regression Testing**  
   After all files are done, project‑level regression suites are executed to detect cross‑module incompatibilities; any failure triggers project‑level repair.

5. **Security & Performance Review**  
   A whole‑repository security audit and performance hotspot analysis is performed, outputting a final report.

> 💡 All intermediate outputs, failure logs, and repair records are appended to a persistent global history, so every subsequent call retains the full reasoning memory.

---

## 🚀 Key Features

- **Persistent Full Context**  
  Every LLM call carries the complete conversation history and critical artifacts since task start, consuming 40k–60k tokens per call and eliminating context fragmentation.

- **Async High‑Density Tool‑Use**  
  Built on `asyncio`, the agent executes thousands of file reads/writes and Shell commands (e.g., `pytest`) per run, with over 2000 tool invocations per task.

- **Automated Test‑Repair Loop**  
  Unit and integration tests are generated immediately after each file rewrite. Failures are automatically diagnosed, repaired, and re‑tested.

- **Extreme Token Consumption Modeling**  
  A single full‑repo refactor reliably reaches **80–120 million tokens**, exemplifying long‑chain reasoning, massive context, and iterative backtracking.

- **Dual‑Mode Operation**  
  Supports a fully simulated mode (no real filesystem or API needed) and a real‑world mode that can plug into actual codebases and CI pipelines.

---

## 📦 Installation

```bash
git clone https://github.com/yourusername/codeforge.git
cd codeforge
pip install -r requirements.txt
```

`requirements.txt` (core project uses only Python stdlib; add real API clients when needed):

```
# CodeForge currently uses only Python standard libraries.
# If you later implement real LLM / Shell integration, add:
# openai
# anthropic
# pytest
```

Requires Python 3.10+.

---

## 🧪 Quick Start

Run the demo in simulated mode (virtual token consumption, no real files):

```bash
python codeforge_autonomous_refactor_agent.py
```

You will see the full stage‑by‑stage output, token accounting per LLM call, and final total token usage.

### Tune the task scale

Edit the `AgentConfig` at the bottom of the script:

```python
config = AgentConfig(
    simulated_file_count=30,          # number of mock files
    simulated_test_fail_rate=0.25,    # probability of test failures
    total_target_tokens=80_000_000,   # target token consumption
)
```

Increase `simulated_file_count` and `simulated_shell_commands_per_file` to model even larger projects.

---

## ⚙️ Connecting to a Real Project

1. **Enable real filesystem**  
   Set `enable_real_filesystem=True` in `AgentConfig` and point `repo_path` to your legacy codebase.

2. **Enable real shell execution**  
   Set `enable_real_shell=True` – `FileManager.shell()` will then use `asyncio.create_subprocess_shell` to actually run commands.

3. **Plug in a real LLM API**  
   Replace the simulated return in `LLMClient.call()` with your own API call (OpenAI, DeepSeek, Anthropic, etc.) and implement true token counting.

---

## 🧰 Repository Structure

```
.
├── codeforge_autonomous_refactor_agent.py   # Main agent
├── README.md                                # Project documentation
└── legacy_repo/                             # Example or real legacy repo (configured by you)
```

---

## 🤝 Contributing

Issues and PRs are warmly welcomed!  
If you are working on high‑consumption, long‑context agent scenarios, feel free to share and collaborate.

---

## 📜 License

This project is open‑sourced under the MIT License. See the `LICENSE` file for details.

---

## ⭐ Acknowledgments

Inspired by the collective research community pushing the boundaries of large‑scale AI agents.  
CodeForge is a concrete step toward exploring the **"model as runtime"** paradigm.

---

<p align="center">
  <strong>⭐ Star this repo if you believe token‑heavy autonomous agents are the future</strong>
</p>
```