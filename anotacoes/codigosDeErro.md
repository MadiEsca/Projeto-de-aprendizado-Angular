# Trabalhando com erros

## Códigos de erro HTTP

Como bem sabemos, o código HTTP pode retornar alguns códigos de Status, onde cada um tem um determinado significado. Sendo alguns deles:
|HTTP (status)| 	Descrição|
|-------------|--------------|
|200 	|Sucesso.|
|201 	|Recurso criado com êxito pelo método POST.|
|204 	|Requisição tratada com sucesso.|
|304 	|Recurso não foi modificado.|
|400 	|Requisição malfeita.|
|401 	|Falha de autenticação.|
|403 	|O usuário não tem permissão para fazer determinada ação.|
|404 	|Requisição não encontrada.|
|405 	|Método não permitido.|
|415 	|Mídia não suportada.|
|422 	|Falha de validação de dados.|
|429 	|Excesso de requisições.|
|500 	|Erro interno do servidor.|

A especificação RFC 7807 padroniza os formatos das mensagens de erro em APIs HTTP, a fim de evitar que novos formatos sejam criados.

> Em geral, ela determina que:
>- devem ser usados os códigos de status HTTP entre os ranges 400 e 500 para representar as mensagens de erro;
>- o header Content-Type deve ser do tipo application/problem, incluindo o formato de serialização da mensagem: JSON ou XML.

## Configurando mensagens de erro
Essas informações estão no PDF.

## Capturas de exeções
Durante o desenvolvimento do projeto, é normal que ocorram erros.

Há erros, **relacionados a ações do usuário**, que são **previstos**, como o mau preenchimento de formulário, por exemplo. Para resolvê-los, basta que o sistema retorne uma mensagem ao usuário.

Outros erros estão **relacionados à programação**, como erros de sintaxe ou de digitação, que são facilmente detectáveis e corrigíveis.

Há, ainda, os erros **relacionados ao tempo de execução**, que ocorrem quando algum problema inesperado acontece. ***Esse tipo de erro trata-se de uma exceção que deve ser lançada, capturada e tratada.***

Lançar um erro (comando `throw`) significa fornecer um texto que será mostrado pelo navegador. Assim, quando ele ocorrer, em vez de apenas números, você pode incluir informações que tornem o problema mais identificável e fácil de resolver, como informar o nome da função na mensagem de erro.

Para capturar e tratar uma exceção, utilizamos os comandos catch (capturar) e try (tentar, no sentido de tratar). A sintaxe usada é a seguinte:

```ts
try {
	// seu código aqui
  } catch (error) {
	// tratamento de erro aqui
  }
```

O tratamento de exceções pode poluir e diminuir a perfomance sistêmica, mas reduz consideravelmente o tempo de debugging (ou depuração), quando usado adequadamente, além de evitar interrupções em seu sistema.

