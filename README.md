# 🐍 Python Power-Up para DevOps: K8s & Dagger 🚀

Bem-vindo ao meu repositório de aprendizado acelerado\! Este espaço contém *scripts* e projetos práticos desenvolvidos para solidificar meu conhecimento em Python, com um foco direto na automação de tarefas de **DevOps**, utilizando ferramentas como **Docker**, **Kubernetes** e **Dagger** no meu ambiente **macOS/Colima**.

Este repositório segue uma progressão estruturada, transformando conhecimentos básicos de Python em ferramentas de engenharia de infraestrutura.

-----

## ✨ Roteiro da Jornada de Aprendizado

Nossa jornada foi dividida em etapas focadas na aplicação prática:

### Fase 1: Alicerce Python

  * **Foco:** Modularização e lógica básica.
  * **Desafio 1:** Criação de *scripts* reutilizáveis com geração dinâmica de YAML para K8s.

### Fase 2: Conexão com Infraestrutura

  * **Foco:** Manipulação de dados complexos e modelagem de recursos.
  * **Desafio 2:** Processamento de JSON aninhado (simulando *output* de API K8s) usando List Comprehensions.
  * **Desafio 3:** Modelagem de recursos (Container, Deployment) usando **Orientação a Objetos (POO)**.

### Fase 3: Automação e Execução Externa

  * **Foco:** Interagir com o *shell* e construir ferramentas de linha de comando.
  * **Desafio 4:** Uso do módulo **`subprocess`** para executar comandos `docker` e *parsing* de saída de tabelas.
  * **Desafio 5:** Construção de uma **CLI profissional** usando **`argparse`** e classes de serviço simuladas para interagir com a API K8s.

### Fase 4: Produção e Persistência

  * **Foco:** Refinamento de ferramentas com *logging* e configuração externa.
  * **Desafio Final:** Integração de **`logging`** estruturado e gerenciamento de estado persistente usando **`configparser`** para salvar configurações do usuário (`~/.devops_util.ini`).

### Fase 5: Pipeline-as-Code

  * **Foco:** Orquestração de *builds* e testes nativamente em Python.
  * **Desafio 6:** Definição de um *pipeline* CI/CD completo (`build`, `test`, `publish`) utilizando o **Dagger SDK** em código **assíncrono**.

([https://img.icons8.com/color/48/000000/python.png](https://www.google.com/search?q=https://img.icons8.com/color/48/000000/python.png)) | ([https://img.icons8.com/external-those-icons-lineal-colour/48/external.png](https://www.google.com/search?q=https://img.icons8.com/external-those-icons-lineal-colour/48/external.png)) | ([https://img.icons8.com/fluency/48/docker.png](https://www.google.com/search?q=https://img.icons8.com/fluency/48/docker.png))

-----

## 📂 Estrutura e Execução

Os *scripts* são nomeados de forma a refletir o desafio que abordam.

| Arquivo Exemplo | Foco Principal | Requisitos |
| :--- | :--- | :--- |
| `k8s_util.py` | Geração de YAML | Básico Python |
| `data_processor.py` | JSON Parsing, POO | Módulo `json` |
| `k8s_manager_cli.py` | CLI robusta, Logging, Config | `argparse`, `logging`, `configparser` |
| `dagger_pipeline.py` | Pipeline-as-Code | Dagger SDK, `asyncio` |

### Exemplo de Execução (CLI com Persistência - Desafio Final):

A CLI salva sua preferência de *namespace* no seu `$HOME`, garantindo que a automação seja *stateful*.

```bash
# 1. Primeira execução: Cria ~/.devops_util.ini com 'namespace=staging'
python k8s_manager_cli.py -d api-gateway 
# INFO:root:Namespace padrão carregado: staging

# 2. Override e atualização da config
python k8s_manager_cli.py -n production -d auth-service
# INFO:root:Namespace atualizado e persistido para: production

# 3. Reexecução sem argumentos (usa o valor persistido)
python k8s_manager_cli.py -d web-frontend
# INFO:root:Namespace padrão carregado: production
```

-----

## 🎯 Próximos Passos (Mentoria)

A base de *scripting* para automação DevOps está completa\! O próximo passo seria aprofundar em:

1.  **Concorrência em Python:** Utilizar `asyncio` para otimizar *scripts* que fazem múltiplas chamadas K8s/Cloud em paralelo.
2.  **Testes Unitários:** Aplicar `unittest` ou `pytest` aos seus *scripts* e classes (como `Container` e `K8sService`).
3.  **Interação Real com K8s:** Substituir a simulação do `K8sService` pelo cliente oficial **`kubernetes-client`** para interagir com seu cluster Colima.