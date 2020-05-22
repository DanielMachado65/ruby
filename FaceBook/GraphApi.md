# Graph API

> api `gráfico social`. Api do Facebook para busca de dados. 

Nessa documentação você vai poder ver como buscar informações do Facebook

### @Conceitos Gerais:

1. nós - (dados sobre um objeto especifico) objetos individuas como: usuário, foto, comentário

2. bordas - (coleções de objetos) conexões entre uma coleção de objetos a um únic objeto, como:

   - Fotos em uma página

   - Comentários em uma foto

3. campos - **dados** sobre um objeto, como aniversário de um usuário ou o nome de uma página.

### Funcionamento

A `Graph API` é baseada em __HTTP__, portanto funciona com qualquer linguagem que tenha uma biblioteca HTTP.

```c
curl -i -X GET "https://graph.facebook.com/facebook/picture?redirect=false"
```