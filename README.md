<h1 align="center">
HelpTS - API
</h1>

<p align = "center">
Esta é a API da aplicação Help TS - um banco de dados pensado em auxiliar os desenvolvedores a tiparem os seus projetos em TypeScript. O objetivo desta aplicação é além de expandir o conhecimento TS, auxiliar futuros devs que estejam com dúvidas na hora de tipar um código.
</p>

<p align="center">
  <a href="#endpoints">Endpoints</a>
</p>

A API tem um total de XX endpoints, sendo possível transitar entre usuários, soluções e comentários das soluções.

A URL base da API é https://json-server-project-help-ts.herokuapp.com/

## Rotas que não precisam de autenticação

<h2 align ='center'> Listando times cadastrados </h2>

Nessa aplicação, o usuário sem fazer login ou se cadastrar, consegue visualizar os outros times já cadastrados na plataforma, na API podemos acesssar a lista da seguinte forma:

<!-- `GET /users - FORMATO DA RESPOSTA - STATUS 200`

```json
[
    {
      "email": "danone@email.com",
      "password": "$2a$10$1yak2vwsO2XTyMshwCkpBONT5X3Qr1KsJGWmYd9k6NlwFx9TyVdZy",
      "name": "Danone FC",
      "city": "Palhoça",
      "players": ["Cristiano", "Ronaldo", "Messi", "Neymar"],
      "url_image": "https://i.pinimg.com/564x/a2/df/be/a2dfbe8df09c969ec925b8cf1fa6ab47.jpg",
      "id": 1
    },
    {
      "email": "kenzieclub@kenzie.com",
      "password": "$2a$10$1yak2vwsO2XTyMshwCkpBONT5X3Qr1KsJGWmYd9k6NlwFx9TyVdZy",
      "name": "Danone FC",
      "city": "Palhoça",
      "players": ["Tsunode", "Wesley", "4lysson", "Vilson"],
      "url_image": "https://veja.abril.com.br/wp-content/uploads/2019/12/1.jpg",
      "id": 2
    }
]
``` -->

`GET /solutions - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "title": "Como tipar um useState",
    "content": {
      "text": "Para tipar um state é simples, basta...",
      "code": "useState('exemplo')"
    },
    "created_at": "31/08/2022",
    "updated_at": "31/08/2022",
    "tags": ["hooks"],
    "likes": 0,
    "userId": 1,
    "id": 1
  }
]
```

`GET /comments - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "id": 1,
    "userId": 1,
    "content": "...",
    "created_at": "...",
    "solutionId": 1
  }
]
```

`GET /users - FORMATO DA RESPOSTA - STATUS 200`

```json
[
  {
    "email": "kenzinho@mail.com",
    "password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
    "name": "Kenzinho",
    "github": "...",
    "contact?": "",
    "id": 1
  }
]
```

<h2 align ='center'> Criação de usuário </h2>
## Cadastro

`POST /register - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "kenzer@gmail.com",
  "password": "123456",
  "name": "Kenzinho",
  "github": "www.github.com/Kenzinho",
  "contact": "(11)99999-9999"
}
```

Caso o cadastro seja realizado de forma correta, a resposta será assim:

`POST /users - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6Im5hQGdtYWlsLmNvbSIsImlhdCI6MTY2MTk4ODQxMywiZXhwIjoxNjYxOTkyMDEzLCJzdWIiOiIyIn0.meRv3qYnZMkfjkTIAcN7IBR2diFzGg9gYt2EZWjHdqw",
	"user": {
		"email": "kenzer@gmail.com",
		"name": "Kenzinho",
		"github": "www.github.com/Kenzinho",
		"contact": "(11)99999-9999",
		"id": 2
	}
  }
}
```

<h2 align = "center"> Login </h2>

```json
{
  "email": "kenzer@gmail.com",
  "password": "123456"
}
```

Caso de tudo certo, a resposta será assim:

`POST /login - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImtlbnppbmhvQG1haWwuY29tIiwiaWF0IjoxNjYxOTg2MzM4LCJleHAiOjE2NjE5ODk5MzgsInN1YiI6IjEifQ.R1CTslLSJuSYBfSAYlkd6-Wvgci2ha0BapiBOtLCuAs",
  "user": {
    "email": "kenzer@gmail.com",
    "name": "Kenzinho",
    "github": "www.github.com/Kenzinho",
    "contact": "(11)99999-9999",
    "id": 2
  }
}
```

Com esta resposta, temos duas informações importantes, token e user, sendo que ambos podem ser guardados no localStorage para fazer a gestão do usuário no Frontend.

## Rotas que necessitam de autorização

Rotas que necessitam de autorização(token) deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<h2 align ='center'> Criar Solução </h2>

`POST /solutions - FORMATO DA REQUISIÇÃO`

```json
{
  {
      "title": "Como tipar uma function",
      "content": {
        "text": "...",
        "code": "..."
      },
      "created_at": "31/08/2022",
      "updated_at": "31/08/2022",
      "tags": ["function"],
      "likes": 0,
      "userId": 2
 }
}
```

`POST /solutions - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  {
	"title": "Como tipar uma function",
	"content": {
		"text": "...",
		"code": "..."
	},
	"created_at": "31/08/2022",
	"updated_at": "31/08/2022",
	"tags": ["function"],
	"likes": 0,
    "userId": 2,
	"id": 3
}
}
```

1. o campo - "tags" deve receber um, ou mais, dos seguintes tipos:

- "hooks"
- "function"
- "interface"
- -

2. o campo "userId": é o ID do usuário que estiver criando a solução.

<h2 align ='center'> Atualizando a solução </h2>

`PATCH /solutions/id (id do evento a ser editado) - FORMATO DA REQUISIÇÃO`

```json
{
  {
	"title": "Como tipar uma function - Editado",
	"content": {
		"text": "...",
		"code": "..."
	},
	"created_at": "31/08/2022",
	"updated_at": "31/08/2022",
	"tags": ["function"],
	"likes": 0,
	"userId": 2
}
}
```

`PATCH /solutions/id - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  {
	"title": "Como tipar uma function - Editado",
	"content": {
		"text": "...",
		"code": "..."
	},
	"created_at": "31/08/2022",
	"updated_at": "31/08/2022",
	"tags": ["function"],
	"userId": 2,
	"id": 3,
	"likes": 0
}
}
```

<h2 align ='center'> Deletando a solução </h2>

`DELETE /solutions/id (id do evento a ser editado) - Não é necessário passar corpo na requisição!`

<h2 align ='center'> Atualizando o usuário </h2>

`PATCH /users/id (id do Usuário a ser editado) - FORMATO DA REQUISIÇÃO`

```json
{
  "name": "Kenzinha",
  "github": "www.github.com/Kenzinha",
  "contact": "(99)11111-1111"
}
```

`PATCH /users/id (id do Usuário a ser editado) - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "email": "kenzer@gmail.com",
  "password": "$2a$10$NjRK6KkNGX.bT1Q9wYNxGO.fQv1z/L1f53G5YqZVGQmrZejoOCdbC",
  "name": "Kenzinha",
  "github": "www.github.com/Kenzinha",
  "contact": "(99)11111-1111",
  "id": 3
}
```

<h2 align ='center'> Deletando o Usuário</h2>

`Delete /users/id (id do Usuário a ser editado) - Não é necessário passar corpo na requisição!`

<h1>Escrito e criado por - team campeonateiros!! </h1>
