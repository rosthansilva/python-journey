## 🛠️ Seu Primeiro Desafio (Fase 1)

Para fixar o conceito de modularização e manipulação de dados em Python, vamos criar um *script* de utilidade:

### Desafio 1: Gerador de Configuração Simples

**Cenário:** Você precisa gerar rapidamente um arquivo `.yaml` para um novo *deployment* do Kubernetes, mas quer que a *tag* da imagem seja dinâmica e configurável.

**Tarefas:**

1.  **Crie um Módulo (`k8s_util.py`):** Defina uma função chamada `gerar_deployment_yaml(nome_app, imagem_tag, replicas=1)`.
2.  **Estrutura YAML:** A função deve retornar uma **string** formatada no padrão YAML (por enquanto, apenas formatação de *string* é suficiente, sem se preocupar com bibliotecas YAML complexas ainda).
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
3.  **Script Principal (`main.py`):**
      * Importe a função de `k8s_util.py`.
      * Defina variáveis: `app = "api-gateway"`, `tag = "v1.2.3"`, `num_replicas = 3`.
      * Chame a função para obter o YAML.
      * **BÔNUS:** Use a função nativa do Python para **escrever este YAML gerado em um arquivo chamado `deployment_<nome_app>.yaml`**.

**Sua Entrega:** O conteúdo dos dois arquivos (`k8s_util.py` e `main.py`) e o resultado do arquivo `.yaml` gerado.

**Dica:** Para escrever o arquivo no Bônus, use o comando `with open('nome_do_arquivo.yaml', 'w') as f: f.write(yaml_string)`.

-----