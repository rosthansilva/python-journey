## 🛠️ Your First Challenge (Phase 1)

To solidify the concept of modularity and data manipulation in Python, let's create a utility *script*:

### Challenge 1: Simple Configuration Generator

**Scenario:** You need to quickly generate a `.yaml` file for a new Kubernetes *deployment*, but you want the image *tag* to be dynamic and configurable.

**Tasks:**

1.  **Create a Module (`k8s_util.py`):** Define a function named `gerar_deployment_yaml(nome_app, imagem_tag, replicas=1)`.
2.  **YAML Structure:** The function must return a **string** formatted in the YAML pattern (for now, just string formatting is sufficient, without worrying about complex YAML libraries yet).
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: <nome_app>
    spec:
      replicas: <replicas>
      selector:
        matchLabels:
          app: <nome_app>
      template:
        metadata:
          labels:
            app: <nome_app>
        spec:
          containers:
          - name: app-container
            image: minha-registry/<nome_app>:<imagem_tag>
    ```
3.  **Main Script (`main.py`):**
      * Import the function from `k8s_util.py`.
      * Define variables: `app = "api-gateway"`, `tag = "v1.2.3"`, `num_replicas = 3`.
      * Call the function to get the YAML.
      * **BONUS:** Use Python's native function to **write this generated YAML to a file named `deployment_<nome_app>.yaml`**.

**Your Delivery:** The content of both files (`k8s_util.py` and `main.py`) and the result of the generated `.yaml` file.

**Tip:** To write the file in the Bonus part, use the command `with open('file_name.yaml', 'w') as f: f.write(yaml_string)`.
