## 🛠️ Challenge 2: Data Processing and Requests (Phase 2)

This challenge focuses on two essential pillars: dealing with **JSON** (the dominant API format) and simulating an interaction with an external service (like the K8s API).

### Scenario: Image Auditing in a Cluster

Imagine you need to simulate auditing images used in a list of *deployments* you received in JSON format from a security *scanner*.

#### 🧠 Key Concepts for this Challenge:

1.  **`json` Module**: To load and manipulate JSON data.
2.  **`requests` Module (Simulated)**: To simulate fetching data from an API.
3.  **List Comprehensions**: A *Pythonic* and concise way to build lists.

### Tasks:

1.  **Simulation Data (JSON):** Create a multiline *string* in Python (using triple quotes `"""..."""`) that represents the following JSON structure. This string simulates a response from an API listing *deployments*:

    ```json
    {
      "api_version": "apps/v1",
      "items": [
        {
          "metadata": {
            "name": "auth-service",
            "namespace": "prod"
          },
          "spec": {
            "template": {
              "spec": {
                "containers": [
                  {"name": "main", "image": "registry.corp/auth:2.5.0"},
                  {"name": "sidecar", "image": "fluentd:latest"}
                ]
              }
            }
          }
        },
        {
          "metadata": {
            "name": "web-frontend",
            "namespace": "staging"
          },
          "spec": {
            "template": {
              "spec": {
                "containers": [
                  {"name": "ui", "image": "registry.corp/frontend:1.9.1"}
                ]
              }
            }
          }
        }
      ]
    }
    ```

2.  **Loading and Processing:**

      * Use the **`json`** module to load the above *string* into a Python data structure (a *dictionary*).
      * Use **List Comprehension** (or a `for` *loop* if you prefer, but **try the *comprehension***) to iterate over all *deployments* in the `items` list.
      * For **each *deployment***, extract:
          * The *deployment* name (`metadata.name`).
          * The *namespace* (`metadata.namespace`).
          * A **list** of **all image *tags*** found in the containers (e.g., `"2.5.0"`, `"latest"`, `"1.9.1"`).

3.  **Final Output:** Print the final result clearly to the screen. The ideal format would be a list of dictionaries, where each dictionary represents a *deployment* and its images.

**Desired Output Example:**

```
Image Audit Found:
[
  {'deployment': 'auth-service', 'namespace': 'prod', 'tags': ['2.5.0', 'latest']},
  {'deployment': 'web-frontend', 'namespace': 'staging', 'tags': ['1.9.1']}
]
```

-----

This challenge forces you to navigate the structure of a nested object (like a K8s manifest), which is a daily skill in DevOps.

**Show me how you would structure your Python *script* to solve this challenge\!** I look forward to seeing your implementation\!
