# Requisições Http

Ao trabalharmos com a comunicação entre o cliente e o servidor, seja ele um servidor web ou do *backend*, é imprescindível a utilização de uma *API* (*Aplication Programing Interface*). E é por meio dessa API que iremos realizar a comunicação entre o cliente e o servidor, através de **requisições http** 

Para realizar essas requisições, o Angular nos disponibiliza o módulo [**HttpClient**](https://angular.dev/guide/http/making-requests), que nos permite implementar e utilizar os **verbos HTTP** (*GET*, *PUT*, *POST*, *DELETE*, *PATH* ...), tanto para carregar as informações existentes do servidor quanto para modificá-las.

> *[`HttpClient`](https://angular.dev/api/common/http/HttpClient) has methods corresponding to the different HTTP verbs used to make requests, both to load data and to apply mutations on the server. Each  method returns an [RxJS `Observable`](https://rxjs.dev/guide/observable) which, **when subscribed**, sends the request and then emits the results when the server responds.*

---

## Trabalhando com requisições

Ao trabalhar com requisições utilizando o HttpClient, temos q ter em mente que:

- Sempre que implementamos algum método, de qualquer tipo que seja (*GET*, *PUT*, *POST*, *DELETE*), ele retornará um ***`observable`***, que irá realizar a requisição e retornar seus resultados **apenas** quando o método for escrito (***subscribe***)
- Sempre que um método for escrito (***subscribe***) ele retornará um **novo** ***`observable`***, e , consequentemente, uma nova requisição, ou seja, se um método for escrito duas vezes, ele irá retornar duas requisições diferentes.
  - Um exemplo disso é quando criamos um *service* para cuidar das chamadas da nossa API. Por ser um *service*, todos os seus **métodos** e **atributos** são os mesmos independente do componente onde ele está sendo injetado. Dessa forma, sempre que realizarmos o *subscribe* de um método do service em algum componente, mesmo que seja o mesmo método porém componente diferentes,  uma nova requisição será criada para cada um. 

### Buscando dados (GET)

Quando precisamos buscar dados dentro do nosso servidor, utilizamos, geralmente, o método **GET**, que retorna os dados do servidor sem os modificar.

```ts
http.get<Config>('/api/config').subscribe((config) => {
  // process the configuration.
});
```

- `<Config>`- É um tipa a requisição dizendo que ela irá retornar um *`Observable`* do tipo `Config`
- `'/api/config'` - A URL para qual a requisição será feita
- `.subscribe((config) => {...})` - Realiza o *subscribe* do método, fazendo com que a requisição seja realmente realizada e os dados retornados sejam armazenados na variável `config`
  - `(config)=> {...}` - Essa é uma ***Arrow Function*** que irá realizar determinada ação com base no sucesso, ou não, da nossa requisição; *`config`* é o resultante da requisição *GET*, que nos possibilita realizar configurações ou outras ações com os dados retornados.

### Alterando dados (POST)

Quando precisamos mudar ou adicionar dados dentro do nosso servidor, é necessário que utilizemos o método **POST**.

```ts
http.post<Config>('/api/config', newConfig).subscribe((config) => {
  console.log('Updated config:', config);
});
```

- Esse método é similar ao **GET**, mas ele aceita um parâmetro a mais, o ***`body`***, que dita as informações que serão adicionadas ao servidor

### Configurando os parâmetros da url

Parâmetros de URL são imprescindíveis quando queremos, por exemplo, abrir a página de edição do usuário cujo ID é 1, 2, ou qualquer outro número, de forma a página de cada usuário difere em diversos aspectos, como informações, foto, entre outras coisas.

```ts
http
  .get('/api/config', {
    params: {filter: 'all'},
  })
  .subscribe((config) => {
    // ...
  });
```

- `{params: {filter: 'all'}}` - É uma das formas que podemos utilizar para definir um parâmetro dentro da url.

Podemos passar uma instancia de [**HttpParams**](https://angular.dev/api/common/http/HttpParams) caso aja a necessidade de um controle maior sobre a construção ou a serialização dos parâmetros

> ***IMPORTANT:** Instances of [`HttpParams`](https://angular.dev/api/common/http/HttpParams) are immutable and cannot be directly changed. Instead, mutation methods such as `append()` return a new instance of [`HttpParams`](https://angular.dev/api/common/http/HttpParams) with the mutation applied.*

```ts
const baseParams = new HttpParams().set('filter', 'all');
http
  .get('/api/config', {
    params: baseParams.set('details', 'enabled'),
  })
  .subscribe((config) => {
    // ...
  });
```

### Definindo os Headers da requisições

Para definirmos *Headers* dentro das requisições, basta passá-los por meio da opção ***`headers{}`***.

```ts
http
  .get('/api/config', {
    headers: {
      'X-Debug-Level': 'verbose',
    },
  })
  .subscribe((config) => {
    // ...
  });
```

Da mesma forma que nos os parâmetros da url, é possível criar uma instancia de configuração para os *H*

*Headers*, por meio do [`HttpHeaders`](https://angular.dev/api/common/http/HttpHeaders).

```ts
const baseHeaders = new HttpHeaders().set('X-Debug-Level', 'minimal');
http
  .get<Config>('/api/config', {
    headers: baseHeaders.set('X-Debug-Level', 'verbose'),
  })
  .subscribe((config) => {
    // ...
  });
```

