## 🛠️ Desafio 3: Modelagem Orientada a Objetos (POO) para Recursos K8s

O objetivo é parar de manipular dicionários JSON crus e começar a criar **Classes** que representam nossos objetos do Kubernetes.

### Cenário: Criando Classes para Gerenciamento de Contêineres

Vamos modelar um `Container` e um `Deployment` usando Classes Python.

#### 🧠 Conceitos Chave para este Desafio:
1.  **Classes e Objetos:** Definir `class`, `__init__` (o construtor), e atributos.
2.  **Métodos:** Adicionar comportamento aos objetos.
3.  **Método `__str__`:** Para criar uma representação amigável do objeto.

### Tarefas:

1.  **Classe `Container`:**
    * Crie uma classe chamada `Container`.
    * Seu construtor (`__init__`) deve aceitar `name` (str) e `image` (str).
    * Adicione um método chamado `get_tag()` que retorna apenas a *tag* da imagem (a parte após o último `:`).
    * Implemente o método especial `__str__` para que, ao imprimir um objeto `Container`, ele retorne algo como: `"Container(name='ui', image='registry/frontend:1.9.1' -> Tag: 1.9.1)"`.

2.  **Classe `Deployment`:**
    * Crie uma classe chamada `Deployment`.
    * Seu construtor (`__init__`) deve aceitar `name` (str), `namespace` (str), e uma lista de objetos `Container` (inicialmente vazia).
    * Adicione um método chamado `add_container(container_obj)` que adiciona um objeto `Container` à lista interna do *Deployment*.
    * Adicione um método chamado `get_all_tags()` que percorre todos os contêineres associados e retorna uma **lista única** de todas as *tags* encontradas (use um `set` internamente para garantir a unicidade antes de converter para `list`, se quiser um desafio extra!).
    * Implemente o método `__str__` para que, ao imprimir um objeto `Deployment`, ele retorne algo como: `"Deployment(name='web-frontend' in ns='staging' | Containers: 1 | Tags: ['1.9.1'])"`.

3.  **Execução e Teste:**
    * Crie duas instâncias da classe `Container` baseadas nas imagens do desafio anterior (Ex: `Container("main", "registry.corp/auth:2.5.0")` e `Container("sidecar", "fluentd:latest")`).
    * Crie uma instância da classe `Deployment` chamada `auth_deploy` usando os dados do primeiro item do JSON do Desafio 2 (`auth-service`, `prod`).
    * Use o método `add_container` para adicionar os dois contêineres que você acabou de criar ao `auth_deploy`.
    * Imprima o objeto `auth_deploy` (isso deve chamar seu `__str__`).
    * Imprima o resultado de `auth_deploy.get_all_tags()`.

---

Este desafio transforma dados brutos em **modelos de código**. Isso é fundamental para usar *SDKs* como o `kubernetes-client`, onde você manipula objetos `V1Deployment`, e não apenas dicionários.

**Qual será a estrutura das suas classes `Container` e `Deployment`?** Mostre-me como você implementaria isso!