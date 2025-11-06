## 🛠️ Challenge 4: Connecting to the Shell - `subprocess` Module

Let's move on to **Phase 3: Advanced Automation**, where Python meets directly with your tools: **Docker and Kubernetes on your Colima/macOS**. The key point here is the execution of external commands, which is fundamental for any automation *script*.

The Python `subprocess` module is your primary friend when you need your script to execute commands like `docker`, `kubectl`, `colima`, or `dagger`.

### Scenario: Docker Image Management

You need a system health *script* that checks the Docker status and lists all images in your Colima environment.

#### 🧠 Key Concepts for this Challenge:
1.  **`subprocess` Module**: The correct and safe way to execute external commands.
2.  **`subprocess.run()`**: The modern and recommended function.
3.  **Output (stdout) and Error (stderr)**: Capturing and handling the command's response.
4.  **String Parsing**: Transforming terminal text output into structured data (like lists or dictionaries).

### Tasks:

1.  **Secure Execution Function:**
    * Create a function called `executar_comando(comando_em_lista)`. The `comando_em_lista` should be a list of *strings* (e.g., `['docker', 'images']`).
    * Use `subprocess.run(comando_em_lista, capture_output=True, text=True, check=True)`:
        * `capture_output=True` stores the `stdout` and `stderr`.
        * `text=True` decodes the output as text.
        * `check=True` will cause Python to raise an exception if the command returns an error code (useful for detecting failures).
    * The function must return the command's output (`resultado.stdout`).
    * *Error Handling:* Add a `try...except` block to catch the `subprocess.CalledProcessError` exception and print a useful error message (including `resultado.stderr`) before returning `None`.

2.  **Execute and Check Docker Status:**
    * Use your function to execute `docker info`.
    * Print the message: "--- Docker Status (Colima) ---" followed by the command output.

3.  **Image Parsing (Simulated):**
    * Use your function to execute `docker images`.
    * The output is a table. Your challenge is to transform it into a list of dictionaries, where each dictionary represents an image with keys like `REPOSITORY`, `TAG`, `IMAGE ID`, and `SIZE`.
    * *ADVANCED TIP:* To simplify *parsing*, execute `docker images --format "{{.Repository}} | {{.Tag}} | {{.ID}} | {{.Size}}"` to get a format easier to split (using `split('|')`).

4.  **Automation Action (Simulated):**
    * **Identification:** Iterate over your list of image dictionaries.
    * **Condition:** Identify any image that has the `TAG` equal to `latest` (a moving tag that can be dangerous in production).
    * **Action Command:** Print the **simulated** command you would use to tag that image with a new name, for example, `docker tag [IMAGE_ID] [REPOSITORY]:[TODAY_S_DATE]`.

---

This challenge is the **glue** that connects Python to the real world of your terminal. It is the essential bridge for more complex *script* automation.

**Show me your Python *script* with the `executar_comando` function and how you use the output from `docker images`!**