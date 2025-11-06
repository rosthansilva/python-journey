## 🛠️ Desafio 2: Processamento de Dados e Requisições (Fase 2)

Este desafio foca em dois pilares essenciais: lidar com **JSON** (o formato dominante das APIs) e simular uma interação com um serviço externo (como a API do K8s).

### Cenário: Auditoria de Imagens em um Cluster

Imagine que você precisa simular a auditoria de imagens usadas em uma lista de *deployments* que você recebeu em formato JSON de um *scanner* de segurança.

#### 🧠 Conceitos Chave para este Desafio:

1.  **Módulo `json`**: Para carregar e manipular dados JSON.
2.  **Módulo `requests` (simulado)**: Para simular a obtenção de dados de uma API.
3.  **List Comprehensions**: Uma forma *pythônica* e concisa de construir listas.

### Tarefas:

1.  **Dados de Simulação (JSON):** Crie uma *string* multilinha em Python (usando aspas triplas `"""..."""`) que represente a seguinte estrutura JSON. Esta string simula uma resposta de uma API que lista *deployments*:

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

2.  **Carregamento e Processamento:**

      * Use o módulo **`json`** para carregar a *string* acima em uma estrutura de dados Python (um *dictionary*).
      * Use **List Comprehension** (ou *loop* `for` se preferir, mas **tente a *comprehension***) para iterar sobre todos os *deployments* na lista `items`.
      * Para **cada *deployment***, extraia:
          * O nome do *deployment* (`metadata.name`).
          * O *namespace* (`metadata.namespace`).
          * Uma **lista** de **todas as *tags*** de imagem encontradas nos contêineres (ex: `"2.5.0"`, `"latest"`, `"1.9.1"`).

3.  **Saída Final:** Imprima na tela, de forma clara, o resultado final. O formato ideal seria uma lista de dicionários, onde cada dicionário representa um *deployment* e suas imagens.

**Exemplo de Saída Desejada:**

```
Auditoria de Imagens Encontrada:
[
  {'deployment': 'auth-service', 'namespace': 'prod', 'tags': ['2.5.0', 'latest']},
  {'deployment': 'web-frontend', 'namespace': 'staging', 'tags': ['1.9.1']}
]
```

-----

Este desafio força você a navegar pela estrutura de um objeto aninhado (como um manifesto K8s), que é uma habilidade diária em DevOps.

**Me mostre como você estruturaria seu *script* Python para resolver este desafio\!** Estou ansioso para ver sua implementação\!