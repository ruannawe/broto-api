# Broto api staging [swagger](https://mcstaging.broto.com.br/swagger)


## Autenticação (Fabricante e Revenda)

[integrationAdminTokenServiceV1CreateAdminAccessTokenPost](https://mcstaging.broto.com.br/swagger#/integrationAdminTokenServiceV1/integrationAdminTokenServiceV1CreateAdminAccessTokenPost)

Clique em `Try it out`, coloque seu usuário e senha conforme o exemplo abaixo e por fim clique em `Execute`.

``` json
{
  "username": "seu usuário",
  "password": "sua senha"
}
```

Autêntica usuário por meio de login e senha e retorna um token para colocar no header da página do swagger. Confira no exemplo abaixo:

![](https://i.imgur.com/BCH4wnL.png)


## Cotações

### Listar todas as cotações

[webjumpMultisellerDropshipApiNegotiableQuoteServiceV1GetListGet](https://mcstaging.broto.com.br/swagger#/webjumpMultisellerDropshipApiNegotiableQuoteServiceV1/webjumpMultisellerDropshipApiNegotiableQuoteServiceV1GetListGet)

Clique em `Try it out` e depois em `Execute`.

**Essa requisição não precisa de nenhum parâmetro**

Retorna uma lista com todas as cotações associadas ao fabricante ou a revenda, dependendo de qual usuário estiver logado. Confira o exemplo de retorno abaixo:

``` json
[
  {
    "vendor_quote_id": "584",
    "udropship_vendor": "5",
    "status": "Nova solicitação",
    "quote_id": "4040",
    "product_sku": "JD0083-1",
    "product_name": "Trator 3 - Teste",
    "product_id": "4015",
    "customer_email": "jlmonroy24@gmail.com",
    "customer_firstname": "Jeferson Luis",
    "customer_lastname": "Monroy"
  }
]
```

Para deixar essa documentação mais objetiva, a partir desse ponto vou omitir os passos que descrevem o clique em `Try it out` e `Execute`.


### Listar uma cotação
 [webjumpMultisellerDropshipApiNegotiableQuoteServiceV1FindGet](https://mcstaging.broto.com.br/swagger#/webjumpMultisellerDropshipApiNegotiableQuoteServiceV1/webjumpMultisellerDropshipApiNegotiableQuoteServiceV1FindGet)

Preencher o parâmetro `quoteId` com o `id` da cotação.

Retorna a cotação especificada no `id`. Confira o exemplo de retorno abaixo:

``` json
{
  "street": "Rua Padre Aníbal Difrância\n33\nJardim Mangalot\nApto 10",
  "city": "São Paulo",
  "region": "São Paulo",
  "postcode": "05135160",
  "country_id": "BR",
  "telephone": "(11)97616-0727",
  "email": "jlmonroy24@gmail.com",
  "vendor_quote_id": "584",
  "udropship_vendor": "5",
  "status": "Nova solicitação",
  "quote_id": "4040",
  "product_sku": "JD0083-1",
  "product_name": "Trator 3 - Teste",
  "product_id": "4015",
  "customer_email": "jlmonroy24@gmail.com",
  "customer_firstname": "Jeferson Luis",
  "customer_lastname": "Monroy"
}
```

### Associar cotação com revenda

[webjumpMultisellerDropshipApiNegotiableQuoteServiceV1AssignPost](https://mcstaging.broto.com.br/swagger#/webjumpMultisellerDropshipApiNegotiableQuoteServiceV1/webjumpMultisellerDropshipApiNegotiableQuoteServiceV1AssignPost)

Atualmente já existe uma auto associação da cotação com a revenda, caso a mesma esteja associada com a região que a cotação foi solicitada. Caso a cotação tenha sido feita para uma região onde não existe revenda cadastrada, existe a possibilidade de associar a cotação com uma revenda manualmente. Operação não permitida para usuários com perfil revenda.

Preencher json com `quoteId` e `subVendorId` para fazer a associação
``` json
{
  "quoteId": "string",
  "subVendorId": "string"
}
```

Resposta da api em caso de sucesso
``` json
{
  "vendor_quote_id": "string",
  "udropship_vendor": "string",
  "status": "string",
  "quote_id": "string",
  "product_sku": "string",
  "product_name": "string",
  "product_id": "string",
  "customer_email": "string",
  "customer_firstname": "string",
  "customer_lastname": "string"
}
```

### Responder uma cotação

[webjumpMultisellerDropshipApiNegotiableQuoteServiceV1SendCommentPost](https://mcstaging.broto.com.br/swagger#/webjumpMultisellerDropshipApiNegotiableQuoteServiceV1/webjumpMultisellerDropshipApiNegotiableQuoteServiceV1SendCommentPost)

Preencher o campo `quoteId` para informar qual cotação está sendo respondida. No corpo da requisição na chave `comment` informar qual é o comentário que deve ser enviado. Segue exemplo abaixo.

``` json
{
  "comment": "string"
}
```

Resposta em caso de sucesso

``` json
{
  "entity_id": 4900,
  "parent_id": 4040,
  "creator_type": 10,
  "is_decline": 0,
  "is_draft": 0,
  "creator_id": 5,
  "comment": "Novo comentário 06/05/2021",
  "created_at": "2021-05-06 15:22:17",
  "attachments": null
}
```

### Listar os comentários da cotação

[webjumpMultisellerDropshipApiNegotiableQuoteServiceV1GetQuoteCommentsGet](https://mcstaging.broto.com.br/swagger#/webjumpMultisellerDropshipApiNegotiableQuoteServiceV1/webjumpMultisellerDropshipApiNegotiableQuoteServiceV1GetQuoteCommentsGet)

Preencher o campo `quoteId` para informar de qual cotação os comentários serão listados.

Resposta da requisição
``` json
[
  {
    "entity_id": 284,
    "parent_id": 4040,
    "creator_type": 3,
    "is_decline": 0,
    "is_draft": 0,
    "creator_id": 49,
    "comment": "Teste Review",
    "created_at": "2020-12-14 17:22:17",
    "attachments": []
  }
]
```


### Enviar proposta para uma cotação

[webjumpMultisellerDropshipApiNegotiableQuoteServiceV1SendProposalToCustomerPost](https://mcstaging.broto.com.br/swagger#/webjumpMultisellerDropshipApiNegotiableQuoteServiceV1/webjumpMultisellerDropshipApiNegotiableQuoteServiceV1SendProposalToCustomerPost)

Preencher o campo `quoteId`, `quotePrice` referente ao preço da proposta, e informar no campo `quoteFile` os dados do arquivo que está sendo enviado. Sempre prefira enviar a proposta no arquivo PDF conforme o exemplo abaixo.

``` json
{
  "quoteId": "8101",
  "quotePrice": 100,
  "quoteFile": [
    {
      "base64_encoded_data": "JVBERi0xLjMNCiXi48/TDQoNCjEgMCBvYmoNCjw8DQovVHlwZSAvQ2F0YWxvZw0KL091dGxpbmVzIDIgMCBSDQovUGFnZXMgMyAwIFINCj4+DQplbmRvYmoNCg0KMiAwIG9iag0KPDwNCi9UeXBlIC9PdXRsaW5lcw0KL0NvdW50IDANCj4+DQplbmRvYmoNCg0KMyAwIG9iag0KPDwNCi9UeXBlIC9QYWdlcw0KL0NvdW50IDINCi9LaWRzIFsgNCAwIFIgNiAwIFIgXSANCj4+DQplbmRvYmoNCg0KNCAwIG9iag0KPDwNCi9UeXBlIC9QYWdlDQovUGFyZW50IDMgMCBSDQovUmVzb3VyY2VzIDw8DQovRm9udCA8PA0KL0YxIDkgMCBSIA0KPj4NCi9Qcm9jU2V0IDggMCBSDQo+Pg0KL01lZGlhQm94IFswIDAgNjEyLjAwMDAgNzkyLjAwMDBdDQovQ29udGVudHMgNSAwIFINCj4+DQplbmRvYmoNCg0KNSAwIG9iag0KPDwgL0xlbmd0aCAxMDc0ID4+DQpzdHJlYW0NCjIgSg0KQlQNCjAgMCAwIHJnDQovRjEgMDAyNyBUZg0KNTcuMzc1MCA3MjIuMjgwMCBUZA0KKCBBIFNpbXBsZSBQREYgRmlsZSApIFRqDQpFVA0KQlQNCi9GMSAwMDEwIFRmDQo2OS4yNTAwIDY4OC42MDgwIFRkDQooIFRoaXMgaXMgYSBzbWFsbCBkZW1vbnN0cmF0aW9uIC5wZGYgZmlsZSAtICkgVGoNCkVUDQpCVA0KL0YxIDAwMTAgVGYNCjY5LjI1MDAgNjY0LjcwNDAgVGQNCigganVzdCBmb3IgdXNlIGluIHRoZSBWaXJ0dWFsIE1lY2hhbmljcyB0dXRvcmlhbHMuIE1vcmUgdGV4dC4gQW5kIG1vcmUgKSBUag0KRVQNCkJUDQovRjEgMDAxMCBUZg0KNjkuMjUwMCA2NTIuNzUyMCBUZA0KKCB0ZXh0LiBBbmQgbW9yZSB0ZXh0LiBBbmQgbW9yZSB0ZXh0LiBBbmQgbW9yZSB0ZXh0LiApIFRqDQpFVA0KQlQNCi9GMSAwMDEwIFRmDQo2OS4yNTAwIDYyOC44NDgwIFRkDQooIEFuZCBtb3JlIHRleHQuIEFuZCBtb3JlIHRleHQuIEFuZCBtb3JlIHRleHQuIEFuZCBtb3JlIHRleHQuIEFuZCBtb3JlICkgVGoNCkVUDQpCVA0KL0YxIDAwMTAgVGYNCjY5LjI1MDAgNjE2Ljg5NjAgVGQNCiggdGV4dC4gQW5kIG1vcmUgdGV4dC4gQm9yaW5nLCB6enp6ei4gQW5kIG1vcmUgdGV4dC4gQW5kIG1vcmUgdGV4dC4gQW5kICkgVGoNCkVUDQpCVA0KL0YxIDAwMTAgVGYNCjY5LjI1MDAgNjA0Ljk0NDAgVGQNCiggbW9yZSB0ZXh0LiBBbmQgbW9yZSB0ZXh0LiBBbmQgbW9yZSB0ZXh0LiBBbmQgbW9yZSB0ZXh0LiBBbmQgbW9yZSB0ZXh0LiApIFRqDQpFVA0KQlQNCi9GMSAwMDEwIFRmDQo2OS4yNTAwIDU5Mi45OTIwIFRkDQooIEFuZCBtb3JlIHRleHQuIEFuZCBtb3JlIHRleHQuICkgVGoNCkVUDQpCVA0KL0YxIDAwMTAgVGYNCjY5LjI1MDAgNTY5LjA4ODAgVGQNCiggQW5kIG1vcmUgdGV4dC4gQW5kIG1vcmUgdGV4dC4gQW5kIG1vcmUgdGV4dC4gQW5kIG1vcmUgdGV4dC4gQW5kIG1vcmUgKSBUag0KRVQNCkJUDQovRjEgMDAxMCBUZg0KNjkuMjUwMCA1NTcuMTM2MCBUZA0KKCB0ZXh0LiBBbmQgbW9yZSB0ZXh0LiBBbmQgbW9yZSB0ZXh0LiBFdmVuIG1vcmUuIENvbnRpbnVlZCBvbiBwYWdlIDIgLi4uKSBUag0KRVQNCmVuZHN0cmVhbQ0KZW5kb2JqDQoNCjYgMCBvYmoNCjw8DQovVHlwZSAvUGFnZQ0KL1BhcmVudCAzIDAgUg0KL1Jlc291cmNlcyA8PA0KL0ZvbnQgPDwNCi9GMSA5IDAgUiANCj4+DQovUHJvY1NldCA4IDAgUg0KPj4NCi9NZWRpYUJveCBbMCAwIDYxMi4wMDAwIDc5Mi4wMDAwXQ0KL0NvbnRlbnRzIDcgMCBSDQo+Pg0KZW5kb2JqDQoNCjcgMCBvYmoNCjw8IC9MZW5ndGggNjc2ID4+DQpzdHJlYW0NCjIgSg0KQlQNCjAgMCAwIHJnDQovRjEgMDAyNyBUZg0KNTcuMzc1MCA3MjIuMjgwMCBUZA0KKCBTaW1wbGUgUERGIEZpbGUgMiApIFRqDQpFVA0KQlQNCi9GMSAwMDEwIFRmDQo2OS4yNTAwIDY4OC42MDgwIFRkDQooIC4uLmNvbnRpbnVlZCBmcm9tIHBhZ2UgMS4gWWV0IG1vcmUgdGV4dC4gQW5kIG1vcmUgdGV4dC4gQW5kIG1vcmUgdGV4dC4gKSBUag0KRVQNCkJUDQovRjEgMDAxMCBUZg0KNjkuMjUwMCA2NzYuNjU2MCBUZA0KKCBBbmQgbW9yZSB0ZXh0LiBBbmQgbW9yZSB0ZXh0LiBBbmQgbW9yZSB0ZXh0LiBBbmQgbW9yZSB0ZXh0LiBBbmQgbW9yZSApIFRqDQpFVA0KQlQNCi9GMSAwMDEwIFRmDQo2OS4yNTAwIDY2NC43MDQwIFRkDQooIHRleHQuIE9oLCBob3cgYm9yaW5nIHR5cGluZyB0aGlzIHN0dWZmLiBCdXQgbm90IGFzIGJvcmluZyBhcyB3YXRjaGluZyApIFRqDQpFVA0KQlQNCi9GMSAwMDEwIFRmDQo2OS4yNTAwIDY1Mi43NTIwIFRkDQooIHBhaW50IGRyeS4gQW5kIG1vcmUgdGV4dC4gQW5kIG1vcmUgdGV4dC4gQW5kIG1vcmUgdGV4dC4gQW5kIG1vcmUgdGV4dC4gKSBUag0KRVQNCkJUDQovRjEgMDAxMCBUZg0KNjkuMjUwMCA2NDAuODAwMCBUZA0KKCBCb3JpbmcuICBNb3JlLCBhIGxpdHRsZSBtb3JlIHRleHQuIFRoZSBlbmQsIGFuZCBqdXN0IGFzIHdlbGwuICkgVGoNCkVUDQplbmRzdHJlYW0NCmVuZG9iag0KDQo4IDAgb2JqDQpbL1BERiAvVGV4dF0NCmVuZG9iag0KDQo5IDAgb2JqDQo8PA0KL1R5cGUgL0ZvbnQNCi9TdWJ0eXBlIC9UeXBlMQ0KL05hbWUgL0YxDQovQmFzZUZvbnQgL0hlbHZldGljYQ0KL0VuY29kaW5nIC9XaW5BbnNpRW5jb2RpbmcNCj4+DQplbmRvYmoNCg0KMTAgMCBvYmoNCjw8DQovQ3JlYXRvciAoUmF2ZSBcKGh0dHA6Ly93d3cubmV2cm9uYS5jb20vcmF2ZVwpKQ0KL1Byb2R1Y2VyIChOZXZyb25hIERlc2lnbnMpDQovQ3JlYXRpb25EYXRlIChEOjIwMDYwMzAxMDcyODI2KQ0KPj4NCmVuZG9iag0KDQp4cmVmDQowIDExDQowMDAwMDAwMDAwIDY1NTM1IGYNCjAwMDAwMDAwMTkgMDAwMDAgbg0KMDAwMDAwMDA5MyAwMDAwMCBuDQowMDAwMDAwMTQ3IDAwMDAwIG4NCjAwMDAwMDAyMjIgMDAwMDAgbg0KMDAwMDAwMDM5MCAwMDAwMCBuDQowMDAwMDAxNTIyIDAwMDAwIG4NCjAwMDAwMDE2OTAgMDAwMDAgbg0KMDAwMDAwMjQyMyAwMDAwMCBuDQowMDAwMDAyNDU2IDAwMDAwIG4NCjAwMDAwMDI1NzQgMDAwMDAgbg0KDQp0cmFpbGVyDQo8PA0KL1NpemUgMTENCi9Sb290IDEgMCBSDQovSW5mbyAxMCAwIFINCj4+DQoNCnN0YXJ0eHJlZg0KMjcxNA0KJSVFT0YNCg==",
      "type": "application/pdf",
      "name": "teste.pdf",
      "extension_attributes": {}
    }
  ]
}
```

Resposta em caso de sucesso.

```json
"Your quotation was success send"
```

## Revendas

### Listar todas as revendas

[webjumpMultisellerDropshipApiSellerServiceV1GetListGet](https://mcstaging.broto.com.br/swagger#/webjumpMultisellerDropshipApiSellerServiceV1/webjumpMultisellerDropshipApiSellerServiceV1GetListGet)

Para obter a lista de revendas é necessário estar logado com um usuário que tenha o perfil Fabricante.

**Essa requisição não precisa de nenhum parâmetro**

``` json
[
  {
    "entity_id": "26",
    "vendor_name": "John Deere",
    "email": "WichrowskiJacksonR@JohnDeere.com",
    "telephone": "(23)99999-9911",
    "street": "Carlos Eduardo Monteiro de Lemos\r\n",
    "city": "Águia Branca",
    "country_id": "BR",
    "vendor_id": "275"
  }
]
```

### Associar revenda com região

[webjumpMultisellerDropshipApiSellerServiceV1AssociateCountiesPost](https://mcstaging.broto.com.br/swagger#/webjumpMultisellerDropshipApiSellerServiceV1/webjumpMultisellerDropshipApiSellerServiceV1AssociateCountiesPost)

Requisição que associa revenda com uma região. A api não permite duas revendas associadas a mesma região.

``` json
{
  "subVendorId": "431",
  "countiesCodes": [
    "1200393"
  ]
}
```

Resposta caso sucesso

``` json
true
```

## Regiões

### Filtro de regiões

[webjumpMultisellerDropshipApiCountyServiceV1GetListGet](https://mcstaging.broto.com.br/swagger#/webjumpMultisellerDropshipApiCountyServiceV1/webjumpMultisellerDropshipApiCountyServiceV1GetListGet)

* Listar por nome do município (usando query params)

```json
https://mcstaging.broto.com.br/rest/all/V1/multiseller-api/regions/counties/search?searchCriteria[filterGroups][0][filters][0][field]=nome_municipio&searchCriteria[filterGroups][0][filters][0][value]=São Paulo
```


Resposta em caso de sucesso
```json
[
  {
    "entity_id": "11495",
    "uf": "35",
    "nome_uf": "São Paulo",
    "microrregiao_geografica": "61",
    "nome_microrregiao": "São Paulo",
    "municipio": "50308",
    "codigo_municipio_completo": "3550308",
    "nome_municipio": "São Paulo"
  }
]
```

* Listar por código do município (usando query params)

```json
https://mcstaging.broto.com.br/rest/all/V1/multiseller-api/regions/counties/search?searchCriteria[filterGroups][0][filters][0][field]=codigo_municipio_completo&searchCriteria[filterGroups][0][filters][0][value]=3547809
```

Resposta em caso de sucesso
```json
[
  {
    "entity_id": "11411",
    "uf": "35",
    "nome_uf": "São Paulo",
    "microrregiao_geografica": "61",
    "nome_microrregiao": "São Paulo",
    "municipio": "47809",
    "codigo_municipio_completo": "3547809",
    "nome_municipio": "Santo André"
  }
]
```
