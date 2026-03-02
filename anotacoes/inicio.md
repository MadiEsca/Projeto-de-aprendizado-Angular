# Introdução ao Angular

Esse é um projeto de estudos, onde todas as anotações e códigos de exemplo relacionados ao Angular serão escritos e guardados para consultas posteriores.

---
## Conceitos chave
Esse será nosso glossário de termos, onde irei explicar melhor alguns termos comuns
### Componente pai X Componente filho
**Componente pai** é o componente principal, ou seja, o componente que está acima de outro, ou melhor dizendo, **um componente onde outros componentes estão inseridos**. Enquanto um **componente filho** é justamente o contrário, um **componente que está dentro de outro componente**.

> **_Mas de que forma isso acontece?_**
> Vamos utilizar o arquivo `app.html` como exemplo. Esse é o nosso componente pai, onde nossos outros componentes serão utilizados, dessa forma, todos os outros componentes são componentes filhos do componente `app.html`, que, como todos os outros componentes, é composto por outros arquivos, como: `app.ts`, `app.css` e `app.spec.ts`.

> **_outro exemplo_**
> Vamos supor que criamos um novo componente chamado **página principal**, que para ser criado foram utilizados outros componentes dentro dela, como por exemplo um componente `menu`, `barra lateral` e `footer`. Dessa forma, temos como componente pai a **página principal** e como componentes filhos o **menu**, **barra lateral** e **footer**.

**Resumindo**: componente pai é o componente que **utiliza** outro componente, enquanto componente filho é o componente é **utilizado** por outro componente

---
### Utilização de [] & ()
Conhecemos esses dois sinais como sendo de bindings, `property bindings` e `event binding` respectivamente, mas quando iniciarmos a utilização de `@Inputs` e `@Outputs` vamos perceber que eles também são utilizados lá. Com isso, podemos ressignificar ambos os sinais da seguinte forma:
- `[ ]` - significa input, ou entrada de dados
- `( )` - Significa output, ou saída de dados

Que é exatamente a forma com a qual acessamos valores de input e output de componentes.

Sendo que, ==os outputs **passam informações** de um componente filho para um componente pai== enquanto um ==input **recebe informações** de um componente pai e envia para um componente filho==.

---

## Componentização
Dentro do Angular utilizamos a ideia de **componentes**, ou seja, nossos projetos e sites são criados a partir de componentes que interagem, ou não, entre si.

Com isso temos um controle maior sobre cada parte do nosso código, como por exemplo quando queremos modificar algo em uma determinada parte do nosso site, como no _menu_ ou no _footer_.

### Criando um componente

Os componentes que irão compor nosso projeto, como **menu**, **footer**, **homepage** etc, são criados dentro da pasta *app*, para posteriormente serem utilizados dentro de outros componentes ou até mesmo como páginas da nossa aplicação, por meio das **rotas**.

> *Antes de criar um componente, é preciso criar uma rota (âncora) para ele, onde quer que ele seja utilizado*.

#### Criando rotas para nossos componentes
Para isso, acesse o arquivo `app.routes.ts` (`V21 Angular`). Esse arquivo é utilizado para criar **rotas de navegação** dentro do projeto, para, por exemplo, as páginas internas de um site.

Nosso arquivo terá uma estrutura semelhante a seguinte:

```tsx
import {<nome-componente1>} from './pasta/para/arquivo.ts' /*.ts -> não é necessário*/

import {<nome-componente2>} from './pasta/para/arquivo.ts'

const routes: Routes = [
    {
        path: '',
        component: <nome-componente1>
    },
    {
        path: '/home',
        component: <nome-componente2>
    },
]

```

#### Integrando nossos componentes
Para utilizar um componente dentro de outro componente, basta importar o componente desejado e adicioná-lo ao array `imports:[...]` do decorador componente que utilizará o outro.

```tsx
import {<nome-componente>} from './pasta/para/arquivo' /*Arquivo typescript*/

@component({
    import: [<nome-componente>]
})

```

> Esse procedimento de criar pasta, arquivos e rota (app-routing) será feito para todos os arquivos adicionados.

### Anatomia de um componente
Os componentes são a base para o funcionamento dos projetos que utilizam o Angular. Dessa forma, vamos entender um pouco mais sobre como funciona a estrutura de um componente dentro do Angular.

``` tsx
import { Component } from '@angular/core'; //Importações globais

@Component({
  selector: 'app-dashboard', //Nome do componente
  imports: [], //Importação dos componentes q serão utilizados dentro desse componente
  templateUrl: './dashboard.html', //Caminho para o arquivo HTML do nosso componente
  styleUrl: './dashboard.css', //Caminho para o arquivo CSS do nosso componente
})

export class Dashboard {
    //Onde definimos a lógica do nosso componente
}
```

## Template Bindings
É a sincronização de dados entre o Javascript e o HTML de um componente, seja **internamente**, pelo arquivo.ts do próprio componente com seu HTML, ou **externamente**, de um componente para outro.

### Processo de binding

Trata-se do processo de integração do TypeScript com o HTML, que possibilita a integração entre um arquivo com a extensão `.ts` e um arquivo com a extensão `.html`. Essa importação pode ser de um **dado**, um **texto**, uma **imagem** ou até mesmo de um **evento**.

Através dos bindings é possível realizarmos diversas ações,tais como:
- Event listeners
- Alteração dinâmica de textos e imagens
- Controle de dados
- Várias outras coisas...

### Tipos de binding
Agora vamos mergulhar nos tipos de biding que o Angular nos permite realizar.

#### Interpolação
A interpolação é a forma mais simples e direta de exibir dados do componente no template HTML. Ela utiliza chaves duplas `{{ }}` para inserir valores de variáveis, propriedades ou expressões JavaScript diretamente no conteúdo do elemento.

**Utilizada geralmente quando**
- A informação é apenas Read-Only
- Mostrar textos simples ou valores calculados

**Sintaxe**
``` html
<!-- Mostrando o valor de uma variável -->
<h1> {{ titulo }} <h1>

<!-- Operações matemáticas -->
<p>Total: {{ 10 + 20 }}</p>
<!-- Resultado: Total: 30 -->

<!-- Métodos de string -->
<p>{{ nome.toUpperCase() }}</p>
<!-- Converte para maiúsculas -->

<!-- Operadores ternários -->
<p>{{ idade >= 18 ? 'Maior de idade' : 'Menor de idade' }}</p>

<!-- Chamadas de métodos -->
<p>{{ calcularTotal() }}</p>

<!-- Acessar propriedades de objetos -->
<p>{{ usuario.nome }}</p>
```

#### Property Binding
O **Property Binding** ==permite definir propriedades e atributos de elementos HTML== dinamicamente através do TypeScript do componente. Diferente da interpolação (que apenas exibe valores), o Property Binding **modifica propriedades reais** dos elementos HTML.

**Utilizado geralmente quando**
- É necesssário controlar os atributos HTML dinamicamente (`disable`, `src`, `href`, `etc.`), por exemplo em formulários

| Situação | Use |
| --- | --- |
| Exibir texto simples | Interpolação `{{ }}` |
| Definir atributos HTML | Property Binding `[]` |
| Definir propriedades booleanas | Property Binding `[]` |
| Passar valores para componentes | Property Binding `[]` |
| Conteúdo HTML dinâmico | Property Binding `[innerHTML]` |

**sintaxe**
```html
[propriedade]="valor"

<p [innerHTML]="titulo"> </p>
```
> **obs**
> Os colchetes são necessários para indicar uma _property binding_

#### Event Binding
O **Event Binding** permite capturar eventos do DOM (cliques do mouse, digitação no teclado, mudanças em inputs, etc.) e executar métodos ou expressões no componente TypeScript. É a forma de fazer o template **comunicar-se com o componente** quando algo acontece na interface.

```ts
(evento)="metodo()"
```

#### Two-way data binding
O **Two-Way Data Binding** (ligação de dados bidirecional) permite que dados fluam em **ambas as direções** simultaneamente:

- **Componente → Template**: O valor do componente é exibido no elemento
- **Template → Componente**: Mudanças no elemento atualizam o componente automaticamente

É especialmente útil em **formulários**, onde você precisa tanto exibir valores quanto capturar mudanças do usuário.

**Quando usar?**

- **Formulários**: Inputs, textareas, selects, checkboxes, radio buttons
- Quando você precisa que mudanças no template atualizem o componente automaticamente
- Para criar interfaces reativas onde dados são sincronizados em tempo real

**Sintaxe**

```html
[(ngModel)]="variavel"
```

**Importante**:

- Os colchetes e parênteses `[()]` são chamados de “banana in a box” (banana na caixa)
- É uma combinação de Property Binding `[]` e Event Binding `()`
- `ngModel` é uma diretiva especial do Angular para two-way binding

#### Class binding
O **Class Binding** permite adicionar ou remover classes CSS dinamicamente baseado em condições ou valores do componente. É a forma de controlar a aparência visual dos elementos através de classes CSS de forma reativa.

**Quando usar?**

- Quando você precisa aplicar/remover classes CSS baseado em condições
- Para criar interfaces que mudam de aparência baseado no estado da aplicação
- Para aplicar estilos condicionais sem usar Style Binding inline
- Quando você tem classes CSS pré-definidas e quer aplicá-las dinamicamente

**Sintaxe**

```html
[class.nome-da-classe]="condicao"
```

**Importante**:

- `nome-da-classe` é o nome da classe CSS (sem o ponto inicial)
- `condicao` deve ser uma _função_ que retorna `true` ou `false`
- Quando `true`, a classe é aplicada; quando `false`, é removida

#### Style Binding

O **Style Binding** permite definir propriedades CSS inline dinamicamente através de valores do componente TypeScript. Diferente do Class Binding (que aplica classes CSS pré-definidas), o Style Binding define estilos diretamente no elemento.

**Sintaxe**

```html
[style.propriedade-css]="valor"
```

**Importante**:

- `propriedade-css` é o nome da propriedade CSS em formato kebab-case (com hífen)
- `valor` pode ser uma string, número, ou expressão que retorna um valor válido para CSS
- Para propriedades com unidades, use a sintaxe `[style.propriedade.unidade]="valor"`

## Controles de fluxo
Agora vamos falar sobre os clássicos:
- `if`
- `Else`
- `Else if`
- `Switch case`
- `For`

### If
Funciona baseado em uma condição que, caso verdadeira, executa ou exibe determinado código. No nosso caso, caso essa condição seja verdadeira, ela irá mostrar uma informação ou se comportar de forma diferente do que caso a condição seja falsa.

**Sintaxe**
```html
@if (condicao){
    <p>bloco de codigo</p>
}
```

### Switch case
Trabalha de forma similar ao If, else e Else if, ou seja, com condições e casos a serem trabalhados em cada condição. O Switch case é uma ótima alternativa vários If's e Else's.

**Sintaxe**
```html
@switch(condicao-principal){
    @case(condicao-1){
        ...
    }
    @case(condicao-2){
        ...
    }
    @default{
        ...
    }
}
```

### For
Diferentemente de todos as condições anteriores, o for não trabalha com condições, mas sim com listas, ou arrays, a serem percorridos, onde temos que realizar a mesma tarefa em cada elemente desse array, seja classificá-los ou apenas mostrá-los em uma lista.

Dessa forma, loops For são utilizados quando queremos trabalhar em cima de listas.

**Sintaxe**
```html
@for(item of itens; track $index){
    <p> {{ item }} </p>
}
```

## Comunicação entre componentes
Vamos aprender de que forma podemos realizar a comunicação entre **componentes pais** e **componentes filhos**, por meio de `@inputs` e `@outputs`.

Input e Output estão relacionados ao componente filho (componente que é utilizado por outro componente), ou seja, o componente filho abre um input para receber um valor do pai; e da mesma forma libera um output para que o pai receba um valor.


### @input
É o parâmetro que define que aquela propriedade estará sendo **recebida de um componente pai**, podendo ser de qualquer tipo, seja string, number, object, boolean etc.

Ele é declarado dentro da classe do typescript do componente e é necessário importá-la dentro do mesmo.

Para utilizarmos o @input da forma correta, é necessário fazer duas coisas antes:
- 1° - Dentro do componente que iremos utilizar o @Input
    - Precisamos importar o Input e declará-lo dentro do parâmetro que queremos "terceirizar" para o componente pai
    ```ts
    import { Component, Input } from '@angular/core'
    ...
    export class nome-componente{
        //@Input() nomePropriedade: tipoPropriedade = 'valor padrão'
        @Input() tituloMenu: String = ''1
    }
    ```
- 2° - Dentro do componente pai
    - Dentro desse componente, de forma similar a anterior, iremos criar um atributo, do mesmo tipo (String, number etc) do input do componente filho, para que possamos referenciá-lo, por meio de property bindings, dentro do nosso componente filho
    - **_dentro do arquivo.ts_**
        ```ts
        ...
        export class componente-pai{
            nomeTituloMenu: String = "Esse é o título do meu menu"
        }
        ```
    - **_Dentro do arquivo.html_**
        ```html
        ...
        <nome-componente [tituloMenu]="nomeTituloMenu"></nome-componente>
        ```
> _Esse exemplo estará localizado dentro do componente `menu`_

### Output
Se dentro do `Input` um **componente ==filho recebe==** determinado valor **do componente pai, que o ==envia==**; e no `Output` ocorre o contrário, o ==**componente filho envia**== algum valor para o **componente pai, que o ==recebe==**.

Para que isso ocorra, da mesma forma que com o Input, será necessário criarmos algumas coisas tanto no componente filho quanto pai, sendo elas:
- Componente filho:
    Dentro do nosso componente filho iremos criar um objeto, ou propriedade, que receba `@Output`, assim como no @Input. Além de que será necessário importar o `@Output` dentro do nosso projeto.
    
    ```ts
    import { Component, EventEmitter, Output } from '@angular/core';
    ...
    export class componente-filho{
        @Output() enviarMensagem = new EventEmitter<String>() //Criação de um objeto emmiter q irá enviar uma String para o componente pai

        emitirValor(){ // Função que será utilizada para enviar o valor para o componente pai
            this.enviarMensagem.emit("Texto do componente filho, enviado para o componente pai")
        }
    }
    ```
- Componente pai:
    Agora que temos tudo criado dentro do nosso componente filho, vamos receber e utilizar esses valores dentro do nosso componente pai.
    - Utilizando o `@Output` do componente filho dentro do componente pai
        ```html
        <componente-filho
            (enviarMensagem)="receberValorOutputFilho($event)">
        </componente-filho> <!-- Indica que em qualquer página esse componente, menu, será carregado -->
        ```
        **explicação:**
        - `enviarMensagem` - É o nosso o objeto/atributo que definimos com o `@Output`
        - `receberValorOutputFilho($event)` - É o método que será executado assim que recebermos o valor que for enviado pelo nosso componente filho.
            - `$event` - Representa justamente o conteúdo que foi **enviado** pelo componente filho, **recebido** e utilizado pelo componente pai.

    - Agora que temos toda a estrutura para a utilização dos dados enviados pelo nosso componente filho, vamor criar uma função, ou método, que consiga receber esse valor do nosso componente filho, e iremos fazer isso de forma similar ao que já fizemos com o `@Input`.
    ```ts
    export class componente-pai{
        receberValorOutputFilho(texto: String) {
            console.log(`recebido: ${texto}`)
        }
    }
    ```
    - **Explicação**
        - `receberValorOutputFilho(texto: String){}` - Esse é o método que recebe e utiliza os valores que foram enviados pelo nosso componente filho
            - `texto: String` - Lembra do `$event`? Que representava tudo que nosso componente filho enviava? Essa é a representação dele, dentro de nossa função
                - `texto` - É a mesma coisa que $event, mas foi renomeado, dessa forma, pode receber qualquer nome
                - `:String` - É o tipo da nossa resposta. Tem que ser do mesmo tipo que foi enviado pelo nosso componente filho. Nesse caso é do tipo `:String` mas poderia ser de qualquer outro (`number`, `boolean` etc.)
            - `{...}` - Todo o restante se refere a lógica que foi aplicada em cima dos dados recebidos

---

## Services
Vamos avançar mais um pouco e começar a trabalhar com o que chamamos de services. Elas são utilizadas para manter estados comuns entre determinados componentes. Ou seja, ao invés de termos que criar diversos métodos, parâmetros ou instâncias de objetos, iguais em diversos componentes diferentes, podemos apenas criar um service e utilizá-lo dentro desses componentes.

Dessa forma temos ainda mais praticidade, além de um código mais limpo e organizado.

### **Criando um `service`**
para isso basta utilizarmos o seguite comando do angular:
```bash
ng g s <nome-service>
ng generate service <nome-service>
```

### Estrutura de um service
Um service é composto por apenas dois arquivos:
- `service.ts` - Arquivo que utilizamos para programar o service
- `service.spec.ts`- Arquivo de testes

```ts
@Injectable({
  providedIn: 'root',
})
```
- `@Injectable` - É uma notação e indica que esse arquivo, ou service, pode ser injetado em qualquer componente dentro do nosso projeto
- `providedIn: 'root'` - Indica que essa é uma instância única, ou seja, qualquer componente que a implementar, estará referenciando sempre ao mesmo objeto, com isso, tudo é compartilhado com quem o intancia, desde métodos a atributos. Além disso, qualquer alteração feita no service por algum dos componentes, irá afetar automaticamente todos que o implementam.

---

## Requisições HTTP
Vamos trabalhar agora com as famosas **requisições HTTP**. Como bem sabemos, nossas requisições e respostas **http** trabalham em cima de alguns verbos, sendo os mais conhecidos:
| **Operação do CRUD Verbo HTTP** | **Verbo HTTP** |
| ------------------------------- | -------------- |
| CREATE                          |     POST       |
| READ                            |     GET        |
| UPDATE                          |    PUT, PATCH  |
| DELETE                          |     DELETE     |

O Angular nos permite trabalhar com esses verbos e requisições por meio do **`HttpCliente`**, o provider que utilizamos dentro do nosso arquivo `app.config.ts` para que possamos acessar suas funcionalidades dentro do nosso projeto.

Para conseguirmos trabalhar com requisições http dentro do Angular, precisamos realizar algumas configurações, além de seguirmos algumas boas práticas.

- 1° - Importação do provider HTTP
    Dentro do arquivo `app.config.ts` iremos adicionar a seguinte linha:
    ```ts
    export const appConfig: ApplicationConfig = {
    providers: [
        provideHttpClient() //Provider que permite fazer requisições http
    ]
    };
    ```
- 2° - Criar um Service http
    Uma recomendação é criar um service que irá implementar os métodos para que as requisições HTTP possam ser realidas, ao invés de implementarmos esses métodos dentro de cada componente.

    Outra recomendação é criarmos uma interface para tipar as responses geradas pela nossa API. Essa interface será utilizada para que possamos tipar cada campo da nossa requisição de uma forma mais simplificada. Fazemos essa tipagem da seguinte forma:
    ```ts
    export interface IPost{
        UserID: number // Campo: tipo
        ID: number // Campo: tipo
        Title: string // Campo: tipo
        Body: string // Campo: tipo
    }
    ```
    Utilizamos a `keyword` **`export`** para que possamos tipar outros campos com essa mesma interface, dentro dos componentes que injetarem esse Service
    > O "I" é apenas uma convenção para a nomeação de interfaces

    Com isso, vamos tipar, a partir de agora, nosso método, para que ele possa retornar apenas objetos do tipo `IPost`, a interface que criamos anteriormente.

    ```ts
    export class HttpService {
    private readonly _httpClient: HttpClient = inject(HttpClient) //Torna nossa implementação privada e não modificável

    private readonly url: string = "https://jsonplaceholder.typicode.com/posts"
    //Método do tipo GET
    getPosts(): Observable<IPost[]>{ //1
        return this._httpClient.get<IPost[]>(this.url) //Faz com que nosso observable seja retornado assim que for assinado | 2
        }
    }
    ```

    - 1 - Indica que essa função irá, obrigatoriamente, retornar **um Observable que contém uma lista de `IPost`**
    - 2 - Esse trecho faz a requisição HTTP e retorna um Observable que, quando for assinado (subscribe), emitirá um array de IPost.


- 3° - Realizar a utilização do Service
    Agora que temos um Service que consuma nossa API, podemos simplesmente injetar esse service dentro do nosso componente e finalmente utilizá-lo. Da seguinte forma

    - Injetando o Service no componente:
    ```ts
    ...
    _httpService = inject(_HttpService)
    ```


# Pesquisas
ngOnInit
Observable
Tipagem com interfaces