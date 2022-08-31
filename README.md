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

<h2 align ='center'> Criação de usuário </h2>
### Cadastro

`POST /register - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "danone@email.com",
  "password": "123456",
  "name": "Danone FC",
  "city": "Palhoça"
}
```

Caso o cadastro seja feito de forma correta, a resposta será assim:

`POST /users - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImRhbm9uZUBlbWFpbC5jb20iLCJpYXQiOjE2NjE5MDA2NjAsImV4cCI6MTY2MTkwNDI2MCwic3ViIjoiMiJ9.ZlkLFQiR3QFk4p-g0e4CNxh-fVfudgGZ0i8JVkFUPVs",
  "user": {
    "email": "danone@email.com",
    "name": "Danone FC",
    "city": "Palhoça",
    "id": 2
  }
}
```

1. O campo "city": deve receber a cidade de origem do time cadastrado.

<h2 align = "center"> Login </h2>

```json
{
  "email": "danone@email.com",
  "password": "123456"
}
```

Caso de tudo certo, a resposta será assim:

`POST /login - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImRhbm9uZUBlbWFpbC5jb20iLCJpYXQiOjE2NjE5MDY0NTEsImV4cCI6MTY2MTkxMDA1MSwic3ViIjoiMSJ9.xH2G55cvVVoIf6oKF10bgG-vmuUyBfBfNeYQebxtnT0",
  "user": {
    "email": "danone@email.com",
    "name": "Danone FC",
    "city": "Palhoça",
    "players": ["Cristiano", "Ronaldo", "Messi", "Neymar"],
    "url_image": "https://i.pinimg.com/564x/a2/df/be/a2dfbe8df09c969ec925b8cf1fa6ab47.jpg",
    "id": 1
  }
}
```

Com esta resposta, temos duas informações importantes, token e user, sendo que ambos podem ser guardados no localStorage para fazer a gestão do usuario no Frontend.

## Rotas que necessitam de autorização

Rotas que necessitam de autorização(token) deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

<h2 align ='center'> Criar Evento (token) </h2>

`Post /events - FORMATO DA REQUISIÇÃO`

```json
{
  "category": "FUTEBOL",
  "userId": 2,
  "name": "Torneio da Galera",
  "localization": "Ginásio Nazareno - Palhoça/sc",
  "date-start": "30/08/2022",
  "date-end": "30/08/2022"
}
```

`Post /events - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "category": "FUTEBOL",
  "userId": 2,
  "name": "Torneio da Galera",
  "localization": "Ginásio Nazareno - Palhoça/sc",
  "date-start": "30/08/2022",
  "date-end": "30/08/2022",
  "id": 2
}
```

1. o campo - "category" deve receber respectivamente os sequintes tipos de evento:

- "Futebol"
- "Voleibol"
- "Basquete"

2. o campo "userId": é o ID do usuário que estiver criando o evento, pois somente ele consegue adicionar informações relacionados ao evento.

<h2 align ='center'> Atualizando o Evento (token) </h2>

`Patch /events/id (id do evento a ser editado) - FORMATO DA REQUISIÇÃO`

```json
{
  "image": "",
  "informations": [
    {
      "Inscrição": "R$ 100,00",
      "Premiações": "Troféu e medalha para 1° e 2° lugar",
      "Quantidade": "Limite de 12 times participantes",
      "Localização": "Esquina do bar Madalena"
    }
  ],
  "teams": ["Danone FC", "Gueto FC", "Galaticos"]
}
```

`Patch /events - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "category": "Futebol",
  "userId": 3,
  "name": "Copa doss cria",
  "localization": "Morro do alemão",
  "date-start": "03/09/2022",
  "date-end": "03/09/2022",
  "id": 2,
  "informations": [
    {
      "Inscrição": "R$ 100,00",
      "Premiações": "Troféu e medalha para 1° e 2° lugar",
      "Quantidade": "Limite de 12 times participantes",
      "Localização": "Esquina do bar Madalena"
    }
  ],
  "teams": ["Danone FC", "Gueto FC", "Galaticos"]
}
```

1. O campo "informations": deve receber um objeto com as seguintes informações:

- "Inscrição" - valor da inscrição do evento
- "Premiações" - quais são as premiações
- "Quantidade" - limite de participantes
- "Localização" - endereço do evento

2. O campo "teams" - recebe um array dos times que estão participando do evento!

<h2 align ='center'> Deletando o Evento (token) </h2>

`Delete /events/id (id do evento a ser editado) - Não é necessário passar corpo na requisição!`

<h2 align ='center'> Atualizando o usuário (token) </h2>

`Patch /users/id (id do Usuário a ser editado) - FORMATO DA REQUISIÇÃO`

```json
{
  "players": ["Zezin", "Anão", "Canhotin", "Vissoto"],
  "url_image": "https://thumbs.dreamstime.com/z/ilustra%C3%A7%C3%A3o-do-vetor-da-silhueta-bola-voleibol-isolada-no-branco-119929868.jpg"
}
```

`Patch /users/id (id do Usuário a ser editado) - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "email": "canela@mail.com",
  "password": "$2a$10$l7lutElDxqAexWlpmo.OjeiI26h2fILW8rrGlW0B18YY3Xa3BjBVa",
  "name": "Só canela FC",
  "city": "São Paulo",
  "id": 3,
  "players": ["Zezin", "Anão", "Canhotin", "Vissoto"],
  "url_image": ""
}
```

<h2 align ='center'> Deletando o Usuário (token) </h2>

`Delete /users/id (id do Usuário a ser editado) - Não é necessário passar corpo na requisição!`

<h1>Escrito e criado por - team campeonateiros!! </h1>
