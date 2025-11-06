## 🛠️ Desafio 6: Python e Dagger - O Pipeline Definido em Código

Vamos usar a biblioteca oficial do Dagger em Python para definir uma *pipeline* simples que simula um processo de *build*, teste e *push* de uma imagem, tudo orquestrado pelo Dagger.

### Pré-requisitos Mentais (Você precisará simular a instalação do Dagger SDK):

Para este desafio, você deve imaginar que a biblioteca `@dagger.io/dagger` está instalada e que você tem um motor Dagger rodando no seu Colima (`dagger start`).

### Cenário: Pipeline Simples de CI/CD para uma Aplicação Web

Você tem um repositório simples com um `Dockerfile` e um script de teste (`test.sh`).

### Tarefas:

1.  **Estrutura Base do Dagger Client:**

      * Importe o Dagger Client: `import dagger` e `import asyncio` (pois o Dagger SDK é assíncrono).
      * Crie a função `main()` decorada com `@dagger.with_container_engine()` para ser o ponto de entrada assíncrono do Dagger.
      * Dentro de `main()`, inicialize o cliente: `async with dagger.AsyncClient() as client:`.

2.  **Definindo o Projeto (Contexto):**

      * Use `client.container().from_source(...)` para carregar o **diretório atual** (`.`) como o contexto do seu *pipeline*.

3.  **Passo 1: Build da Imagem (Build Stage):**

      * No seu contexto de fonte, use o método `.container()` e `.with_dockerfile()` para especificar o `Dockerfile` no diretório raiz.
      * Use `.build(tag="myapp:test-$(date +%s)")` para construir a imagem. **Armazene o resultado (o objeto de imagem)** em uma variável, por exemplo, `built_image`.

4.  **Passo 2: Executar Testes (Test Stage):**

      * Usando a imagem que você acabou de construir (`built_image`), execute o script de teste:
      * Use `.with_entrypoint(["/bin/sh", "-c"])` e o comando para executar o teste: `await built_image.exec(["./test.sh"])`.
      * **Tratamento de Falha:** Para simular a falha de teste, se o `./test.sh` falhar (retornar código diferente de 0), o Dagger *automaticamente* falha o *pipeline*. Você precisa **envelopar** a chamada `await built_image.exec(...)` em um `try...except dagger.dagger.errors.ExecError as e:` para capturar a falha de teste e imprimir uma mensagem informativa.

5.  **Passo 3: Publicar a Imagem (Publish Stage):**

      * **SE** os testes passaram (o bloco `try` não falhou), use o objeto `built_image`.
      * Defina a *tag* final (ex: `myapp:latest`).
      * Use `.publish(f"seu-usuario/myapp:latest")` (substitua `seu-usuario` pelo seu nome de usuário Docker/Colima).

6.  **Execução Final:**

      * No final do seu *script*, adicione o código padrão para rodar a função `main`:
        ```python
        if __name__ == "__main__":
            asyncio.run(main())
        ```

-----

### O que você deve me mostrar:

O código Python completo do seu *script* principal (`dagger_pipeline.py`), incluindo as importações, a estrutura assíncrona, a lógica de `try/except` para os testes, e a chamada de `publish`.

Este desafio exige que você pense em termos de **grafos de execução** e **assincronicidade**, que são o coração do Dagger. Boa sorte\!