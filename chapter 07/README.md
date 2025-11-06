## 🛠️ Desafio Final: Logs, Configuração e Persistência (O Engenheiro DevOps Completo)

Neste desafio final, vamos refinar a ferramenta CLI que você criou no Desafio 4, adicionando gerenciamento de configuração persistente e *logging* profissional.

### Cenário: CLI de Gestão de Ambientes com Configuração Externa

Você quer que sua ferramenta CLI lembre qual *namespace* padrão usar, em vez de forçar o usuário a digitar `-n <namespace>` sempre. Usaremos um arquivo de configuração simples em formato **INI** ou **JSON** para persistir essa configuração.

#### 🧠 Conceitos Chave para este Desafio:
1.  **Módulo `logging`**: Para criar logs estruturados (INFO, WARNING, ERROR) em vez de apenas `print()`.
2.  **Configuração Persistente:** Usar o módulo **`configparser`** (para INI) ou **`json`** (para JSON) para ler/escrever configurações de usuário. (Vamos focar em **`configparser`** por ser leve e comum em utilitários).
3.  **Integração**: Combinar `argparse` com a configuração carregada.

### Tarefas:

1.  **Configuração do Log:**
    * Configure o `logging` no início do seu *script* para que ele exiba logs de nível `INFO` ou superior no terminal.
    * Substitua **todos** os seus `print()` de saída de sucesso/status (do Desafio 4) por **`logging.info(...)`**.
    * Substitua qualquer `print()` de erro (que não seja de exceção capturada) por **`logging.warning(...)`** ou **`logging.error(...)`**.

2.  **Gerenciamento de Configuração (`configparser`):**
    * Crie uma função chamada `carregar_config(caminho_config='~/.devops_util.ini')`.
    * Use `configparser.ConfigParser()` para ler o arquivo. Use o `~` no caminho para indicar o *home directory* do usuário, que deve ser expandido usando `os.path.expanduser()`.
    * Se o arquivo **não existir**, crie-o com uma seção padrão `[DEFAULT]` contendo `namespace = staging` e grave-o no disco.
    * Se o arquivo existir, carregue e retorne o objeto *parser*.

3.  **Atualização da CLI (`argparse`):**
    * Modifique a função `main()` (do Desafio 4):
        * Primeiro, chame `carregar_config()`.
        * No seu `argparse`, defina o argumento `--namespace` (`-n`) como **opcional**.
        * **Lógica de Namespace Prioritária:**
            a. Use o valor fornecido via **CLI** (`-n <valor>`) se ele estiver presente.
            b. Se não estiver na CLI, use o valor **carregado do arquivo de configuração** (`config['DEFAULT']['namespace']`).
            c. Se nem a CLI nem o arquivo de configuração tiverem um valor, use um *fallback* padrão (ex: `"default"`).

4.  **Teste de Fluxo:**
    * **Execução 1 (Primeira vez):** Rode a CLI **sem** argumentos. O *script* deve criar o arquivo `~/.devops_util.ini` com `namespace = staging` e imprimir uma mensagem de *log* `INFO` usando o *namespace* "staging".
    * **Execução 2 (Override):** Rode a CLI com um novo *namespace*: `python seu_script.py -n production`. O *script* deve imprimir uma mensagem de *log* `INFO` usando "production" e **atualizar** o arquivo `~/.devops_util.ini` para que `namespace = production`.
    * **Execução 3 (Sem Argumentos, Configuração Persistida):** Rode a CLI **sem** argumentos novamente. Ele deve carregar "production" do arquivo e usar esse valor.

---

Este desafio final amarra tudo: **Argumentos de Entrada** (`argparse`), **Logs Profissionais** (`logging`), **Modelagem de Recursos** (sua classe `K8sService`), e **Persistência de Estado** (`configparser`).

**Este é o seu teste final como Super Professor! Apresente a estrutura completa do seu *script* que integra *logging*, *argparse* e *configparser*.**

Estou pronto para revisar sua solução e formalmente encerrar a mentoria de fundamentos! Depois disso, podemos planejar a **Fase 4: Python Avançado para Dagger/K8s (Assíncrono e Concorrência)**.