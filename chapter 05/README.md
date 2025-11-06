## 🛠️ Desafio 5: Construindo uma Ferramenta CLI (`argparse`) e Simulação K8s Client

Este desafio irá introduzir a maneira padrão de criar ferramentas de linha de comando em Python e simular o uso de uma biblioteca cliente real como o `kubernetes-client`.

### Cenário: Verificador de Status de Deployment CLI

Você precisa de uma ferramenta rápida (CLI) para verificar o status de um *deployment* no seu cluster, recebendo o nome e o *namespace* como argumentos de linha de comando. A ferramenta deve lidar com o caso em que o *deployment* não existe.

#### 🧠 Conceitos Chave para este Desafio:

1.  **Módulo `argparse`**: A forma padrão em Python para criar CLIs, processando argumentos como `--name` ou `-n`.
2.  **Classes de Serviço (OOP):** Estruturar a lógica de interação com o K8s em uma classe dedicada.
3.  **Tratamento de Exceções Específicas:** Simular a captura de erros comuns, como "Not Found" (`404`), usando exceções personalizadas.

### Tarefas:

1.  **Exceção Personalizada:**

      * Defina uma classe de exceção simples chamada `DeploymentNotFound` no topo do seu *script*. (Isto simula a exceção que uma biblioteca K8s levantaria para um erro 404).

    <!-- end list -->

    ```python
    class DeploymentNotFound(Exception):
        pass
    ```

2.  **Classe `K8sService` (O Wrapper da API):**

      * Crie uma classe chamada `K8sService` para encapsular a lógica do Kubernetes.
      * Adicione um método chamado `get_deployment_status(namespace, name)`:
          * Dentro deste método, implemente a seguinte **lógica de simulação**:
              * Se o `name` for **`deployment-erro`** ou o `namespace` for **`ns-nao-existe`**, **levante** a exceção `DeploymentNotFound`.
              * Caso contrário, retorne um dicionário simulando um *status* de sucesso: `{"replicas": 5, "ready_replicas": 5, "status": "Ready"}`.

3.  **Função Principal (`main()` com `argparse`):**

      * Use o módulo **`argparse`** para criar um *parser* de argumentos.
      * Defina dois argumentos **obrigatórios**:
          * `--namespace` (ou `-n`), com `help='O namespace do deployment.'`.
          * `--name` (ou `-d`), com `help='O nome do deployment.'`.
      * No corpo da sua função `main()`:
          * Parse os argumentos.
          * Crie uma instância de `K8sService`.
          * Use um bloco **`try...except`** para:
              * Chamar `service.get_deployment_status(...)`.
              * **Em caso de sucesso (bloco `try`):** Imprima o status do *deployment* de forma clara e amigável.
              * **Capturar a exceção `DeploymentNotFound`:** Imprima uma mensagem de erro específica e útil para o usuário, indicando qual *deployment* não foi encontrado.

-----

### Como Testar (Simulação do Terminal):

Seu código deve funcionar de forma semelhante a estes comandos (você pode simular esta execução na sua cabeça ou usando a linha de comando):

1.  **Sucesso:** `python meu_script.py -n prod -d api-gateway`
2.  **Falha (Deployment Não Encontrado):** `python meu_script.py -n staging -d deployment-erro`
3.  **Falha (Namespace Não Encontrado):** `python meu_script.py -n ns-nao-existe -d algum-deployment`

**Qual será a estrutura do seu *script* `verificador_k8s.py`?** Estou ansioso para ver como você lida com a interface de linha de comando\!