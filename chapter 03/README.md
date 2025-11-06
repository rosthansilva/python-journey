## 🛠️ Challenge 3: Object-Oriented Modeling (OOP) for K8s Resources

The goal is to stop manipulating raw JSON dictionaries and start creating **Classes** that represent our Kubernetes objects.

### Scenario: Creating Classes for Container Management

Let's model a `Container` and a `Deployment` using Python Classes.

#### 🧠 Key Concepts for this Challenge:
1.  **Classes and Objects:** Defining `class`, `__init__` (the constructor), and attributes.
2.  **Methods:** Adding behavior to objects.
3.  **`__str__` Method:** To create a friendly representation of the object.

### Tasks:

1.  **`Container` Class:**
    * Create a class named `Container`.
    * Its constructor (`__init__`) must accept `name` (str) and `image` (str).
    * Add a method called `get_tag()` that returns only the image *tag* (the part after the last `:`).
    * Implement the special method `__str__` so that when printing a `Container` object, it returns something like: `"Container(name='ui', image='registry/frontend:1.9.1' -> Tag: 1.9.1)"`.

2.  **`Deployment` Class:**
    * Create a class named `Deployment`.
    * Its constructor (`__init__`) must accept `name` (str), `namespace` (str), and a list of `Container` objects (initially empty).
    * Add a method called `add_container(container_obj)` that adds a `Container` object to the *Deployment*'s internal list.
    * Add a method called `get_all_tags()` that iterates over all associated containers and returns a **unique list** of all found *tags* (use a `set` internally to ensure uniqueness before converting to `list`, if you want an extra challenge!).
    * Implement the `__str__` method so that when printing a `Deployment` object, it returns something like: `"Deployment(name='web-frontend' in ns='staging' | Containers: 1 | Tags: ['1.9.1'])"`.

3.  **Execution and Testing:**
    * Create two instances of the `Container` class based on the images from the previous challenge (e.g., `Container("main", "registry.corp/auth:2.5.0")` and `Container("sidecar", "fluentd:latest")`).
    * Create an instance of the `Deployment` class called `auth_deploy` using the data from the first JSON item of Challenge 2 (`auth-service`, `prod`).
    * Use the `add_container` method to add the two containers you just created to `auth_deploy`.
    * Print the `auth_deploy` object (this should call your `__str__`).
    * Print the result of `auth_deploy.get_all_tags()`.

-----