# Mocks e json-server:

## **O que é um Mock?**
Mock é uma técnica que salva nossa vida no desenvolvimento. Basicamente, é quando a gente desenvolve e testa a interface da nossa aplicação usando dados falsos, em vez de depender do backend, que pode estar fora do ar ou em construção.

## **Como Criar um Mock Usando `json-server`**
`json-server` é uma mão na roda. Ele cria um servidor RESTful a partir de um arquivo JSON. Vamos ver como fazer isso rapidinho.

### **Passo 1: Instalar o `json-server`**
Primeiro, instale o `json-server` globalmente com o npm:

```bash
npm install -g json-server
```

![Instalar json-server](https://i.imgur.com/KbzFe9h.jpeg)


### **Passo 2: Criar um Arquivo JSON**
Crie um arquivo chamado `db.json` e coloque os dados que você quer simular. Tipo assim:

```json
{
  "posts": [
    { "id": 1, "title": "Post 1", "author": "Author 1" },
    { "id": 2, "title": "Post 2", "author": "Author 2" }
  ],
  "comments": [
    { "id": 1, "body": "Comment 1", "postId": 1 },
    { "id": 2, "body": "Comment 2", "postId": 1 }
  ]
}
```

### **Passo 3: Iniciar o Servidor `json-server`**
Navegue até o diretório onde está o `db.json` e rode o comando:

```bash
json-server --watch db.json
```

![Iniciar json-server](https://i.imgur.com/zZeMAuV.jpeg)



### **Passo 4: Testar com o Postman**
Agora que o servidor está rodando, vamos usar o Postman pra fazer requisições GET e POST.

**Fazer Requisição GET com o Postman**
Abra o Postman e configure uma nova requisição GET para `http://localhost:3000/posts`. Clique em "Send" para ver os dados.

![Postman GET](https://i.imgur.com/la7vFdS.jpeg)

### **Fazer Requisição POST com o Postman**
Para adicionar novos dados, configure uma requisição POST para `http://localhost:3000/posts`. No corpo da requisição, use JSON:

```json
{
  "title": "Novo Post",
  "author": "Autor Novo"
}
```

Clique em "Send" para enviar os dados.

![Postman POST](https://i.imgur.com/arrafft.png)

### **Verificar o Resultado**
Depois de enviar a requisição POST, faça outra requisição GET para conferir se os novos dados aparecem. Easy peasy!!!

---

## **A Importância do Contrato entre Front e Back**
Antes de criar mocks, é fundamental ter um contrato claro entre frontend e backend. Esse contrato define os endpoints da API, os formatos dos dados e as possíveis respostas que o frontend pode esperar.

### **Benefícios de um Contrato Back-Front**
- Clareza e Consistência: Garante que todo mundo está na mesma página sobre a estrutura dos dados.
- Desenvolvimento Paralelo: Permite que frontend e backend trabalhem em paralelo sem bloqueios.
- Facilidade de Testes: Ajuda a criar mocks precisos para testes unitários e de integração.

### **Usando OpenAPI para Definir Contratos**
OpenAPI é uma ferramenta poderosa para definir contratos de API. Um dos maiores benefícios é que podemos visualizar a especificação no Swagger Editor, que ajuda a garantir que tudo está certo.

Exemplo de contrato OpenAPI com mais informações:

```yaml
openapi: 3.0.0
info:
  title: Blog API
  description: API para gerenciar posts e comentários de um blog
  version: 1.0.0
servers:
  - url: http://localhost:3000
paths:
  /posts:
    get:
      summary: Lista todos os posts
      responses:
        '200':
          description: Um array de posts
          content:
            application/json:
              schema:
                type: array
                items:
                  type: object
                  properties:
                    id:
                      type: integer
                      example: 1
                    title:
                      type: string
                      example: Meu Post
                    author:
                      type: string
                      example: Autor Exemplo
    post:
      summary: Cria um novo post
      requestBody:
        required: true
        content:
          application/json:
            schema:
              type: object
              properties:
                title:
                  type: string
                  example: Novo Post
                author:
                  type: string
                  example: Autor Novo
      responses:
        '201':
          description: Post criado com sucesso
```

![Exemplo OpenAPI](https://i.imgur.com/lFCD92Q.png)

### **Visualizando no Swagger Editor**
Você pode copiar essa especificação e colar no [Swagger Editor](https://editor.swagger.io/). Isso ajuda a visualizar e validar a especificação da API.

### **Plugando o OpenAPI no Localhost**
Com o `json-server` rodando, você pode usar a interface do Swagger para testar os endpoints diretamente no `localhost`. Isso é super útil para ver como a API se comporta sem escrever uma linha de código.

### **Conclusão**
Usar mocks como o `json-server` e definir contratos claros com OpenAPI é uma prática super comum e útil. Facilita o desenvolvimento e testes sem depender do backend. Assim, dá pra prototipar rapidinho e manter o ritmo do desenvolvimento. E não se esqueça: sempre tenha um contrato claro entre frontend e backend!

---