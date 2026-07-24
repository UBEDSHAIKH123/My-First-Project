# Multi-Agent System for APT Testing

A project demonstrating a **Multi-Agent System (MAS)** designed to perform **Automated Performance Testing (APT)** across distributed components.

---

## Overview

This project implements a multi-agent architecture where autonomous agents collaborate to plan, execute, and report on automated performance tests. Each agent is responsible for a specific role in the testing pipeline, enabling parallel execution, scalability, and intelligent test orchestration.

---

## What is a Multi-Agent System?

A Multi-Agent System (MAS) is a system composed of multiple interacting intelligent agents. Each agent:

- Operates autonomously within its designated scope
- Communicates with other agents via a shared message bus or API
- Makes decisions based on its local observations and shared state
- Contributes to a collective goal — in this case, comprehensive APT testing

---

## What is APT Testing?

**Automated Performance Testing (APT)** is the practice of automatically validating that a system meets its performance requirements (e.g., response time, throughput, resource utilization) without manual intervention. This includes:

- **Load Testing** – Simulating expected user traffic
- **Stress Testing** – Pushing the system beyond normal capacity
- **Spike Testing** – Sudden bursts of high load
- **Endurance Testing** – Sustained load over a long period
- **Scalability Testing** – Measuring how performance changes as load increases

---

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│                    Orchestrator Agent                   │
│   - Schedules and coordinates all testing agents        │
│   - Aggregates results and generates reports            │
└──────────────┬──────────────────────────┬───────────────┘
               │                          │
     ┌─────────▼──────────┐   ┌───────────▼────────────┐
     │   Load Generator   │   │   Monitor Agent        │
     │   Agent            │   │                        │
     │ - Spawns virtual   │   │ - Collects CPU, memory,│
     │   users            │   │   latency, error rate  │
     │ - Sends HTTP/API   │   │ - Streams metrics to   │
     │   requests         │   │   Orchestrator         │
     └─────────┬──────────┘   └───────────┬────────────┘
               │                          │
     ┌─────────▼──────────────────────────▼────────────┐
     │                  Target System                   │
     │          (Application Under Test)                │
     └──────────────────────────────────────────────────┘
               │
     ┌─────────▼──────────┐
     │   Reporter Agent   │
     │ - Parses metrics   │
     │ - Generates HTML / │
     │   JSON reports     │
     │ - Sends alerts on  │
     │   threshold breach │
     └────────────────────┘
```

---

## Agents

| Agent | Responsibility |
|---|---|
| **Orchestrator Agent** | Coordinates all agents, manages test lifecycle, aggregates results |
| **Load Generator Agent** | Generates synthetic traffic (virtual users, API calls) against the target system |
| **Monitor Agent** | Collects real-time performance metrics (latency, throughput, CPU, memory) |
| **Reporter Agent** | Parses collected metrics, produces reports, and raises alerts on SLA breaches |

---

## How It Works

1. **Configuration** – Define test scenarios (load profile, endpoints, thresholds) in a config file.
2. **Initialization** – The Orchestrator Agent starts all sub-agents and distributes the test plan.
3. **Execution** – The Load Generator Agent sends requests; the Monitor Agent continuously collects metrics.
4. **Analysis** – The Orchestrator Agent correlates results and checks against defined SLAs.
5. **Reporting** – The Reporter Agent produces a detailed performance report (HTML/JSON/CSV).

---

## Getting Started

### Prerequisites

- Python 3.9+
- A running instance of the application under test

### Installation

```bash
git clone https://github.com/UBEDSHAIKH123/My-First-Project.git
cd My-First-Project
pip install -r requirements.txt
```

### Running Tests

```bash
python orchestrator.py --config test_config.yaml
```

### Example Configuration (`test_config.yaml`)

```yaml
target_url: "http://localhost:8080"
test_type: load
duration_seconds: 60
virtual_users: 50
ramp_up_seconds: 10
thresholds:
  max_response_time_ms: 500
  error_rate_percent: 1
```

---

## Output

After a test run, the Reporter Agent generates:

- `report.html` – Visual charts for response time, throughput, and error rate
- `report.json` – Machine-readable metrics for CI/CD integration
- Console summary with pass/fail status against defined thresholds

---

## Project Structure

```
My-First-Project/
├── agents/
│   ├── orchestrator.py      # Orchestrator Agent
│   ├── load_generator.py    # Load Generator Agent
│   ├── monitor.py           # Monitor Agent
│   └── reporter.py          # Reporter Agent
├── config/
│   └── test_config.yaml     # Default test configuration
├── reports/                 # Generated test reports
├── tests/                   # Unit and integration tests
├── requirements.txt
└── README.md
```

---

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/my-feature`)
3. Commit your changes (`git commit -m "Add my feature"`)
4. Push to the branch (`git push origin feature/my-feature`)
5. Open a Pull Request

---

## License

This project is licensed under the MIT License.
