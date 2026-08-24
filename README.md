# JsonPlaceholder API Tests

Collection desenvolvida para realizar **testes automatizados de API utilizando Postman** sobre a API pública [JSONPlaceholder](https://jsonplaceholder.typicode.com/).

O projeto tem como objetivo validar o comportamento dos principais endpoints, contemplando **cenários positivos e negativos**, além de validar:

- Status codes
- Estrutura das respostas
- Headers
- Tempo de resposta
- Campos obrigatórios
- Tipos de dados
- Dados retornados
- Regras de negócio
- JSON Schema

---

## API utilizada

**JSONPlaceholder**

API REST pública utilizada para testes e desenvolvimento.

**Base URL:**

```text
https://jsonplaceholder.typicode.com
```

---

## Estrutura da Collection

A Collection está organizada por recurso da API:

```text
JsonPlaceholder API Tests
│
├── Albums
├── Comments
├── Photos
├── Users
├── Posts
└── Todos
```

Cada pasta contém as requisições relacionadas ao respectivo recurso.

---

## Variáveis

A Collection utiliza variáveis em diferentes escopos para facilitar a reutilização dos dados, manutenção das requisições e execução dos testes.

### Environment Variables

A variável `baseUrl` é configurada no Environment e utilizada como URL base da API.

| Variável | Escopo | Finalidade | Exemplo |
|---|---|---|---|
| `baseUrl` | Environment | Define a URL base da API | `https://jsonplaceholder.typicode.com` |

Exemplo de utilização:

```text
{{baseUrl}}/users
```

### Collection Variables

As variáveis específicas da Collection são utilizadas para parametrizar IDs, filtros e dados necessários durante a execução dos testes.

| Variável | Finalidade |
|---|---|
| `id` | Identificador genérico utilizado nas requisições |
| `userId` | Identificador de um usuário específico |
| `postId` | Identificador de um post específico |
| `albumId` | Identificador de um álbum específico |
| `oldTitle` | Armazena o título anterior de um post para comparação após atualização |
| `completed` | Define o valor do filtro de conclusão dos Todos |

Exemplos:

```text
{{baseUrl}}/posts/{{postId}}
{{baseUrl}}/posts?userId={{userId}}
{{baseUrl}}/todos?completed={{completed}}
```

---

# Cenários de testes

## Albums

Testes relacionados ao recurso `/albums`.

### GET — Buscar todos os álbuns

**Validações:**

- Código de status é `200`
- Resposta é um array
- Resposta não está vazia
- Resposta contém 100 registros
- Resposta contém os campos esperados
- Campos possuem o tipo correto

### POST — Criar álbum

**Validações:**

- Código de status é `201`
- Resposta é um objeto
- Campos possuem o tipo correto
- Campo `title` não está vazio

### PATCH — Atualizar álbum

**Validações:**

- Código de status é `200`
- Resposta é um objeto
- Campos possuem o tipo correto
- Campo `title` não está vazio
- Verifica se o campo `title` foi atualizado

### DELETE — Excluir álbum

**Validações:**

- Código de status é `200`
- Resposta é um objeto
- Resposta é um objeto vazio

### GET — Álbum de ID inexistente

**Validações:**

- Código de status é `404`
- Resposta é um objeto vazio

---

## Comments

Testes relacionados ao recurso `/comments`.

### GET — Buscar todos os comentários

**Validações:**

- Código de status é `200`
- Resposta é um array
- Resposta não está vazia
- Resposta contém os campos esperados
- Campos possuem o tipo correto

### GET — Buscar comentários por postagem

**Validações:**

- Código de status é `200`
- Resposta é um array
- Resposta contém pelo menos um comentário
- Resposta contém os campos esperados
- Campos possuem o tipo correto
- Campos não estão vazios
- Campo `email` é válido
- Todos os comentários pertencem ao `postId` informado

### POST — Criar comentário

**Validações:**

- Código de status é `201`
- Resposta é um objeto
- Campos possuem o tipo correto
- Campos não estão vazios

### PATCH — Atualizar comentário

**Validações:**

- Código de status é `200`
- Resposta é um objeto
- Campos possuem o tipo correto
- Campo `name` não está vazio
- Verifica se o campo `name` foi atualizado

### DELETE — Excluir comentário

**Validações:**

- Código de status é `200`
- Resposta é um objeto
- Resposta é um objeto vazio

---

## Photos

Testes relacionados ao recurso `/photos`.

### GET — Buscar todas as fotos

**Validações:**

- Código de status é `200`
- Resposta é um array
- Resposta não está vazia
- Resposta contém os campos esperados
- Campos possuem o tipo correto
- Resposta contém 5000 registros

### POST — Criar foto

**Validações:**

- Código de status é `201`
- Resposta é um objeto
- Campos possuem o tipo correto
- Campo `title` não está vazio

### PATCH — Atualizar foto

**Validações:**

- Código de status é `200`
- Resposta é um objeto
- Campos possuem o tipo correto
- Campos não estão vazios
- Verifica se o campo `title` foi atualizado corretamente

### DELETE — Excluir foto

**Validações:**

- Código de status é `200`
- Resposta é um objeto
- Resposta é um objeto vazio

---

## Users

Testes relacionados ao recurso `/users`.

### GET — Buscar todos os usuários

**Validações:**

- Código de status é `200`
- Resposta é um array
- Resposta não está vazia
- Resposta contém os campos esperados
- Campos possuem o tipo correto
- Campo `address` é um objeto
- `address` contém os campos esperados
- Campo `geo` é um objeto
- `geo` contém os campos esperados
- Email é válido
- Resposta contém 10 registros

### GET — Buscar usuário por ID

**Validações:**

- Código de status é `200`
- Resposta é um objeto
- Resposta contém os campos esperados
- Campos possuem o tipo correto
- Campo `address` é um objeto
- `address` contém os campos esperados
- Campo `geo` é um objeto
- `geo` contém os campos esperados
- Campo `company` é um objeto
- `company` possui os campos esperados
- Resposta não está vazia
- Email é válido
- ID é igual ao valor da variável

### POST — Criar usuário

**Validações:**

- Código de status é `201`
- Resposta é um objeto
- ID foi gerado
- Nome enviado na requisição é igual ao nome retornado
- Username enviado na requisição é igual ao username retornado
- Email enviado na requisição é igual ao email retornado
- Resposta contém os campos esperados
- Campos possuem o tipo correto
- Campos não estão vazios

### PUT — Atualizar usuário

**Validações:**

- Código de status é `200`
- Resposta é um objeto
- ID retornado corresponde ao ID informado
- Resposta contém os campos esperados
- Campos possuem o tipo correto
- Campo `name` foi atualizado
- Campo `username` foi atualizado
- Campo `email` foi atualizado
- Email é válido

### PATCH — Atualizar parcialmente usuário

**Validações:**

- Código de status é `200`
- Resposta é um objeto
- Resposta contém os campos esperados
- Campos possuem o tipo correto
- `address` possui os campos esperados
- `company` possui os campos esperados
- Campo `email` foi atualizado
- Email é válido

### DELETE — Excluir usuário

**Validações:**

- Código de status é `200`
- Resposta é um objeto
- Resposta é um objeto vazio

### GET — Usuário inválido

**Validações:**

- Código de status é `404`
- Resposta é um objeto
- Resposta é um objeto vazio

---

## Posts

Testes relacionados ao recurso `/posts`.

### GET — Buscar todas as postagens

**Validações:**

- Código de status é `200`
- Resposta é um array
- Resposta não está vazia
- Resposta contém os campos esperados
- Campos possuem o tipo correto
- Resposta contém 100 registros

### GET — Buscar postagens por usuário

**Validações:**

- Código de status é `200`
- Resposta é um array
- Resposta contém pelo menos uma postagem
- Resposta contém os campos esperados
- Campos possuem o tipo correto
- Todas as postagens pertencem ao usuário `{{userId}}`
- Resposta está em conformidade com o JSON Schema
- Postagem de ID `5` é encontrada

### POST — Criar postagem

**Validações:**

- Código de status é `201`
- Resposta é um objeto
- Campos possuem o tipo correto
- Campos não estão vazios

### PATCH — Atualizar postagem

**Validações:**

- Código de status é `200`
- Resposta é um objeto
- Resposta contém os campos esperados
- Campos possuem o tipo correto
- Campos não estão vazios
- Retorna a postagem de ID `5`
- Postagem pertence ao usuário `{{userId}}`
- Título antigo existe
- Título foi alterado

### DELETE — Excluir postagem

**Validações:**

- Código de status é `200`
- Resposta retorna um objeto
- Resposta é um objeto vazio

### GET — ID inexistente

**Validações:**

- Código de status é `404`
- Resposta é um objeto
- Resposta deve ser um objeto vazio

### POST — Atualização com tipo de dado inválido

Cenário utilizado para avaliar o comportamento da API diante de dados com tipos inválidos.

Exemplo:

```json
{
  "title": 12345
}
```

**Validações:**

- Campos possuem o tipo correto
- Campos não estão vazios

---

## Todos

Testes relacionados ao recurso `/todos`.

### GET — Buscar todos

**Validações:**

- Código de status é `200`
- Resposta é um array
- Resposta não está vazia
- Resposta contém os campos esperados
- Campos possuem o tipo correto
- Resposta contém 200 registros

### GET — Buscar todos por status de conclusão

**Validações:**

- Código de status é `200`
- Resposta é um array
- Resposta contém pelo menos um item
- Resposta contém os campos esperados
- Campos possuem o tipo correto
- Todos os itens possuem o status `completed` correspondente ao valor informado

### POST — Criar todo

**Validações:**

- Código de status é `201`
- Resposta é um objeto
- Campos possuem o tipo correto
- Campo `title` não está vazio

### PATCH — Atualizar todo

**Validações:**

- Código de status é `200`
- Resposta é um objeto
- Resposta contém os campos obrigatórios
- Campos possuem o tipo correto
- Campo `title` não está vazio
- Campos foram atualizados corretamente

### DELETE — Excluir todo

**Validações:**

- Código de status é `200`
- Resposta retorna um objeto
- Resposta é um objeto vazio

---

# Cenários negativos

A Collection também contempla cenários negativos para avaliar o comportamento da API diante de recursos inexistentes ou dados inválidos.

### Buscar recurso inexistente

```http
GET {{baseUrl}}/posts/999
```

**Validações:**

- Status `404`
- Resposta `{}`

### Atualização com tipos de dados inválidos

Exemplo:

```json
{
  "title": 12345
}
```

Esse cenário é utilizado para avaliar o comportamento da API diante de um tipo de dado diferente do esperado.

---

# Exemplos de validações automatizadas

## Status Code

```javascript
pm.test("Código de status é 200", function () {
    pm.response.to.have.status(200);
});
```

## Content-Type

```javascript
pm.test("Content-Type é application/json", function () {
    if (pm.response.code != 204) {
        pm.expect(
            pm.response.headers.get("Content-Type")
        ).to.include("application/json");
    }
});
```

## Tempo de resposta

```javascript
pm.test("Tempo de resposta é menor que 1000ms", function () {
    pm.expect(pm.response.responseTime).to.be.below(1000);
});
```

## Estrutura da resposta

```javascript
const response = pm.response.json();

pm.test("Resposta é um array", function () {
    pm.expect(response).to.be.a("array");
});
```

## Campos obrigatórios

```javascript
pm.test("Resposta contém os campos esperados", function () {
    response.forEach(album => {
        pm.expect(album).to.have.property("userId");
        pm.expect(album).to.have.property("id");
        pm.expect(album).to.have.property("title");
    });
});
```

## Tipos de dados

```javascript
pm.test("Campos possuem o tipo correto", function () {
    response.forEach(album => {
        pm.expect(album.userId).to.be.a("number");
        pm.expect(album.id).to.be.a("number");
        pm.expect(album.title).to.be.a("string");
    });
});
```

## Validação dos dados retornados

```javascript
const expectId = Number(pm.variables.get("id"));

pm.test("ID é igual ao valor da variável", function () {
    pm.expect(response.id).to.equal(expectId);
});
```

## Regra de negócio

```javascript
pm.test(`Todas as postagens pertencem ao usuário ${userId}`, function () {
    response.forEach(post => {
        pm.expect(post.userId).to.equal(userId);
    });
});
```

---

# Validações compartilhadas

As validações abaixo são configuradas no nível da **Collection** e são aplicadas às requisições conforme a configuração definida:

- Tempo de resposta menor que `1000ms`
- `Content-Type` igual a `application/json`

Dessa forma, essas validações não precisam ser repetidas individualmente em cada requisição.

Essa abordagem reduz a duplicação de scripts e facilita a manutenção da Collection.

---

# JSON Schema

A Collection utiliza **JSON Schema** para validar a estrutura da resposta de determinados endpoints.

Exemplo:

```javascript
const schema = {
    type: "array",
    items: {
        type: "object",
        required: ["userId", "id", "title", "body"],
        properties: {
            userId: { type: "number" },
            id: { type: "number" },
            title: { type: "string" },
            body: { type: "string" }
        }
    }
};

pm.test("Resposta está em conformidade com o JSON Schema", function () {
    pm.response.to.have.jsonSchema(schema);
});
```

---

# Execução dos testes

Os testes podem ser executados:

- Individualmente pelo Postman
- Utilizando o **Collection Runner**

O Collection Runner permite executar a Collection ou grupos de requisições e acompanhar os resultados dos testes automatizados.

---

# Resultado esperado

Ao executar a Collection, os testes devem validar automaticamente os comportamentos esperados de cada endpoint.

Os resultados podem ser acompanhados diretamente no Postman, permitindo identificar:

- Testes aprovados
- Testes reprovados
- Status retornado
- Tempo de resposta
- Mensagens de assertion

---

# Próximas evoluções

Como evolução do projeto, estão previstas as seguintes melhorias:

- [ ] Implementar execução automatizada da Collection utilizando **Newman**
- [ ] Integrar a execução dos testes a um pipeline de **CI/CD**
- [ ] Avaliar a geração de relatórios automatizados dos testes
- [ ] Ampliar a cobertura de cenários negativos
- [ ] Avaliar o uso de **Mock Server** para simular cenários e respostas específicas
- [ ] Evoluir o gerenciamento de dados de teste e variáveis
- [ ] Ampliar a cobertura de validações de contratos e schemas

> As funcionalidades listadas nesta seção representam possibilidades de evolução do projeto e não fazem parte da implementação atual.

---

# Considerações

O projeto foi estruturado buscando centralizar validações comuns no nível da **Collection** e manter nas requisições as validações específicas de cada cenário.

Essa abordagem reduz a duplicação de scripts, facilita a manutenção da Collection e permite uma melhor organização dos testes automatizados.

O projeto também busca demonstrar a aplicação prática de conceitos de **QA e testes de API**, incluindo validação de contratos, status codes, headers, payloads, tipos de dados, regras de negócio e cenários positivos e negativos.
