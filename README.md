# 🐍 Python Power-Up for DevOps: K8s & Dagger 🚀

Welcome to my accelerated learning repository\! This space contains practical *scripts* and projects developed to solidify my knowledge in Python, with a direct focus on automating **DevOps** tasks, utilizing tools like **Docker**, **Kubernetes**, and **Dagger** on my **macOS/Colima** environment.

This repository follows a structured progression, transforming basic Python knowledge into infrastructure engineering tools.

-----

## ✨ Journey Roadmap

Our journey has been divided into stages focused on practical application:

### Phase 1: Python Foundation

  \* **Focus:** Modularity and basic logic.
  \* **Challenge 1:** Creating reusable *scripts* with dynamic YAML generation for K8s.

### Phase 2: Infrastructure Connection

  \* **Focus:** Complex data manipulation and resource modeling.
  \* **Challenge 2:** Processing nested JSON (simulating K8s API *output*) using List Comprehensions.
  \* **Challenge 3:** Modeling resources (Container, Deployment) using **Object-Oriented Programming (OOP)**.

### Phase 3: Automation and External Execution

  \* **Focus:** Interacting with the *shell* and building command-line tools.
  \* **Challenge 4:** Using the **`subprocess`** module to execute `docker` commands and *parsing* table output.
  \* **Challenge 5:** Building a **Professional CLI** using **`argparse`** and simulated service classes to interact with the K8s API.

### Phase 4: Production and Persistence

  \* **Focus:** Refining tools with structured *logging* and external configuration.
  \* **Final Challenge:** Integrating structured **`logging`** and managing persistent state using **`configparser`** to save user settings (`~/.devops_util.ini`).

### Phase 5: Pipeline-as-Code

  \* **Focus:** Orchestrating *builds* and tests natively in Python.
  \* **Challenge 6:** Defining a complete CI/CD *pipeline* (`build`, `test`, `publish`) using the **Dagger SDK** in **asynchronous** code.

(([https://www.google.com/search?q=https://img.icons8.com/color/48/000000/python.png](https://www.google.com/search?q=https://img.icons8.com/color/48/000000/python.png))) | (([https://www.google.com/search?q=https://img.icons8.com/external-those-icons-lineal-colour/48/external.png](https://www.google.com/search?q=https://img.icons8.com/external-those-icons-lineal-colour/48/external.png))) | (([https://www.google.com/search?q=https://img.icons8.com/fluency/48/docker.png](https://www.google.com/search?q=https://img.icons8.com/fluency/48/docker.png)))

-----

## 📂 Structure and Execution

The *scripts* are named to reflect the challenge they address.

| Example File | Main Focus | Requirements |
| :--- | :--- | :--- |
| `k8s_util.py` | YAML Generation | Basic Python |
| `data_processor.py` | JSON Parsing, OOP | `json` module |
| `k8s_manager_cli.py` | Robust CLI, Logging, Config | `argparse`, `logging`, `configparser` |
| `dagger_pipeline.py` | Pipeline-as-Code | Dagger SDK, `asyncio` |

### Example Execution (CLI with Persistence - Final Challenge):

The CLI saves your preferred *namespace* in your `$HOME`, ensuring automation is *stateful*.

```bash
# 1. First run: Creates ~/.devops_util.ini with 'namespace=staging'
python k8s_manager_cli.py -d api-gateway 
# INFO:root:Default namespace loaded: staging

# 2. Override and config update
python k8s_manager_cli.py -n production -d auth-service
# INFO:root:Namespace updated and persisted to: production

# 3. Rerun without arguments (uses persisted value)
python k8s_manager_cli.py -d web-frontend
# INFO:root:Default namespace loaded: production
```

-----

## 🎯 Next Steps (Mentoring)

The foundation for DevOps *scripting* is complete\! The next step would be to delve deeper into:

1.  **Concurrency in Python:** Utilizing `asyncio` to optimize *scripts* that make multiple K8s/Cloud calls in parallel.
2.  **Unit Testing:** Applying `unittest` or `pytest` to your *scripts* and classes (like `Container` and `K8sService`).
3.  **Real K8s Interaction:** Replacing the `K8sService` simulation with the official **`kubernetes-client`** to interact with your Colima cluster.

-----