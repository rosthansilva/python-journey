## 🛠️ Desafio 4: A Conexão com o Shell - Módulo `subprocess`

Vamos agora para a **Fase 3: Automação Avançada**, onde o Python se encontra diretamente com suas ferramentas: **Docker e Kubernetes no seu Colima/macOS**. O ponto-chave aqui é a execução de comandos externos, o que é fundamental para qualquer *script* de automação.


O módulo `subprocess` do Python é o seu principal amigo quando você precisa que seu script execute comandos como `docker`, `kubectl`, `colima`, ou `dagger`.

### Cenário: Gerenciamento de Imagens Docker

Você precisa de um *script* de saúde do sistema que verifique o status do Docker e liste todas as imagens no seu ambiente Colima.

#### 🧠 Conceitos Chave para este Desafio:
1.  **Módulo `subprocess`**: A forma correta e segura de executar comandos externos.
2.  **`subprocess.run()`**: A função moderna e recomendada.
3.  **Saída (stdout) e Erro (stderr)**: Capturar e lidar com a resposta do comando.
4.  **Parsing de String**: Transformar a saída de texto do terminal em dados estruturados (como listas ou dicionários).

### Tarefas:

1.  **Função de Execução Segura:**
    * Crie uma função chamada `executar_comando(comando_em_lista)`. O `comando_em_lista` deve ser uma lista de *strings* (ex: `['docker', 'images']`).
    * Use `subprocess.run(comando_em_lista, capture_output=True, text=True, check=True)`:
        * `capture_output=True` armazena o `stdout` e `stderr`.
        * `text=True` decodifica a saída como texto.
        * `check=True` fará o Python gerar uma exceção se o comando retornar um código de erro (útil para detectar falhas).
    * A função deve retornar a saída do comando (`resultado.stdout`).
    * *Tratamento de Erro:* Adicione um bloco `try...except` para capturar a exceção `subprocess.CalledProcessError` e imprima uma mensagem de erro útil (incluindo `resultado.stderr`) antes de retornar `None`.

2.  **Executar e Verificar o Status do Docker:**
    * Use sua função para executar `docker info`.
    * Imprima a mensagem: "--- Status do Docker (Colima) ---" seguida pela saída do comando.

3.  **Parsing de Imagens (Simulado):**
    * Use sua função para executar `docker images`.
    * A saída é uma tabela. Seu desafio é transformá-la em uma lista de dicionários, onde cada dicionário representa uma imagem com chaves como `REPOSITORY`, `TAG`, `IMAGE ID`, e `SIZE`.
    * *DICA AVANÇADA:* Para simplificar o *parsing*, execute `docker images --format "{{.Repository}} | {{.Tag}} | {{.ID}} | {{.Size}}"` para obter um formato mais fácil de separar (usando `split('|')`).

4.  **Ação de Automação (Simulada):**
    * **Identificação:** Percorra sua lista de dicionários de imagens.
    * **Condição:** Identifique qualquer imagem que tenha a `TAG` igual a `latest` (uma tag que se move e pode ser perigosa em produção).
    * **Comando de Ação:** Imprima na tela o comando **simulado** que você usaria para marcar (`tag`) essa imagem com um novo nome, por exemplo, `docker tag [IMAGE_ID] [REPOSITORY]:[DATA_DE_HOJE]`.

---

Este desafio é a **cola** que une o Python ao mundo real do seu terminal. É a ponte essencial para a automação de *scripts* mais complexos.

**Mostre-me seu *script* Python com a função `executar_comando` e como você usa a saída do `docker images`!**