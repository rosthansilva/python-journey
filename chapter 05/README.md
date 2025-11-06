## 🛠️ Challenge 5: Building a CLI Tool (`argparse`) and K8s Client Simulation

This challenge will introduce the standard way to create command-line tools in Python and simulate the use of a real client library like the `kubernetes-client`.

### Scenario: Deployment Status Checker CLI

You need a quick tool (CLI) to check the status of a *deployment* in your cluster, receiving the name and *namespace* as command-line arguments. The tool must handle the case where the *deployment* does not exist.

#### 🧠 Key Concepts for this Challenge:

1.  **`argparse` Module**: The standard way in Python to create CLIs, processing arguments like `--name` or `-n`.
2.  **Service Classes (OOP):** Structuring interaction logic with K8s in a dedicated class.
3.  **Specific Exception Handling:** Simulating the capture of common errors, like "Not Found" (`404`), using custom exceptions.

### Tasks:

1.  **Custom Exception:**

      * Define a simple exception class named `DeploymentNotFound` at the top of your *script*. (This simulates the exception that a K8s library would raise for a 404 error).

    <!-- end list -->

    ```python
    class DeploymentNotFound(Exception):
        pass
    ```

2.  **`K8sService` Class (The API Wrapper):**

      * Create a class named `K8sService` to encapsulate the Kubernetes logic.
      * Add a method called `get_deployment_status(namespace, name)`:
          * Inside this method, implement the following **simulation logic**:
              * If the `name` is **`deployment-erro`** or the `namespace` is **`ns-nao-existe`**, **raise** the `DeploymentNotFound` exception.
              * Otherwise, return a dictionary simulating a success *status*: `{"replicas": 5, "ready_replicas": 5, "status": "Ready"}`.

3.  **Main Function (`main()` with `argparse`):**

      * Use the **`argparse`** module to create an argument *parser*.
      * Define two **required** arguments:
          * `--namespace` (or `-n`), with `help='The namespace of the deployment.'`.
          * `--name` (or `-d`), with `help='The name of the deployment.'`.
      * In the body of your `main()` function:
          * Parse the arguments.
          * Create an instance of `K8sService`.
          * Use a **`try...except`** block to:
              * Call `service.get_deployment_status(...)`.
              * **On success (in the `try` block):** Print the deployment *status* clearly and friendly.
              * **Catch the `DeploymentNotFound` exception:** Print a specific and useful error message to the user, indicating which *deployment* was not found.

-----

### How to Test (Terminal Simulation):

Your code should work similarly to these commands (you can simulate this execution in your head or using the command line):

1.  **Success:** `python my_script.py -n prod -d api-gateway`
2.  **Failure (Deployment Not Found):** `python my_script.py -n staging -d deployment-erro`
3.  **Failure (Namespace Not Found):** `python my_script.py -n ns-nao-existe -d algum-deployment`

**What will the structure of your `verificador_k8s.py` script be?** I look forward to seeing how you handle the command-line interface\!