# json-server-hamburgueria

Esse é o backend da aplicação Hamburgueria 2.0. O objetivo dessa API e conseguir criar usuários, produtos e compras. 

## Endpoints

Nessa entrega serão utilizados 6 endpoints diferentes.
Todas as rotas que necessitam de autenticação deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

Authorization: Bearer {token}

Sendo que o token, é o campo accessToken disponibilizado na resposta do endpoint /login. Nessa documentação é informado quando uma determinada rota precisa de autenticação.

O url base da API é https://json-server-hamburgueria-doriv.herokuapp.com


### Login

POST /login

Endpoint usado para que o usuário faça o login.
Formato da requisição: 

{

	"email": "kenzinho@mail.com",
	"password": "123456"
}

Formato da resposta - status 200

{

  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImtlbnppbmhvQG1haWwuY29tIiwiaWF0IjoxNjQyNTM5NTk5LCJleHAiOjE2NDI1NDMxOTksInN1YiI6IjEifQ.skWRK8WxOt-asoQ_Le-VIAQsUXVbkhXNsoNLWM2NHm0",

  "user": {

    "email": "kenzinho@mail.com",
    "name": "Kenzinho",
    "id": 1
  }

}

### Users

POST /users

Endpoint usado para criar novo usuário.
Formato da requisição: 

{

	"name": "johndoe",
	"email": "email@mail.com",
	"password": "123456"
}

Formato da resposta - status 201

{

  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImVtYWlsQG1haWwuY29tIiwiaWF0IjoxNjQyNTM5ODEwLCJleHAiOjE2NDI1NDM0MTAsInN1YiI6IjMifQ.iX1DtZ91DgvEX-Q04MjslAdr4iUZR6jp9SeXTSqcjjg",
  "user": {

    "email": "email@mail.com",
    "name": "johndoe",
    "id": 3
  }

}

Formato da resposta - status 400

"Email already exists"


GET /users/:user_id

Endpoint usado para acessar um usuário específico. OBS: Essa rota precisa de autenticação

Formato da resposta - status 200

{

  "email": "kenzinho@mail.com",
  "password": "$2a$10$YQiiz0ANVwIgpOjYXPxc0O9H2XeX3m8OoY1xk7OGgxTnOJnsZU7FO",
  "name": "Kenzinho",
  "age": 38,
  "id": 1

}

### Products

GET /products

Endpoint usado para acessar todos os produtos da API. 

Formato da resposta - status 200

[
  {

    "name": "Hamburguer",
    "category": "Sanduíches",
    "imageUrl": "https://s3-alpha-sig.figma.com/img/bb0c/a182/55225f534ef7e57de0892c7de864a767?Expires=1643587200&Signature=MJaZTwJvTkU1m9XDdDkkd1mADOdLvU6BdstFnwH62d-PAillRvYRFBI8mZ~yUv5ltHm6TNRPnHEOcz90GwtMXEe~pILUrQgMWVqj8Vv7C8soczZPKBl6D1m54wVs~GdyVwBk2bc76xy4dqPNiOuy5jmgG0EX3XjcWDmnjerwfbLpOQzi9rs1BN4Xcq6q4X4uK-1y7TUD7KqUstdv7YlScxmuwW0MRVM0MXt6kpY3FyA8h4hx~py0QCyQ5hsCqQIig0v~skFChTzy3MUHq1WXbRibwNrBPnAKsyKkBzkvZ8qmLx34DCrqXFrfyL53RpymcRw9v7CDYr8rRJh4VDhrSQ__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
    "price": 14,
    "userId": 1,
    "id": 1

  },
  {

    "name": "X-Burguer",
    "category": "Sanduíches",
    "imageUrl": "https://s3-alpha-sig.figma.com/img/a31b/2c16/9de750feaf42d98ebd46941dad1f6afd?Expires=1643587200&Signature=QN~bRrGRGN~bXakqk7pwTgE6al3TS5IxYYs10b1t4C7UW9zv8BJWXNfFBOuUA0-ik3cnwQCI0C8CVkoX5zDjjdjue-3kLnISTMJqT1TISEkMMQVGCqDbzeUmB0xmsswM5JHoMrcI~mFA2oYSR4TDFkhjdBgcgVckM7u900xCdT8eD17OA0GctBuc2p9dVukppAHreqW0LncgsAuWiq2Xyq7aM9x2qoE6V8gwwRWLWssjHrfuL1f4nrpgI7Ia0xqazRcnBrQtkEBo5~lFwOfTK1eijPZqKC1An6jFmWwXyg-KBUmb01ixBjvebJN4WB2cHPeOPaBwAv4TLi6E7nceFA__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
    "price": 16,
    "userId": 1,
    "id": 2
  }
]

### Purchase

GET /purchases

Endpoint usado para acessar todos as compras da API. OBS: Essa rota precisa de autenticação

Formato da resposta - status 200

[
  {

    "products": [
      {
        "name": "Hamburguer",
        "category": "Sanduíches",
        "imageUrl": "https://s3-alpha-sig.figma.com/img/bb0c/a182/55225f534ef7e57de0892c7de864a767?Expires=1643587200&Signature=MJaZTwJvTkU1m9XDdDkkd1mADOdLvU6BdstFnwH62d-PAillRvYRFBI8mZ~yUv5ltHm6TNRPnHEOcz90GwtMXEe~pILUrQgMWVqj8Vv7C8soczZPKBl6D1m54wVs~GdyVwBk2bc76xy4dqPNiOuy5jmgG0EX3XjcWDmnjerwfbLpOQzi9rs1BN4Xcq6q4X4uK-1y7TUD7KqUstdv7YlScxmuwW0MRVM0MXt6kpY3FyA8h4hx~py0QCyQ5hsCqQIig0v~skFChTzy3MUHq1WXbRibwNrBPnAKsyKkBzkvZ8qmLx34DCrqXFrfyL53RpymcRw9v7CDYr8rRJh4VDhrSQ__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        "price": 14,
        "quantity": 2,
        "userId": 1,
        "id": 1
      },
      {
        "name": "Fanta Guaraná",
        "category": "Bebidas",
        "imageUrl": "https://s3-alpha-sig.figma.com/img/60f1/9a01/e0f45751b040264e27bff533cd98a9fa?Expires=1643587200&Signature=XCPJ8Iw5phIPR~ZkPxjpHmfbw7jSb4~cTr5DEy0zyC8ZqLq8CL8kWGmKyuz1SkRriU3z7bg1G2eRzdrUDzwO0qVYK2AwaykmlTO4PfjP41m5gitIcARdKdbR08qM~B5wM-bdVigbzDK6LyGNw9EI3inbm9eeRCrwGm8wOLuCVdaMVuTeY2NrWCjPHNC0EFxuB809UVTf6YDfjKjN8QWYNp1oiQ1jbhtZN2u1m9tk66s-rcWfHKGQnoa19zYu4o84mU~DP4rFlNV4D6T9Bknvl3xI~rTwKxlsR~Cyru4nP0Ox5bw7GFGFu3PKuRg2evKxzaCV6SUW7gbVAvXBja1oDg__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        "price": 5,
        "quantity": 1,
        "userId": 1,
        "id": 5
      },
      {
        "name": "Coca Cola",
        "category": "Bebidas",
        "imageUrl": "https://s3-alpha-sig.figma.com/img/2bc5/898e/0066008c52d555a980ec793bcaf8317f?Expires=1643587200&Signature=eejehZ8tR5iNhpM6nxpgO~yFDSRElUnQKjB9H4CjDR~hSxKh6P9UDEeEHnlRxS7L3wHzcqlMomAUBDCiIUVbHL3iYnDnXwNeBGAIVxRZQ3VAdB~tko~0OlOy0xJc-c2k1ZIoQlh5GVAVymF3khsenzokJtn7JhRrgOosF4rhZWcMROLiQOya84DSpq~5AS954eQfb3lMkgn32NR~jJJkwpg8FvskNcm2~cuPen9CCta6LQnKG~h-M-sbuETl3aXV~zfL2lIjk8EHU10kiM7J2xgyGmShgOvI9s8WJgt59rP~qZ-Y5DTlsQJ8IndqurWj8Odv4w3xqJhgOzskInb95w__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        "price": 7,
        "quantity": 1,
        "userId": 1,
        "id": 6
      }
    ],
    "total": 40,
    "id": 1,
    "userId": 1
  },
  {
      
    "products": [
      {
        "name": "Hamburguer",
        "category": "Sanduíches",
        "imageUrl": "https://s3-alpha-sig.figma.com/img/bb0c/a182/55225f534ef7e57de0892c7de864a767?Expires=1643587200&Signature=MJaZTwJvTkU1m9XDdDkkd1mADOdLvU6BdstFnwH62d-PAillRvYRFBI8mZ~yUv5ltHm6TNRPnHEOcz90GwtMXEe~pILUrQgMWVqj8Vv7C8soczZPKBl6D1m54wVs~GdyVwBk2bc76xy4dqPNiOuy5jmgG0EX3XjcWDmnjerwfbLpOQzi9rs1BN4Xcq6q4X4uK-1y7TUD7KqUstdv7YlScxmuwW0MRVM0MXt6kpY3FyA8h4hx~py0QCyQ5hsCqQIig0v~skFChTzy3MUHq1WXbRibwNrBPnAKsyKkBzkvZ8qmLx34DCrqXFrfyL53RpymcRw9v7CDYr8rRJh4VDhrSQ__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        "price": 14,
        "quantity": 1,
        "userId": 1,
        "id": 1
      },
      {
        "name": "Coca Cola",
        "category": "Bebidas",
        "imageUrl": "https://s3-alpha-sig.figma.com/img/2bc5/898e/0066008c52d555a980ec793bcaf8317f?Expires=1643587200&Signature=eejehZ8tR5iNhpM6nxpgO~yFDSRElUnQKjB9H4CjDR~hSxKh6P9UDEeEHnlRxS7L3wHzcqlMomAUBDCiIUVbHL3iYnDnXwNeBGAIVxRZQ3VAdB~tko~0OlOy0xJc-c2k1ZIoQlh5GVAVymF3khsenzokJtn7JhRrgOosF4rhZWcMROLiQOya84DSpq~5AS954eQfb3lMkgn32NR~jJJkwpg8FvskNcm2~cuPen9CCta6LQnKG~h-M-sbuETl3aXV~zfL2lIjk8EHU10kiM7J2xgyGmShgOvI9s8WJgt59rP~qZ-Y5DTlsQJ8IndqurWj8Odv4w3xqJhgOzskInb95w__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        "price": 7,
        "quantity": 1,
        "userId": 1,
        "id": 6
      }
    ],
    "total": 21,
    "id": 2,
    "userId": 2
  }
]

Para obter apenas as compras de um determinado usuário, deve-se usar os Query Params com a propriedade userId. Dessa forma a requisição seria:

GET /purchases/?userId=:user_id

OBS: Essa rota precisa de autenticação.
Formato da resposta - status 200

[
  {

    "products": [
      {
        "name": "Hamburguer",
        "category": "Sanduíches",
        "imageUrl": "https://s3-alpha-sig.figma.com/img/bb0c/a182/55225f534ef7e57de0892c7de864a767?Expires=1643587200&Signature=MJaZTwJvTkU1m9XDdDkkd1mADOdLvU6BdstFnwH62d-PAillRvYRFBI8mZ~yUv5ltHm6TNRPnHEOcz90GwtMXEe~pILUrQgMWVqj8Vv7C8soczZPKBl6D1m54wVs~GdyVwBk2bc76xy4dqPNiOuy5jmgG0EX3XjcWDmnjerwfbLpOQzi9rs1BN4Xcq6q4X4uK-1y7TUD7KqUstdv7YlScxmuwW0MRVM0MXt6kpY3FyA8h4hx~py0QCyQ5hsCqQIig0v~skFChTzy3MUHq1WXbRibwNrBPnAKsyKkBzkvZ8qmLx34DCrqXFrfyL53RpymcRw9v7CDYr8rRJh4VDhrSQ__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        "price": 14,
        "quantity": 2,
        "userId": 1,
        "id": 1
      },
      {
        "name": "Fanta Guaraná",
        "category": "Bebidas",
        "imageUrl": "https://s3-alpha-sig.figma.com/img/60f1/9a01/e0f45751b040264e27bff533cd98a9fa?Expires=1643587200&Signature=XCPJ8Iw5phIPR~ZkPxjpHmfbw7jSb4~cTr5DEy0zyC8ZqLq8CL8kWGmKyuz1SkRriU3z7bg1G2eRzdrUDzwO0qVYK2AwaykmlTO4PfjP41m5gitIcARdKdbR08qM~B5wM-bdVigbzDK6LyGNw9EI3inbm9eeRCrwGm8wOLuCVdaMVuTeY2NrWCjPHNC0EFxuB809UVTf6YDfjKjN8QWYNp1oiQ1jbhtZN2u1m9tk66s-rcWfHKGQnoa19zYu4o84mU~DP4rFlNV4D6T9Bknvl3xI~rTwKxlsR~Cyru4nP0Ox5bw7GFGFu3PKuRg2evKxzaCV6SUW7gbVAvXBja1oDg__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        "price": 5,
        "quantity": 1,
        "userId": 1,
        "id": 5
      },
      {
        "name": "Coca Cola",
        "category": "Bebidas",
        "imageUrl": "https://s3-alpha-sig.figma.com/img/2bc5/898e/0066008c52d555a980ec793bcaf8317f?Expires=1643587200&Signature=eejehZ8tR5iNhpM6nxpgO~yFDSRElUnQKjB9H4CjDR~hSxKh6P9UDEeEHnlRxS7L3wHzcqlMomAUBDCiIUVbHL3iYnDnXwNeBGAIVxRZQ3VAdB~tko~0OlOy0xJc-c2k1ZIoQlh5GVAVymF3khsenzokJtn7JhRrgOosF4rhZWcMROLiQOya84DSpq~5AS954eQfb3lMkgn32NR~jJJkwpg8FvskNcm2~cuPen9CCta6LQnKG~h-M-sbuETl3aXV~zfL2lIjk8EHU10kiM7J2xgyGmShgOvI9s8WJgt59rP~qZ-Y5DTlsQJ8IndqurWj8Odv4w3xqJhgOzskInb95w__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
        "price": 7,
        "quantity": 1,
        "userId": 1,
        "id": 6
      }
    ],
    "total": 40,
    "id": 1,
    "userId": 1
  }
  
]

POST /purchases

Endpoint usado para criar a compra do usuário. OBS: Essa rota precisa de autenticação.

Formato da requisição:

{

	"products": [
        {
          "name": "Hamburguer",
          "category": "Sanduíches",
          "imageUrl": "https://s3-alpha-sig.figma.com/img/bb0c/a182/55225f534ef7e57de0892c7de864a767?Expires=1643587200&Signature=MJaZTwJvTkU1m9XDdDkkd1mADOdLvU6BdstFnwH62d-PAillRvYRFBI8mZ~yUv5ltHm6TNRPnHEOcz90GwtMXEe~pILUrQgMWVqj8Vv7C8soczZPKBl6D1m54wVs~GdyVwBk2bc76xy4dqPNiOuy5jmgG0EX3XjcWDmnjerwfbLpOQzi9rs1BN4Xcq6q4X4uK-1y7TUD7KqUstdv7YlScxmuwW0MRVM0MXt6kpY3FyA8h4hx~py0QCyQ5hsCqQIig0v~skFChTzy3MUHq1WXbRibwNrBPnAKsyKkBzkvZ8qmLx34DCrqXFrfyL53RpymcRw9v7CDYr8rRJh4VDhrSQ__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
          "price": 14,
          "quantity": 2,
          "userId": 1,
          "id": 1
        },
        {
          "name": "Fanta Guaraná",
          "category": "Bebidas",
          "imageUrl": "https://s3-alpha-sig.figma.com/img/60f1/9a01/e0f45751b040264e27bff533cd98a9fa?Expires=1643587200&Signature=XCPJ8Iw5phIPR~ZkPxjpHmfbw7jSb4~cTr5DEy0zyC8ZqLq8CL8kWGmKyuz1SkRriU3z7bg1G2eRzdrUDzwO0qVYK2AwaykmlTO4PfjP41m5gitIcARdKdbR08qM~B5wM-bdVigbzDK6LyGNw9EI3inbm9eeRCrwGm8wOLuCVdaMVuTeY2NrWCjPHNC0EFxuB809UVTf6YDfjKjN8QWYNp1oiQ1jbhtZN2u1m9tk66s-rcWfHKGQnoa19zYu4o84mU~DP4rFlNV4D6T9Bknvl3xI~rTwKxlsR~Cyru4nP0Ox5bw7GFGFu3PKuRg2evKxzaCV6SUW7gbVAvXBja1oDg__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
          "price": 5,
          "quantity": 1,
          "userId": 1,
          "id": 5
        },
        {
          "name": "Coca Cola",
          "category": "Bebidas",
          "imageUrl": "https://s3-alpha-sig.figma.com/img/2bc5/898e/0066008c52d555a980ec793bcaf8317f?Expires=1643587200&Signature=eejehZ8tR5iNhpM6nxpgO~yFDSRElUnQKjB9H4CjDR~hSxKh6P9UDEeEHnlRxS7L3wHzcqlMomAUBDCiIUVbHL3iYnDnXwNeBGAIVxRZQ3VAdB~tko~0OlOy0xJc-c2k1ZIoQlh5GVAVymF3khsenzokJtn7JhRrgOosF4rhZWcMROLiQOya84DSpq~5AS954eQfb3lMkgn32NR~jJJkwpg8FvskNcm2~cuPen9CCta6LQnKG~h-M-sbuETl3aXV~zfL2lIjk8EHU10kiM7J2xgyGmShgOvI9s8WJgt59rP~qZ-Y5DTlsQJ8IndqurWj8Odv4w3xqJhgOzskInb95w__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
          "price": 7,
          "quantity": 1,
          "userId": 1,
          "id": 6
        }
      ],
      "total": 40,
      "userId": 1
}

Formato da resposta - status 201:

{
    
  "products": [
    {
      "name": "Hamburguer",
      "category": "Sanduíches",
      "imageUrl": "https://s3-alpha-sig.figma.com/img/bb0c/a182/55225f534ef7e57de0892c7de864a767?Expires=1643587200&Signature=MJaZTwJvTkU1m9XDdDkkd1mADOdLvU6BdstFnwH62d-PAillRvYRFBI8mZ~yUv5ltHm6TNRPnHEOcz90GwtMXEe~pILUrQgMWVqj8Vv7C8soczZPKBl6D1m54wVs~GdyVwBk2bc76xy4dqPNiOuy5jmgG0EX3XjcWDmnjerwfbLpOQzi9rs1BN4Xcq6q4X4uK-1y7TUD7KqUstdv7YlScxmuwW0MRVM0MXt6kpY3FyA8h4hx~py0QCyQ5hsCqQIig0v~skFChTzy3MUHq1WXbRibwNrBPnAKsyKkBzkvZ8qmLx34DCrqXFrfyL53RpymcRw9v7CDYr8rRJh4VDhrSQ__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
      "price": 14,
      "quantity": 2,
      "userId": 1,
      "id": 1
    },
    {
      "name": "Fanta Guaraná",
      "category": "Bebidas",
      "imageUrl": "https://s3-alpha-sig.figma.com/img/60f1/9a01/e0f45751b040264e27bff533cd98a9fa?Expires=1643587200&Signature=XCPJ8Iw5phIPR~ZkPxjpHmfbw7jSb4~cTr5DEy0zyC8ZqLq8CL8kWGmKyuz1SkRriU3z7bg1G2eRzdrUDzwO0qVYK2AwaykmlTO4PfjP41m5gitIcARdKdbR08qM~B5wM-bdVigbzDK6LyGNw9EI3inbm9eeRCrwGm8wOLuCVdaMVuTeY2NrWCjPHNC0EFxuB809UVTf6YDfjKjN8QWYNp1oiQ1jbhtZN2u1m9tk66s-rcWfHKGQnoa19zYu4o84mU~DP4rFlNV4D6T9Bknvl3xI~rTwKxlsR~Cyru4nP0Ox5bw7GFGFu3PKuRg2evKxzaCV6SUW7gbVAvXBja1oDg__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
      "price": 5,
      "quantity": 1,
      "userId": 1,
      "id": 5
    },
    {
      "name": "Coca Cola",
      "category": "Bebidas",
      "imageUrl": "https://s3-alpha-sig.figma.com/img/2bc5/898e/0066008c52d555a980ec793bcaf8317f?Expires=1643587200&Signature=eejehZ8tR5iNhpM6nxpgO~yFDSRElUnQKjB9H4CjDR~hSxKh6P9UDEeEHnlRxS7L3wHzcqlMomAUBDCiIUVbHL3iYnDnXwNeBGAIVxRZQ3VAdB~tko~0OlOy0xJc-c2k1ZIoQlh5GVAVymF3khsenzokJtn7JhRrgOosF4rhZWcMROLiQOya84DSpq~5AS954eQfb3lMkgn32NR~jJJkwpg8FvskNcm2~cuPen9CCta6LQnKG~h-M-sbuETl3aXV~zfL2lIjk8EHU10kiM7J2xgyGmShgOvI9s8WJgt59rP~qZ-Y5DTlsQJ8IndqurWj8Odv4w3xqJhgOzskInb95w__&Key-Pair-Id=APKAINTVSUGEWH5XD5UA",
      "price": 7,
      "quantity": 1,
      "userId": 1,
      "id": 6
    }
  ],
  "total": 40,
  "userId": 1,
  "id": 4
}