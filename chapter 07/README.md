## 🛠️ Final Challenge: Logs, Configuration, and Persistence (The Complete DevOps Engineer)

In this final challenge, we will refine the CLI tool you created in Challenge 4 by adding persistent configuration management and professional *logging*.

### Scenario: Environment Management CLI with External Configuration

You want your CLI tool to remember which default *namespace* to use, instead of forcing the user to always type `-n <namespace>`. We will use a simple **INI** or **JSON** format file to persist this configuration.

#### 🧠 Key Concepts for this Challenge:
1.  **`logging` Module**: To create structured logs (INFO, WARNING, ERROR) instead of just `print()`.
2.  **Persistent Configuration**: Using the **`configparser`** module (for INI) or **`json`** module (for JSON) to read/write user configurations. (We will focus on **`configparser`** as it is lightweight and common in utility *scripts*).
3.  **Integration**: Combining `argparse` with the loaded configuration.

### Tasks:

1.  **Log Configuration:**
    * Configure `logging` at the beginning of your *script* so that it displays logs of level `INFO` or higher on the terminal.
    * Replace **all** your success/status `print()` statements (from Challenge 4) with **`logging.info(...)`**.
    * Replace any error `print()` (that is not caught by an exception) with **`logging.warning(...)`** or **`logging.error(...)`**.

2.  **Configuration Management (`configparser`):**
    * Create a function called `load_config(config_path='~/.devops_util.ini')`.
    * Use `configparser.ConfigParser()` to read the file. Use the `~` in the path to indicate the user's *home directory*, which should be expanded using `os.path.expanduser()`.
    * If the file **does not exist**, create it with a default section `[DEFAULT]` containing `namespace = staging` and write it to disk.
    * If the file exists, load and return the *parser* object.

3.  **CLI Update (`argparse`):**
    * Modify the `main()` function (from Challenge 4):
        * First, call `load_config()`.
        * In your `argparse`, define the `--namespace` (`-n`) argument as **optional**.
        * **Namespace Priority Logic:**
            * a. Use the value provided via the **CLI** (`-n <value>`) if it is present.
            * b. If not in the CLI, use the value **loaded from the configuration file** (`config['DEFAULT']['namespace']`).
            * c. If neither the CLI nor the configuration file has a value, use a default *fallback* (e.g., `"default"`).

4.  **Flow Test:**
    * **Run 1 (First time):** Run the CLI **without** arguments. The *script* must create the file `~/.devops_util.ini` with `namespace = staging` and print an `INFO` *log* message using the "staging" *namespace*.
    * **Run 2 (Override):** Run the CLI with a new *namespace*: `python your_script.py -n production`. The *script* must print an `INFO` *log* message using "production" and **update** the file `~/.devops_util.ini` so that `namespace = production`.
    * **Run 3 (No Arguments, Persisted Config):** Run the CLI **without** arguments again. It must load "production" from the file and use that value.

-----

This final challenge ties everything together: **Input Arguments** (`argparse`), **Professional Logs** (`logging`), **Resource Modeling** (your `K8sService` class), and **State Persistence** (`configparser`).

**This is your final test as Super Mentor! Present the complete structure of your *script* that integrates *logging*, *argparse*, and *configparser*.**

I am ready to review your solution and formally conclude the fundamentals mentorship! After that, we can plan for **Phase 4: Advanced Python for Dagger/K8s (Asynchronous and Concurrency)**.
