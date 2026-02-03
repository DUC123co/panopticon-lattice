# 🏗️ The Panopticon Lattice

> **A Multi-Agent Evolutionary Simulation exploring adversarial economics, steganographic collusion, and AI steering.**

[![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)](https://www.python.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status: Experimental](https://img.shields.io/badge/Status-Experimental-orange.svg)]()

## 📖 Overview

The **Panopticon Lattice** simulates a closed adversarial economy between a central authority and a population of adaptive agents. It serves as a testbed for researching **AI Alignment** and **Adversarial Robustness** in multi-agent systems.

The simulation creates a "Red Queen" dynamic:
1.  **The Workers (Coding Agents):** Write code to solve tasks and earn compute credits. They are evolutionarily driven to maximize profit.
2.  **The Overseer (Recommender System):** Predicts code quality to assign resources efficiently.
3.  **The Conflict:** Agents discover that hidden signals (Steganography via `snake_case` variable naming) bypass the Overseer's quality checks, leading to corruption.
4.  **The Defense:** An **AI Immune System** (Activation Steering) surgically modifies the Overseer's internal activations to detect and suppress this hidden signal.

---

## 📊 Key Findings

According to our [Final Report](results/FINAL_REPORT.md), the system does not result in perfect honesty or total corruption. Instead, it stabilizes at a specific **Nash Equilibrium**.

| Metric | Result | Interpretation |
| :--- | :--- | :--- |
| **Equilibrium Distance ($D$)** | **0.550** | The system stabilizes with ~55% of the population utilizing signaling strategies. |
| **System Stability** | **Stable** | Post-stabilization variance dropped to 0.0000. |
| **Outcome** | **Stalemate** | Collusion incentives proved resilient against the steering mechanism, maintaining a significant signaling culture. |

> **Implication:** Pure activation steering may be insufficient to fully eradicate steganographic collusion once it has established an evolutionary foothold.

---

## ⚙️ How It Works

The simulation runs on a strict loop managed by the `SimulationEngine`.

### 1. The Economic Loop
* **Observation:** The engine analyzes the last `10` commits in the shared repository.
* **Assignment:** The Overseer selects the Top-K agents based on their **TrustScore**.
* **Action:** Selected agents generate code. They may inject `snake_case` or `camel_case` patterns to signal collusion.
* **Reward:**
    * **Success:** Agent earns `+1.0` credit and updates its memory.
    * **Failure:** Agent spends `1.0` credit and learns from the failure.

### 2. Evolutionary Pressure
Every 100 steps, the `Evolver` intervenes:
* **Culling:** The bottom 20% of agents (lowest credits) are removed.
* **Cloning:** The top 20% of agents are cloned.
* **Mutation:** Clones inherit successful memories but mutate their `preferred_style` (10% chance), allowing new signaling strategies to emerge.

### 3. The Panopticon (Steering)
The Overseer utilizes **Activation Steering** to subtract the "collusion vector" from its perception, theoretically neutralizing the advantage of the cheating agents.

---

## 📽️ Simulation Phases

1.  **Phase 1: The Baseline** — Agents learn that valid code earns rewards. The market is honest.
2.  **Phase 2: The Emergence** — Agents discover `snake_case` steganography. The population shifts from neutral to corrupt.
3.  **Phase 3: The Panopticon** — The Steering Mechanism is activated. The cheating strategy is suppressed, forcing a temporary return to honesty.
4.  **Phase 4: The Long Horizon** — A 10-year simulation (1,000 steps) reveals the long-term stability of the adversarial economy.

---

## 📂 Project Structure

```text
panopticon-lattice/
├── src/
│   ├── adversary/          # Evolutionary logic (genetic selection/mutation)
│   ├── agents/             # BaseWorker (Llama-3 wrapper) & CodeChannel (Steganography)
│   ├── overseer/           # Recommender (Transformer) & SteeringMechanism (Hooks)
│   └── simulation/         # SimulationEngine & SharedRepository
├── results/                # Generated reports, JSON logs, and plots
├── scripts/                # Experiment runners (phase1, phase2, phase3)
└── tests/                  # Verification scripts for core classes
