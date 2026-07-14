# 📋 Spring Boot + MongoDB - API de Users e Posts

Projeto criado para estudo e prática de **Spring Boot** com **MongoDB**, com foco principal em testar e explorar requisições via **Postman**. A arquitetura utiliza o padrão **DTO (Data Transfer Object)** para separar as camadas de entidade e de transporte de dados entre a API e o cliente.

---

## 🚀 Tecnologias utilizadas

- **Java**
- **Spring Boot**
- **MongoDB**
- **Postman** (para testes das requisições)

---

## ⚙️ Configuração do ambiente

Após clonar o repositório, é necessário configurar o banco de dados antes de rodar a aplicação:

1. Acesse o arquivo `src/main/resources/application.properties`
2. Altere as seguintes propriedades:

```properties
spring.application.name=NOME_DO_SEU_PROJETO
spring.data.mongodb.uri=mongodb://localhost:PORTA/NOME_DO_BANCO
```

| Propriedade | Descrição |
|---|---|
| `spring.application.name` | Nome do projeto/aplicação |
| `spring.data.mongodb.uri` | URI de conexão com o MongoDB, no formato `mongodb://localhost:[porta]/[nome_do_banco]` |

> 💡 Certifique-se de que o MongoDB esteja rodando localmente (ou aponte para uma instância remota) antes de iniciar a aplicação.

---

## 🗂️ Estrutura do projeto

O projeto possui duas entidades principais: **User** e **Post**.

### 👤 User
Operações disponíveis:
- Listar todos (Find All)
- Buscar por ID (Find By Id)
- Inserir (Insert)
- Deletar (Delete)
- Atualizar (Update)

### 📝 Post
Operações disponíveis:
- Buscar por ID (Find By Id)
- Buscar por título (Find By Title)
- Busca completa / Full Search (permite pesquisar um texto tanto no título do post quanto nos comentários, com filtro de data mínima e máxima)

---

## 📡 Endpoints (Postman)

### 🔹 Post

| Ação | Verbo | Endpoint |
|---|---|---|
| Buscar por ID | `GET` | `localhost:8080/posts/{id}` |
| Buscar por título | `GET` | `localhost:8080/posts/titlesearch?text=` |
| Busca completa | `GET` | `localhost:8080/posts/fullsearch?text=&minDate=&maxDate=` |

**Exemplo de uso do Full Search:**
```
GET localhost:8080/posts/fullsearch?text=viagem&minDate=21/03/2018&maxDate=23/03/2018
```
Os parâmetros `minDate` e `maxDate` são opcionais. Caso não sejam informados, o sistema considera automaticamente o período entre `01/01/1970` e a data atual.

---

### 🔹 User

| Ação | Verbo | Endpoint |
|---|---|---|
| Listar todos | `GET` | `localhost:8080/users` |
| Buscar por ID | `GET` | `localhost:8080/users/{id}` |
| Inserir novo usuário | `POST` | `localhost:8080/users` |
| Deletar usuário | `DELETE` | `localhost:8080/users/{id}` |
| Atualizar usuário | `PUT` | `localhost:8080/users/{id}` |
| Listar posts do usuário | `GET` | `localhost:8080/users/{id}/posts` |

**Exemplo de body para Insert/Update (POST/PUT):**
```json
{
  "name": "Maria Brown",
  "email": "maria@gmail.com"
}
```

---

## 🌱 Dados de exemplo (Seed)

Ao iniciar a aplicação, o sistema popula automaticamente o banco com dados de exemplo para facilitar os testes, através de um `CommandLineRunner`. São criados:

- **3 usuários**: Maria Brown, Alex Green e Bob Grey
- **2 posts** de autoria da Maria:
  - *"Partiu Viagem"* (21/03/2018)
  - *"Bom dia"* (23/03/2018)
- **3 comentários** distribuídos entre os posts, feitos por Alex e Bob

Isso significa que, assim que o projeto for iniciado, já é possível realizar buscas (`GET`) e testar os endpoints sem precisar cadastrar nada manualmente.

> ⚠️ Todo o banco é limpo (`deleteAll`) antes da inserção dos dados de exemplo, então evite rodar em uma base de produção.

---

## ✅ Pré-requisitos para rodar o projeto

Antes de executar a aplicação, você precisa ter instalado:

- **Java JDK** (versão 11 ou superior recomendada)
- **Maven** (ou utilizar o wrapper `mvnw` incluso no projeto)
- **MongoDB** instalado e em execução localmente (ou uma instância na nuvem, como o MongoDB Atlas)
- **Postman** (ou ferramenta similar) para testar os endpoints
- Uma IDE de sua preferência (IntelliJ, Eclipse, VS Code, etc.)

### ▶️ Como rodar

```bash
# Clone o repositório
git clone https://github.com/Manuelcamp/Java-MongoDB.git

# Acesse a pasta do projeto
cd nome-do-projeto

# Configure o application.properties conforme instruções acima

# Rode o projeto
./mvnw spring-boot:run
```

A aplicação estará disponível em `http://localhost:8080`.

---

## 📌 Observações

Este é o primeiro de uma série de projetos de estudo que serão publicados. O foco aqui foi entender a integração entre Spring Boot e MongoDB, o uso de DTOs para desacoplar entidades da camada de apresentação, e a prática de testes de API via Postman.
