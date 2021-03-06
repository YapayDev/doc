---
title: Transação com Análise de Fraude
position: 2
menu: gateway
right_code: |
    ~~~ json
    curl
        --request POST https://sandbox.gateway.yapay.com.br/checkout/api/v3/transacao
        --header "Content-Type: application/json"
        --curl -u usuario:senha .........
        --data-binary
        {
        "codigoEstabelecimento" : 1000000000000,
        "codigoFormaPagamento" : 190,
        "transacao" : {
            "numeroTransacao" : 1234,
            "valor" : 2000,
            "valorDesconto" : 0,
            "parcelas" : 1,
            "urlCampainha" : "http://seusite.com.br/campainha",
            "ip" : "192.168.12.110",
            "idioma" : 1,
            "campoLivre1" : "",
            "campoLivre2" : "",
            "campoLivre3" : "",
            "campoLivre4" : "",
            "campoLivre5" : ""
        },
        "dadosCartao" : {
            "nomePortador" : "Teste Teste",
            "numeroCartao" : "4002479199570736",
            "codigoSeguranca" : "132",
            "dataValidade" : "12/2020"
        },
        "itensDoPedido" : [
        {
            "codigoProduto" : 1,
            "nomeProduto" : "Produto 1",
            "codigoCategoria" : 1,
            "nomeCategoria" : "categoria",
            "quantidadeProduto" : 1,
            "valorUnitarioProduto" : 2000
        }
        ],
        "dadosCobranca" : {
            "codigoCliente" : 1,
            "tipoCliente" : 1,
            "nome" : "Teste 123",
            "email" : "teste@teste.com",
            "dataNascimento" : "10/01/1975",
            "sexo" : "M",
            "documento" : "123.123.123-12",
            "endereco" : {
                "logradouro" : "Rua",
                "numero" : "123",
                "complemento" : "",
                "cep" : "12345-678",
                "bairro" : "Bairro",
                "cidade" : "Cidade",
                "estado" : "SP",
                "pais" : "BR"
                },
            "telefone" : [
                {
                "tipoTelefone" : "1",
                "ddi" : "55",
                "ddd" : "12",
                "telefone" : "1234-5678"
                }
            ]
        },
        "dadosEntrega" : { 
            "nome" : "Teste 123",
            "endereco" : {
                "logradouro" : "Rua",
                "numero" : "123",
                "complemento" : "",
                "cep" : "12345-678",
                "bairro" : "Bairro",
                "cidade" : "Cidade",
                "estado" : "SP",
                "pais" : "BR"
                },
            "telefone" : [
                {
                "tipoTelefone" : "1",
                "ddi" : "55",
                "ddd" : "12",
                "telefone" : "1234-5678"
                }
            ]
        }
        }
    
    ~~~
    {: title="Exemplo criação transação" }

    ~~~json
    --header "Content-Type: application/json"
        {  "numeroTransacao": 1234,
        "codigoEstabelecimento": "1000000000000",
        "codigoFormaPagamento": 190,
        "valor": 2000, 
        "valorDesconto": 0, 
        "parcelas": 1, 
        "statusTransacao": 1,
        "autorizacao": "12260",
        "codigoTransacaoOperadora": "0",
        "dataAprovacaoOperadora": "24/05/2017", 
        "numeroComprovanteVenda": "10117092009151900057", 
        "nsu": "428706",
        "mensagemVenda": "00 - Success",
        "urlPagamento": "https://sandbox.gateway.yapay.com.br/checkout/PagamentoCielo/PagamentoCielo.do?cod=14956291484887110cf2a-9aeb-4b34-a869-1a61f0611b66", 
        "cartoesUtilizados": ["400247******0736"]
        }
    ~~~    
    {: title="Exemplo retorno transação" }
---


A utilização desta estrutura é indicada para envio de pedidos com a forma de pagamento cartão de crédito, onde o estabelecimento possui contratação de umas das empresas de análise de risco integradas pelo Yapay, sendo elas ClearSale (modalidades: Total/Total Garantido, Application, ID e Start) e FControl (modalidade Fila).

<i class="fa fa-exclamation-circle" aria-hidden="true"></i> Contratação a parte com as empresas **ClearSale** e **FControl**.
{: .informativoVermelho }

**REQUISIÇÃO**


 <i class="fa fa-info-circle" aria-hidden="true"></i> Para enviar a transação, utilize o método <span class="post">POST</span>.
 {: .informativo }

 Para autenticação, enviar `login` e `senha` no HEADER:

| Campo    | Descrição                |
|----------|--------------------------|
| usuario  | Login do estabelecimento |
| senha    | Senha do estabelecimento |


| Campo                    | Descrição                                                                                  | Tipo          | Tamanho            | Obrigatório |
|--------------------------|--------------------------------------------------------------------------------------------|---------------|--------------------|-------------|
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway)           | Numérico      | 13 dígitos         | Sim         |
| codigoFormaPagamento     | <a href="/gateway/codigos-da-api/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                                               | Numérico      | Até 3 dígitos      | Sim         |
| transacao                | Nó reservado para informações da transação                                                 | - | - | - |
| dadosCartao              | Nó reservado para dados de cartão                                                          | - | - | - |
| itensDoPedido            | Nó reservado para informações dos produtos                                                 | - | - | - |
| dadosCobranca            | Nó reservado para informações dos dados de cobrança                                        | - | - | - |
| telefone                 | Nó reservado para informações de telefone                                                  | - | - | - |
| dadosEntrega             | Nó reservado para informações de dados de entrega                                          | - | - | - |



_`transacao`_
{: .subtituloAzul }


| Campo                                | Descrição                                                            | Tipo          | Tamanho            | Obrigatório  |
|--------------------------------------|----------------------------------------------------------------------|---------------|--------------------|--------------|
| numeroTransacao       | Código que identifica a transação dentro do Yapay                                | Numérico      | Até 19 dígitos     | Sim          |
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do Yapay (fornecido pelo gateway) | Numérico      | 13 dígitos         | Sim          |
| codigoFormaPagamento  | Código da forma de pagamento                                                        | Numérico      | Até 3 dígitos      | Sim          |
| valor                 | Valor da transação. Deve ser enviado sem pontos ou vírgulas                         | Numérico      | Até 10 dígitos     | Sim          |
| moeda                 | Tipo da moeda. OBS: Disponível 'USD" apenas para PayPal Internacional               | Alfa Numérico | Até 10 caracteres  | Não          |
| tipoParcelamento      | Use "E" para estabelecimento, use "A" para administradora. Caso não for enviado será utilizado as configurações do seu estabelecimento | Alfa Numérico | 1 caracter | Não |
| valorDesconto         | Valor do desconto da transação. Campo apenas informativo                                                         | Numérico | Até 10 dígitos | Sim |
| parcelas              | Quantidade de parcelas da transação. Verificar se forma de pagamento suporta parcelamento                        | Numérico | Até 2 dígitos  | Sim |
| urlCampainha          | URL será sempre acionada quando o status do pedido mudar. Deve estar preparada para receber dados de campainha   | Alfa Numérico | Até 250 caracteres | Não |
| urlResultado          | Para o modelo de pagamento redirect, O Yapay redirecionará para essa URL | Alfa Numérico | Até 250 caracteres | Para pagamentos redirecionáveis é  obrigatório |
| ip                    | Número do IP do usuário final/cliente. Formato xxx.xxx.xxx.xxx              | Alfa Numérico | Até 15 caracteres | Sim |
| idioma                | 1 - Português 2 - Inglês 3 - Espanhol                                       | Numérico      | - | Sim |
| campoLivre1           | Campo Livre 1                                                               | Alfa Numérico | Até 16 caracteres | Não |
| campoLivre2           | Campo Livre 2 (Envio do FingerPrint ClearSale)                              | Alfa Numérico | Até 16 caracteres | Não |
| campoLivre3           | Campo Livre 3 (Envio do canal de venda ClearSale Total/Total Garantido e Application - solicitar ativação para Suporte Yapay) | Alfa Numérico | Até 16 caracteres | Não |
| campoLivre4           | Campo Livre 4                                                               | Alfa Numérico | Até 16 caracteres | Não |
| campoLivre5           | Campo Livre 5                                                               | Alfa Numérico | Até 16 caracteres | Não |


_`dadosCartao`_
{: .subtituloAzul }

| Campo | Descrição | Tipo | Tamanho | Obrigatório |
|-------| ----------|------| --------|------------ |
| nomePortador    | Nome do titular do cartão de crédito (Exatamente como escrito no cartão) | Alfa Numérico | Até 16 dígitos | Sim 
| numeroCartao    | Numero do cartão de crédito, sem espaços ou traços                       | Numérico      | Até 22 caracteres | Sim 
| codigoSeguranca | Código de segurança do cartão (campo não é armazenado pelo Yapay)     | Numérico      | Até 4 caracteres | Sim 
| dataValidade    | Data de validade do cartão. Formato mm/yyyy                              | Alfa Numérico | 7 caracteres | Sim


_`dadosCobranca`_
{: .subtituloAzul }

| Campo          | Descrição                                                | Tipo          | Tamanho            | Obrigatório |
|----------------|----------------------------------------------------------|---------------|--------------------|-------------|
| nome           | Nome do comprador                                        | Alfa Numérico | Até 100 caracteres | Sim |
| documento      | Documento principal do comprado                          | Alfa Numérico | 30 caracteres      | Sim |
| documento2     | Documento principal do comprado                          | Alfa Numérico | 30 caracteres      | Não |
| email          | E-mail do comprador                                      | Alfa Numérico | 20 caracteres      | Sim |
| codigoCliente  | Código do Comprador                                      | Alfa Numérico | 20 caracteres      | Não |
| dataNascimento | Data Nascimento Comprador                                | Alfa Numérico | 10 caracteres      | Sim |
| sexo           | Sexo Comprador                                           | Alfa Numérico | 2 caracteres       | Não |
| tipoCliente    | Tipo do Cliente - 1 - Pessoa Física 2 - Pessoa Jurídica  | Numérico      | Até 8 dígitos      | Sim |
| endereco       | Nó reservado para dados de endereço do comprador         | -             | -                  | -   |
| telefone       | Nó reservado para dados de telefone do comprador         | -             | -                  | -   |

_`itensDoPedido`_
{: .subtituloAzul }

| Campo                | Descrição                                                          | Tipo          | Tamanho        | Obrigatório |
|----------------------|--------------------------------------------------------------------|---------------|----------------|-------------|
| codigoProduto        | Código único que identifica cada produto                           | Alfa Numérico | 20 caracteres  | Sim         |
| codigoCategoria      | Código que identifica categoria do produto                         | Alfa Numérico | 20 caracteres  | Sim         |
| nomeProduto          | Nome do Produto                                                    | Alfa Numérico | 100 caracteres | Sim         |
| quantidadeProduto    | Quantidade comprada do produto                                     | Numérico      | Até 8 dígitos  | Sim         |
| valorUnitarioProduto | Valor unitário do produto. Deve ser enviado sem pontos ou vírgulas | Numérico      | Até 10 dígitos | Sim         |
| nomeCategoria        | Nome da categoria do produto                                       | Alfa Numérico | 100 caracteres | Sim         |

_`endereco`_
{: .subtituloAzul }

| Campo       | Descrição               | Tipo          | Obrigatório |
|-------------|-------------------------|---------------|-------------|
| logradouro  | Endereço do comprador   | Alfa Numérico | Sim         |
| numero      | Número do comprador     | Alfa Numérico | Sim         |
| bairro      | Bairro do comprador     | Alfa Numérico | Sim         |
| complemento | Complemento do endereço | Alfa Numérico | Não         |
| cidade      | Cidade do comprador     | Alfa Numérico | Sim         |
| estado      | Estado do comprador     | Alfa Numérico | Sim         |
| cep         | CEP do comprador        | Alfa Numérico | Sim         |
| pais        | País do comprador       | Alfa Numérico | Sim         |

_`telefone`_
{: .subtituloAzul }

| Campo        | Descrição                                                                                  | Tipo          | Obrigatório |
|--------------|--------------------------------------------------------------------------------------------|---------------|-------------|
| tipoTelefone | 1 = Outros / 2 = Residencial / 3 = Comercial / 4 = Recados / 5 = Cobrança / 6 = Temporário | Numérico      | Sim         |
| ddi          | Código DDI do telefone                                                                     | Alfa Numérico | Sim         |
| ddd          | Código DDD do telefone                                                                     | Alfa Numérico | Sim         |
| telefone     | Número do telefone                                                                         | Alfa Numérico | Sim         |

_`dadosEntrega`_
{: .subtituloAzul }

| Campo    | Descrição                                        | Tipo          | Tamanho       | Obrigatório |
|----------|--------------------------------------------------|---------------|---------------|-------------|
| nome     | Nome do comprador                                | Alfa Numérico | 20 caracteres | Não         |
| email    | E-mail do comprador                              | Alfa Numérico | 20 caracteres | Não         |
| endereco | Nó reservado para dados de endereço do comprador | -             | -             | -           |
| telefone | Nó reservado para dados de telefone do comprador | -             | -             | -           |

**RESPOSTA**


| Campo                    | Descrição                                                               | Tipo          | Tamanho            |
|--------------------------|-------------------------------------------------------------------------|---------------|--------------------|
| numeroTransacao          | Código que identifica a transação dentro do Yapay                    | Numérico      | Até 19 dígitos     |
| codigoEstabelecimento    | Código que identifica o estabelecimento dentro do Yapay              | Numérico      | 13 dígitos         |
| codigoFormaPagamento     | <a href="/gateway/rest/codigos-da-api-rest/#forma-de-pagamento" target="_blank" class="linkPadraoVerde">Código da forma de pagamento</a>                                            | Numérico      | Até 3 dígitos      |
| valor                    | Valor da transação.                                                     | Numérico      | Até 10 dígitos     |
| valorDesconto            | Valor desconto                                                          | Numérico      | Até 10 dígitos     |
| taxaEmbarque             | Valor taxa embarque                                                     | Numérico      | Até 10 dígitos     |
| parcelas                 | Quantidade de parcelas da transação                                     | Numérico      | Até 2 dígitos      |
| urlPagamento             | Para o modelo redirect. Essa será a URL de redirecionamento da operação | Alfa Numérico | Até 500 caracteres |
| statusTransacao          | Status atual da transação                                               | Numérico      | Até 2 dígitos      |
| autorizacao              | Código de autorização da adquirente                                     | Numérico      | Até 20 dígitos     |
| codigoTransacaoOperadora | <a href="/gateway/rest/codigos-da-api-rest/#status-de-transacao" target="_blank" class="linkPadraoVerde">Status atual da transação</a>                                       | Numérico      | Até 20 dígitos     |
| dataAprovacaoOperadora   | Data de aprovação na adquirente                                         | Alfa Numérico | Até 10 dígitos     |
| numeroComprovanteVenda   | Número do comprovante de venda                                          | Alfa Numérico | Até 20 dígitos     |
| nsu                      | Número de NSU                                                           | Alfa Numérico | Até 10 dígitos     |
| mensagemVenda            | Mensagem de retorno da adquirente                                       | Alfa Numérico | Até 50 dígitos     |
| cartoesUtilizados        | Número de cartão truncado utilizado na transação                        | Alfa Numérico | Até 20 dígitos     |
