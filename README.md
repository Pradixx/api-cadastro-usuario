# API de Cadastro de Usuário

Uma API RESTful desenvolvida com Spring Boot para gerenciar o cadastro de usuários. Este projeto demonstra a implementação de operações CRUD (Create, Read, Update, Delete) para o recurso `Usuario`, utilizando um banco de dados em memória H2.

## Tecnologias Utilizadas

O projeto `api-cadastro-usuario` é construído com as seguintes tecnologias:

*   **Java 24**: Linguagem de programação principal.
*   **Spring Boot 3.5.5**: Framework para facilitar o desenvolvimento de aplicações Java.
*   **Spring Data JPA**: Para persistência de dados e interação com o banco de dados.
*   **Spring Web**: Para construir APIs RESTful.
*   **H2 Database**: Banco de dados em memória utilizado para desenvolvimento e testes.
*   **Maven**: Ferramenta de automação de build e gerenciamento de dependências.
*   **Lombok**: Biblioteca para reduzir código boilerplate em classes Java.

## Funcionalidades

A API oferece os seguintes endpoints para gerenciar usuários:

*   **Cadastrar Usuário**: Permite criar um novo usuário com nome e e-mail.
*   **Buscar Usuário por E-mail**: Retorna os dados de um usuário específico utilizando seu e-mail.
*   **Atualizar Usuário**: Permite atualizar o nome e/ou e-mail de um usuário existente pelo seu ID.
*   **Deletar Usuário**: Remove um usuário específico pelo seu e-mail.

## Estrutura do Projeto

O projeto segue a arquitetura de camadas com uma estrutura de pacotes bem definida:

```
api-cadastro-usuario/
├── mvnw
├── mvnw.cmd
├── pom.xml
└── src/
    └── main/
        └── java/
            └── com/
                └── deigo/
                    └── cadastro_usuario/
                        ├── CadastroUsuarioApplication.java
                        ├── business/
                        │   └── UsuarioService.java
                        ├── controller/
                        │   └── UsuarioController.java
                        └── infrastructure/
                            ├── entitys/
                            │   └── Usuario.java
                            └── repository/
                                └── UsuarioRepository.java
```

*   **`CadastroUsuarioApplication.java`**: Classe principal da aplicação Spring Boot.
*   **`controller/UsuarioController.java`**: Gerencia as requisições HTTP e define os endpoints da API.
*   **`business/UsuarioService.java`**: Contém a lógica de negócios e orquestra as operações entre o controlador e o repositório.
*   **`infrastructure/entitys/Usuario.java`**: Define a estrutura de dados para um usuário, mapeada para o banco de dados.
*   **`infrastructure/repository/UsuarioRepository.java`**: Interface para operações de persistência de dados (CRUD) para a entidade `Usuario`.

## Como Rodar o Projeto

Para configurar e executar o projeto localmente, siga os passos abaixo:

### Pré-requisitos

Certifique-se de ter o seguinte software instalado em sua máquina:

*   **Java Development Kit (JDK) 24** ou superior.
*   **Maven**.

### Passos para Execução

1.  **Clone o repositório:**

    ```bash
    git clone https://github.com/Pradixx/api-cadastro-usuario.git
    cd api-cadastro-usuario
    ```

2.  **Compile o projeto:**

    ```bash
    ./mvnw clean install
    ```

3.  **Execute a aplicação:**

    ```bash
    ./mvnw spring-boot:run
    ```

A aplicação será iniciada e estará acessível em `http://localhost:8081` (conforme configurado no vídeo de demonstração).

## Endpoints da API

Todos os endpoints estão sob o prefixo `/usuario`.

### `POST /usuario`

*   **Descrição**: Cadastra um novo usuário.
*   **Corpo da Requisição**: Objeto `Usuario` (sem `id`).
*   **Resposta**: `200 OK` (sem corpo de resposta).

    ```json
    {
        "email": "novo.usuario@example.com",
        "nome": "Novo Usuário"
    }
    ```

### `GET /usuario?email={email}`

*   **Descrição**: Busca um usuário pelo seu e-mail.
*   **Parâmetros de Query**: `email` (e-mail do usuário a ser buscado).
*   **Resposta**: `200 OK` com o objeto `Usuario` encontrado.

    ```json
    {
        "id": 1,
        "email": "novo.usuario@example.com",
        "nome": "Novo Usuário"
    }
    ```

### `PUT /usuario?id={id}`

*   **Descrição**: Atualiza um usuário existente pelo seu ID. Permite atualização parcial.
*   **Parâmetros de Query**: `id` (ID do usuário a ser atualizado).
*   **Corpo da Requisição**: Objeto `Usuario` com os campos a serem atualizados.
*   **Resposta**: `200 OK` (sem corpo de resposta).

    ```json
    {
        "nome": "Nome Atualizado"
    }
    ```

### `DELETE /usuario?email={email}`

*   **Descrição**: Deleta um usuário pelo seu e-mail.
*   **Parâmetros de Query**: `email` (e-mail do usuário a ser deletado).
*   **Resposta**: `200 OK` (sem corpo de resposta).

## Exemplos de Uso (com `curl`)

Assumindo que a API está rodando em `http://localhost:8081`.

### Cadastrar um novo usuário

```bash
curl -X POST -H "Content-Type: application/json" -d '{"email":"teste@example.com", "nome":"Teste Usuário"}' http://localhost:8081/usuario
```

### Buscar um usuário por e-mail

```bash
curl -X GET "http://localhost:8081/usuario?email=teste@example.com"
```

### Atualizar o nome de um usuário (substitua `{id}` pelo ID real do usuário)

```bash
curl -X PUT -H "Content-Type: application/json" -d '{"nome":"Usuário Teste Atualizado"}' "http://localhost:8081/usuario?id={id}"
```

### Deletar um usuário por e-mail

```bash
curl -X DELETE "http://localhost:8081/usuario?email=teste@example.com"
```

## Licença

Este projeto está licenciado sob a licença MIT. Veja o arquivo `LICENSE` para mais detalhes. (Nota: O arquivo LICENSE não foi fornecido no repositório original, mas é uma boa prática incluí-lo.)