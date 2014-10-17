# Integrações RD Station
## Integração Genérica via JavaScript 

Essa é a integração mais simples de ser feita. Basta apenas adicionar um script padrão diretamente na página do seu formulário, assim como o Google Analytics.

Os seus formulários irão para o RD Station com um identificador. Identificador é o nome do evento, por exemplo, cadastro, newsletter, formulário de orçamento, contato, entre outros, que irá aparecer na conversão do Lead no seu RD Station.


### Requisitos

Existe uma característica necessária e muito importante para a integração funcionar (talvez você precise editá-la ou adicioná-a na sua página)


Todo formulário a ser integrado deve ter um input com o nome <strong>email</strong> ou <strong>email_lead</strong>:
```HTML
<input type="text" name="email" />
```

### Integrando seus formulários

Uma vez atendida a especificação acima, para realizar a integração você deve inserir o script abaixo na página que contém o formulário, seguindo esses passos:

1 - Inserir seu token RD Station onde diz `'SEU_TOKEN_RDSTATION_AQUI'`. Ele pode ser obtido nas suas [Configurações do RD Station](https://www.rdstation.com.br/integracoes);

2 - Definir um identificador para o evento de conversão e inserí-lo no script abaixo onde diz `'IDENTIFICADOR DESEJADO'`;

3 - Adicionar o código na página que contém o formulário.

```HTML
<script type ='text/javascript' src="https://d335luupugsy2.cloudfront.net/js/integration/0.1.0/rd-js-integration.min.js"></script>
<script type ='text/javascript'>
    RDStationFormIntegration('SEU_TOKEN_RDSTATION_AQUI', 'IDENTIFICADOR DESEJADO');
</script>
```

Após esses passos, recomendamos sempre testar a integração para verificar se todos dados aparecem no RD Station.


### Outros campos e informações do formulário

Dos dados do usuário, a informação de e-mail (<strong>email</strong> ou <strong>email_lead</strong>) é <u><strong>obrigatória</strong></u>. Se não estiver presente, o formulário não será integrado.

Diversos outros campos podem ser utilizados para um chaveamento automático com o RD Station. Estes campos irão aparecer diretamente na tela de informação de Lead se mantiverem o mesmo nome.

<ul>
<li>nome</li>
<li>telefone</li>
<li>empresa</li>
<li>cargo</li>
<li>twitter</li>
</ul>

Todas as informações que você deseja enviar ao RD Station deve estar em um <em>input</em> com uma tag <strong>name</strong>. Essas informações ficarão disponíveis nos detalhes da conversão do lead.
```HTML
<input type="text" name="Telefone" />
```
Ps.: Recomenda-se que o campo de nome tenha name="name", pois assim esse será o nome do Lead criado no RD Station. Caso contrário, o e-mail do Lead aparecerá no lugar do nome.
```HTML
<input type="text" name="name" />
```

### Avisos de conversão por email

O RD Station pode lhe enviar um email quando uma nova conversão for realizada em seu site. Para isso, basta colocar o seu email na configuração da página da API https://www.rdstation.com.br/docs/api

### Erros

A API pode retornar erro caso:
 - (401) seu token RD Station esteja errado ou inválido;
 - (400) não esteja recebendo um identificador;
 - (400) não esteja recebendo a informação <strong>email</strong> ou <strong>email_lead</strong> do formulário;

É importante testar a integração após as modificações para evitar que erros comos esses acima apareçam para o seu visitante.

Também é interessante usar alguma validação dos campos pedidos para evitar o não preenchimento do campo de email, mas para isso será preciso algum controle Javascript ou de alguma outra linguagem.


### Exemplos completos

No código HTML abaixo, é possível ver uma página com um formulário simples que envia as informações para a API e depois redireciona o visitante para outra página.

```HTML
<!DOCTYPE html>
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>HTML Puro | Integrações RD Station</title>
<style type="text/css">
html,body{text-align:center;}
#wrapper{width:600px; margin:0 auto; text-align:center;}
#conversion-form{width:300px; margin:0 auto; border:1px solid silver;text-align:left;}
#conversion-form .field{padding:4px;}
#conversion-form .actions{text-align:center;}
#conversion-form label{display:block;}
#conversion-form input[type=text]{width:90%;}
</style>
</head>
<body>
<div id="wrapper">
 
  <h1>Integrações RD Station</h1>
  <h2>Integração Genérica via JavaScript</h2>
 
  <form id="sample"> 
    <div class="field">
      <label>E-mail:*</label>
      <input type="text" name="email" />
    </div>
    <div class="field">
      <label>Nome:*</label>
      <input type="text" name="nome" />
    </div>
    <div class="field">
      <label>Empresa:</label>
      <input type="text" name="empresa" />
    </div>
    <div class="actions">
      <input type="submit" value="Enviar" />
    </div>
  </form> 
</div>
<script type ='text/javascript' src="https://d335luupugsy2.cloudfront.net/js/integration/0.1.0/rd-js-integration.min.js"></script>
<script type ='text/javascript'>
    RDStationFormIntegration('f1c940384a971f2982c61a5e5f11e6b9', 'Formulário de contato');
</script>
    <!--
      * Atenção!
      * Token de testes - Usar o próprio de sua conta encontrado em: https://www.rdstation.com.br/docs/api
    -->
</body>
</html>
```