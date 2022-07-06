# Econo Market API

Esse é o repositório com a API do Econo Market, o link base para a API é : https://ecomarketapi.herokuapp.com

## Endpoints

#

<h2 align ='center'> Cadastrando usuários </h2>

#

`POST /register - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "teste3@gmail.com",
  "cpf": "09329802323", //ou CNPJ no caso de cadastro de empresa
  "endereço": "rua tal", //O campo endereço só existe no caso de cadastro de empresa
  "password": "123456"
}
```

### Caso esteja tudo ok a resposta será assim:

`POST /register - FORMATO DA RESPOSTA - STATUS 201`

```json
{
	"accessToken": tokenGeradoPelaAPI,
	"user": {
		"email": "teste3@gmail.com",
		"id": idGeradoPelaAPI
	}
}
```

#

<h2 align ='center'> Fazendo login </h2>

#

`POST /login - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "teste3@gmail.com",
  "password": "123456"
}
```

### Caso esteja tudo ok a resposta será assim:

`POST /login - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"accessToken": tokenGeradoPelaAPI,
	"user": {
		"email": "teste3@gmail.com",
		"id": idGeradoPelaAPI
	}
}
```

#

## Rota que não precisa de autenticação

#

<h2 align ='center'> Listando produtos </h2>

#

### Nesta aplicação o usuário sem fazer login ou se cadastrar pode ver todos os produtos cadastrados

`GET /products - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "name": "MELANCIA",
    "categoria": "Outros",
    "description": "blablabla",
    "originalPrice": "2R$",
    "promotionalPrice": "1R$",
    "userId": 2,
    "id": 3
  },
  {
    "name": "banana",
    "categoria": "Outros",
    "description": "blablabla",
    "originalPrice": "2R$",
    "promotionalPrice": "1R$",
    "userId": 2,
    "id": 5
  },
  {
    "name": "banana",
    "categoria": "Outros",
    "description": "blablabla",
    "originalPrice": "2R$",
    "promotionalPrice": "1R$",
    "userId": 2,
    "id": 6
  }
]
```

#

## Rotas que precisam de autenticação

#

<h2 align ='center'> Cadastrando Produtos </h2>

#

### Para cadastrar um Produto deverá ser passado junto com ao produto o id do usuário que está cadastrando

`POST /products - FORMATO DA REQUISIÇÃO`

```json
{
	"image": "https/:imagem",
	"name": "Melão",
    "categoria":"Outros",
	"description": "blablabla",
	"originalPrice": "2R$",
	"promotionalPrice": "1R$",
	"userId": {idDoUsuário}
}
```

### Caso o userId passado não seja compatível com o token a resposta será assim:

`POST /products - FORMATO DA RESPOSTA - STATUS 403`

```json
"Private resource creation: request body must have a reference to the owner id"
```

### Caso dê tudo certo, a resposta será assim:

`POST /products - FORMATO DA RESPOSTA - STATUS 201`

```json
{
	"image": "https/:imagem",
	"name": "Melão",
    "categoria":"Outros",
	"description": "blablabla",
	"originalPrice": "2R$",
	"promotionalPrice": "1R$",
	"userId": idDoUsuário,
	"id": idGeradoPelaAPI
}
```

#

<h2 align ='center'> Apagar um produto </h2>

#

### Nesta API só o usuário que cadastrou o produto pode apagar ele

`DELETE /products/{idDoProduto} - FORMATO DA RESPOSTA - STATUS 201`

```json
{}
```

### Caso você esteja tentando apagar o produto que outra pessoa cadastrou a resposta será assim:

`DELETE /products/{idDoProduto} - FORMATO DA RESPOSTA - STATUS 403`

```json
"Private resource access: entity must have a reference to the owner id"
```

#

<h2 align ='center'> Editar um produto </h2>

#

`PATCH /products{idDoProduto} - FORMATO DA REQUISIÇÃO`

### Para alterar um produto deve ser passado o(s) campo(s) que se deseja alterar e obrigatoriamente o userId que receberá o id do usuário

```json
{
	"name":"MELÃO",
	"userId": {idDoUsuário}
}
```

`PATCH /products{idDoProduto} - FORMATO DA RESPOSTA - STATUS 201`

```json
{
	"image": "https/:imagem",
	"name": "MELÃO",
    "categoria":"Outros",
	"description": "blablabla",
	"originalPrice": "2R$",
	"promotionalPrice": "1R$",
	"userId": idDoUsuario,
	"id": idDoProduto
}
```

#

<h2 align ='center'> Adicionar produto na lista de desejo </h2>

#

`POST /wishlist - FORMATO DA REQUISIÇÃO`

### Para adicionar um produto na lista desejo basta enviar o item com o userId sendo o id do usuário que está fazendo a requisição

```json
	{
		"image": "https/:imagem",
		"name": "banana",
        "categoria":"Outros",
		"description": "blablabla",
		"originalPrice": "2R$",
		"promotionalPrice": "1R$",
		"userId": {idDoUsuario}
	}
```

### Caso o userId passado não seja compatível com o token, a resposta será assim:

`POST /wishlist - FORMATO DA RESPOSTA - STATUS 403`

```json
"Private resource creation: request body must have a reference to the owner id"
```

### Caso esteja tudo ok, a resposta será assim:

`POST /wishlist - FORMATO DA RESPOSTA - STATUS 201`

```json
{
	"image": "https/:imagem",
	"name": "banana",
    "categoria":"Outros",
	"description": "blablabla",
	"originalPrice": "2R$",
	"promotionalPrice": "1R$",
	"userId": idDoUsuario,
    "id": idGeradoPelaAPI
}
```

#

<h2 align ='center'> Visualizar lista de desejo </h2>

#

`GET /users/{idDoUsuario}?_embed=wishlist - FORMATO DA REQUISIÇÃO`

### ou

`GET /wishlist?userId={idDoUsuario} - FORMATO DA REQUISIÇÃO`

### Caso o userId passado não seja compatível com o token, a resposta será assim:

`GET /wishlist?userId={idDoUsuario} - FORMATO DA RESPOSTA - STATUS 403`

```json
"Private resource creation: request body must have a reference to the owner id"
```

### Caso esteja tudo ok, a resposta será assim:

`GET /wishlist?userId={idDoUsuario} - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "email": "teste@gmail.com",
  "password": "$2a$10$W.M2drQHRqzR2LBcChzKluPdAqcnwg8Q.S.YzRaRRVGDcZ2cr6LpC",
  "id": 1,
  "wishlist": [
    {
      "image": "https/:imagem",
      "name": "banana",
      "categoria": "Outros",
      "description": "blablabla",
      "originalPrice": "2R$",
      "promotionalPrice": "1R$",
      "userId": 1,
      "id": 2
    }
  ]
}
```

#

<h2 align ='center'> Apagar produto da lista de desejo </h2>

#

`DELETE /wishlist/{idDoProduto} - FORMATO DA RESPOSTA - STATUS 201`

```json
{}
```

### Caso o id do produto não seja compatível com o token a resposta será assim:

```json
"Cannot read properties of undefined (reading 'userId')"
```

#

<h2 align ='center'> Adicionar itens na lista de reserva </h2>

#

`POST /reserved - FORMATO DA REQUISIÇÃO - STATUS 201`

```json
{
  "image": "https/:imagem",
  "name": "banana",
  "categoria":"Outros",
  "description": "blablabla",
  "originalPrice": "2R$",
  "promotionalPrice": "1R$",
  "sellerId": {sellerId},
  "userId": {userId}
}
```

#

<h2 align ='center'> Visualizar lista de itens reservados no comercio </h2>

#

`GET /reserved?_expand=user&sellerId={sellerId} - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "image": "https/:imagem",
    "name": "banana",
    "categoria":"Outros",
    "description": "blablabla",
    "originalPrice": "2R$",
    "promotionalPrice": "1R$",
    "sellerId": sellerId,
    "userId": userId,
    "id": idDoProduto
    "user": {
      "email": "teste2@gmail.com",
      "password": "$2a$10$gW.EKOgpFhfFFQH4yEM6duW.e8PDRlX4gNUpkWnjvoaZ9TJL7Q0AK",
      "id": 2
    }
  },
  {
    "image": "https/:imagem",
    "name": "banana",
    "categoria":"Outros",
    "description": "blablabla",
    "originalPrice": "2R$",
    "promotionalPrice": "1R$",
    "sellerId": sellerId,
    "userId": userId,
    "id": idDoProduto,
    "user": {
      "email": "teste2@gmail.com",
      "password": "$2a$10$gW.EKOgpFhfFFQH4yEM6duW.e8PDRlX4gNUpkWnjvoaZ9TJL7Q0AK",
      "id": 2
    }
  }
]
```

#

`GET /reserved?userId={userId} - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "image": "https/:imagem",
    "name": "banana",
    "categoria":"Outros",
    "description": "blablabla",
    "originalPrice": "2R$",
    "promotionalPrice": "1R$",
    "userId": userId,
    "id": idDoProduto,
  }
]
```

#

<h2 align ='center'> Apagando usuários </h2>

#

### Só é possível apagar a própria conta, caso você tente apagar a conta de outra pessoa acontecerá um erro

`DELETE /users/{userId} - FORMATO DA RESPOSTA - STATUS 200`

```json
{}
```

### Caso o userId passado no endpoint não esteja de acordo com o token a resposta será assim:

`DELETE /users/{userId} - FORMATO DA RESPOSTA - STATUS 403`

```json
"Private resource access: entity must have a reference to the owner id"
```

#

<h2 align ='center'> Editando usuários </h2>

#

`PATCH /users/{userId} - FORMATO DA REQUISIÇÃO`

### No corpo da requisição deverá ser passado os campos que se quer alterar

```json
{
    "password": novaSenha
}
```

### Caso esteja tudo ok a resposta será assim:

`PATCH /users/{userId} - FORMATO DA RESPOSTA - STATUS 200`

```json
{
	"email": emailDoUsuario,
	"password": novaSenha,
	"id": idDoUsuário,
}
```

### Caso o id passado no endpoint não esteja de acordo com o token a reposta será assim:

`PATCH /users/{userId} - FORMATO DA RESPOSTA - STATUS 403`

```json
"Private resource access: entity must have a reference to the owner id"
```
