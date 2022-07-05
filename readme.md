# json-server-base

Esse é o repositório com a base de JSON-Server + JSON-Server-Auth já configurada, feita para ser usada no desenvolvimento das API's nos Capstones do Q2.

## Endpoints

Assim como a documentação do JSON-Server-Auth traz (https://www.npmjs.com/package/json-server-auth), existem 3 endpoints que podem ser utilizados para cadastro e 2 endpoints que podem ser usados para login.

### Cadastro

POST /register <br/>
POST /signup <br/>
POST /users

Qualquer um desses 3 endpoints irá cadastrar o usuário na lista de "Users", sendo que os campos obrigatórios são os de email e password.
Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.

### Login

POST /login <br/>
POST /signin

Qualquer um desses 2 endpoints pode ser usado para realizar login com um dos usuários cadastrados na lista de "Users"

<!-- #

## Rota que não precisa de autenticação

#

<h2 align ='center'> Listando tecnologias </h2>

#

Nesta aplicação o usuário sem fazer login ou se cadastrar pode ver todas as tecnologias cadastradas

`GET /tecnologias - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "tecnologia": "JavaScript",
    "userId": 1,
    "id": 1
  },
  {
    "tecnologia": "Python",
    "userId": 2,
    "id": 2
  },
  {
    "tecnologia": "Python",
    "userId": 1,
    "id": 3
  }
]
```

#

## Rotas que precisam de autenticação

#

<h2 align ='center'> Cadastrando tecnologia </h2>

Para cadastrar uma tecnologia deverá ser passado junto com a tecnologia o id do usuário que está cadastrando

`POST /tecnologias - FORMATO DA REQUISIÇÃO`

```json
{
  "tecnologia": "Python",
  "userId": idDoUsuario
}
```

Caso dê tudo certo, a resposta será assim:

`POST /tecnologias - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "tecnologias": "Python",
  "userId": idDoUsuario,
  "id": 1
}
```

#

<h2 align ='center'> Acessando informações de usuário </h2>

`GET /users/{idDoUsuário} - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "email": "teste@mail.com",
  "password": "$2a$10$vcTAabOT.TDrd8nZ3miXBe4myYUO5H4FyHMeXfGgh7nD5T6DaDDRO",
  "id": idDoUsuario
}
```

#

<h2 align ='center'> Acessando as tecnologias criadas por um usuário específico </h2>

`GET /users/{idDoUsuário}?_embed=tecnologias - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "email": "teste@mail.com",
  "password": "$2a$10$vcTAabOT.TDrd8nZ3miXBe4myYUO5H4FyHMeXfGgh7nD5T6DaDDRO",
  "id": 2,
  "tecnologias": [
    {
      "tecnologia": "Python",
      "userId": 2,
      "id": 2
    }
  ]
} -->
