# json-server-ajude-meu-pet

Esse é o backend da aplicação Ajude meu Pet. O objetivo dessa API e conseguir criar usuários, pets e serviços.

## Endpoints

Esta API possui 4 endpoints diferentes.
Todas as rotas que necessitam de autenticação deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

Authorization: Bearer {token}

Sendo que o token, é o campo accessToken disponibilizado na resposta do endpoint /login. Nessa documentação é informado quando uma determinada rota precisa de autenticação.

O url base da API é https://json-server-ajude-meu-pet.herokuapp.com
<br/><br/>

### Register

POST /register

Endpoint usado para criar novo usuário.
Formato da requisição:

```json
{
  "name": "Kenzinho",
  "email": "kenzinho@mail.com",
  "phone": "(22)98729-9061",
  "password": "123456",
  "street": "Gen. Mário Tourinho",
  "addressNumber": "1733",
  "addressComplement": "706",
  "city": "Curitiba",
  "isClient": false
}
```

Formato da resposta - status 201

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImVtYWlsQG1haWwuY29tIiwiaWF0IjoxNjQyNTM5ODEwLCJleHAiOjE2NDI1NDM0MTAsInN1YiI6IjMifQ.iX1DtZ91DgvEX-Q04MjslAdr4iUZR6jp9SeXTSqcjjg",
  "user": {
    "name": "Kenzinho",
    "email": "kenzinho@mail.com",
    "phone": "(22)98729-9061",
    "password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
    "street": "Gen. Mário Tourinho",
    "addressNumber": "1733",
    "addressComplement": "706",
    "city": "Curitiba",
    "isClient": false,
    "id": 1
  }
}
```

<br/>

Formato da resposta - status 400

"Email already exists"

<br/><br/>

### Users

GET /users/:user_id

Endpoint usado para acessar um usuário específico. OBS: Essa rota precisa de autenticação

Formato da resposta - status 200

```json
{
  "email": "johndoe@mail.com",
  "password": "$2a$10$N/QQ5ePqtKPAZcJntBNScei8qfEkhwYCt9TIxEDOXxhYwmHUXFaPi",
  "name": "John Doe",
  "phone": "(44)99562-4420",
  "street": "Avenida das Américas",
  "addressNumber": "2345",
  "addressComplement": "bloco 1, ap 1508",
  "city": "Rio de Janeiro",
  "isClient": true,
  "id": 2
}
```

<br/>

### Login

POST /login

Endpoint usado para que o usuário faça o login.
Formato da requisição:

```json
{
  "email": "kenzinho@mail.com",
  "password": "123456"
}
```

Formato da resposta - status 200

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImtlbnppbmhvQG1haWwuY29tIiwiaWF0IjoxNjQyNTM5NTk5LCJleHAiOjE2NDI1NDMxOTksInN1YiI6IjEifQ.skWRK8WxOt-asoQ_Le-VIAQsUXVbkhXNsoNLWM2NHm0",
  "user": {
    "email": "kenzinho@mail.com",
    "name": "Kenzinho",
    "phone": "(41)977442211",
    "street": "Gen. Mário Tourinho",
    "addressNumber": "1733",
    "addressComplement": "706",
    "city": "Curitiba",
    "isClient": true,
    "id": 1
  }
}
```

<br/>

Formato da resposta - status 400

"Cannot find user"

ou

"Incorrect password"

<br/><br/>

## Pets

Endpoint usado para acessar todos os pets do seu usuário logado (você deve ter seu token passado como Bearer).

### Ver todos os pets:

GET /pets <br/><br/>

Formato da resposta - status 200

```json
[
  {
    "userId": 2,
    "petName": "Rex",
    "petType": "cachorro",
    "petBirthDate": "20/03/2018",
    "petGender": "male",
    "petSize": "grande",
    "id": 1
  },
  {
    "userId": 2,
    "petName": "Brabo",
    "petType": "cachorro",
    "petBirthDate": "05/11/2020",
    "petGender": "male",
    "petSize": "pequeno",
    "id": 2
  }
]
```

<br/>

### Adicionar pets:

POST /pets <br/><br/>
Formato de envio do JSON:

```json
{
  "userId": 2,
  "petName": "Pudim",
  "petType": "gato",
  "petBirthDate": "17/02/2018",
  "petGender": "male",
  "petSize": "médio"
}
```

Formato da resposta:

```json
{
  "userId": 2,
  "petName": "Pudim",
  "petType": "gato",
  "petBirthDate": "17/02/2018",
  "petGender": "male",
  "petSize": "médio",
  "id": 2
}
```

<br/>

### Atualizar pets:

PATCH /pets/:petId <br/><br/>
Formato de envio do JSON:

```json
{
  "petBirthDate": "06/11/2020"
}
```

Formato da resposta:

```json
{
  "userId": 2,
  "petName": "Brabo",
  "petType": "cachorro",
  "petBirthDate": "06/11/2020",
  "petGender": "male",
  "petSize": "pequeno",
  "id": 2
}
```

### Excluir pets:

DELETE /pets/:petId <br/>
Nota: não é necessário um corpo da requisição (JSON)
<br/><br/>

## Services

Endpoint usado para acessar os serviços para os seus pets (seu usuário deve estar logado e você deve passar seu token como Bearer).

### Ver todos os services:

GET /services <br/><br/>

Formato da resposta - status 200

```json
[
  {
    "servicesCategory": "adestramento",
    "servicesDescription": "básico",
    "servicesDesiredDate": "05/02/2022",
    "servicesDesiredTime": "09:30",
    "servicesObs": "Quero que meu cachorro aprenda a sentar",
    "servicesDepartureStreet": "Avenida das Américas",
    "servicesDepartureNumber": "2345",
    "servicesDepartureComplement": "bloco 1, ap 1508",
    "servicesDepartureCity": "Rio de Janeiro",
    "servicesArrivalStreet": "",
    "servicesArrivalNumber": "",
    "servicesArrivalComplement": "",
    "servicesArrivalCity": "",
    "serviceConclusion": false,
    "clientId": 2,
    "workerId": 1,
    "petId": 1,
    "id": 1
  },
  {
    "servicesCategory": "adestramento",
    "servicesDescription": "avançado",
    "servicesDesiredDate": "09/02/2022",
    "servicesDesiredTime": "10:30",
    "servicesObs": "",
    "servicesDepartureStreet": "Avenida das Américas",
    "servicesDepartureNumber": "2345",
    "servicesDepartureComplement": "bloco 1, ap 1508",
    "servicesDepartureCity": "Rio de Janeiro",
    "servicesArrivalStreet": "",
    "servicesArrivalNumber": "",
    "servicesArrivalComplement": "",
    "servicesArrivalCity": "",
    "serviceConclusion": false,
    "clientId": 2,
    "workerId": 1,
    "petId": 1,
    "id": 2
  }
]
```

<br/>

### Adicionar services:

POST /sevices <br/><br/>
Formato de envio do JSON:

```json
{
  "servicesCategory": "taxi",
  "servicesDescription": "",
  "servicesDesiredDate": "26/02/2022",
  "servicesDesiredTime": "12:00",
  "servicesObs": "Levar ao veterinário e informar que ela não se adaptou ao remédio",
  "servicesDepartureStreet": "Avenida das Américas",
  "servicesDepartureNumber": "2345",
  "servicesDepartureComplement": "bloco 1, ap 1508",
  "servicesDepartureCity": "Rio de Janeiro",
  "servicesArrivalStreet": "Rua Lúcio Costa",
  "servicesArrivalNumber": "245",
  "servicesArrivalComplement": "sala 502",
  "servicesArrivalCity": "Rio de Janeiro",
  "serviceConclusion": false,
  "clientId": 2,
  "workerId": null,
  "petId": 2,
}
```

Formato da resposta:

```json
{
  "servicesCategory": "taxi",
  "servicesDescription": "",
  "servicesDesiredDate": "26/02/2022",
  "servicesDesiredTime": "12:00",
  "servicesObs": "Levar ao veterinário e informar que ela não se adaptou ao remédio",
  "servicesDepartureStreet": "Avenida das Américas",
  "servicesDepartureNumber": "2345",
  "servicesDepartureComplement": "bloco 1, ap 1508",
  "servicesDepartureCity": "Rio de Janeiro",
  "servicesArrivalStreet": "Rua Lúcio Costa",
  "servicesArrivalNumber": "245",
  "servicesArrivalComplement": "sala 502",
  "servicesArrivalCity": "Rio de Janeiro",
  "serviceConclusion": false,
  "clientId": 2,
  "workerId": null,
  "petId": 2,
  "id": 2
}
```

### Atualizar pets:

PATCH /services/:serviceId <br/><br/>
Formato de envio do JSON:

```json
{
  "servicesDesiredDate": "10/02/2022"
}
```

Formato da resposta:

```json
{
  "servicesCategory": "adestramento",
  "servicesDescription": "básico",
  "servicesDesiredDate": "10/02/2022",
  "servicesDesiredTime": "09:30",
  "servicesObs": "Quero que meu cachorro aprenda a sentar",
  "servicesDepartureStreet": "Avenida das Américas",
  "servicesDepartureNumber": "2345",
  "servicesDepartureComplement": "bloco 1, ap 1508",
  "servicesDepartureCity": "Rio de Janeiro",
  "servicesArrivalStreet": "",
  "servicesArrivalNumber": "",
  "servicesArrivalComplement": "",
  "servicesArrivalCity": "",
  "serviceConclusion": false,
  "clientId": 2,
  "workerId": 1,
  "petId": 1,
  "id": 1
}
```

### Excluir service:

DELETE /services/:serviceId <br/>
Nota: não é necessário um corpo da requisição (JSON)
<br/><br/>

<br/><br/>

## Query Params

Para obter apenas os serviços de um determinado pet, deve-se usar os Query Params com a propriedade userId. Dessa forma a requisição seria:

GET /services/?petId=:pet_id

OBS: Essa rota precisa de autenticação.
Formato da resposta - status 200

```json
[
  {
    "servicesCategory": "adestramento",
    "servicesDescription": "básico",
    "servicesDesiredDate": "05/02/2022",
    "servicesDesiredTime": "09:30",
    "servicesObs": "Quero que meu cachorro aprenda a sentar",
    "servicesDepartureStreet": "Avenida das Américas",
    "servicesDepartureNumber": "2345",
    "servicesDepartureComplement": "bloco 1, ap 1508",
    "servicesDepartureCity": "Rio de Janeiro",
    "servicesArrivalStreet": "",
    "servicesArrivalNumber": "",
    "servicesArrivalComplement": "",
    "servicesArrivalCity": "",
    "serviceConclusion": false,
    "clientId": 2,
    "workerId": 1,
    "petId": 1,
    "id": 1
  },
  {
    "servicesCategory": "adestramento",
    "servicesDescription": "avançado",
    "servicesDesiredDate": "09/02/2022",
    "servicesDesiredTime": "10:30",
    "servicesObs": "",
    "servicesDepartureStreet": "Avenida das Américas",
    "servicesDepartureNumber": "2345",
    "servicesDepartureComplement": "bloco 1, ap 1508",
    "servicesDepartureCity": "Rio de Janeiro",
    "servicesArrivalStreet": "",
    "servicesArrivalNumber": "",
    "servicesArrivalComplement": "",
    "servicesArrivalCity": "",
    "serviceConclusion": false,
    "clientId": 2,
    "workerId": 1,
    "petId": 1,
    "id": 2
  }
]
```
