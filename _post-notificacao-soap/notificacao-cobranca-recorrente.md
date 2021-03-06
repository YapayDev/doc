---
title: Notificação cobrança recorrente
position: 2
menu: gateway
right_code: |
  ~~~ text
  POST HTTP
  Content-Type: application/x-www-form-urlencoded
  Content-Length: 125
  numeroRecorrencia=1&codigoEstabelecimento=1000000000000&campoLivre=A&campoLivre2=B&campoLivre3=C&campoLivre4=D&campoLivre5=E
  ~~~
  {: title="Exemplo de chamada" }
---

Neste fluxo de recorrência, o estabelecimento receberá a campainha informando qual recorrência houve a cobrança e, depois disto, deverá acionar a <a href="/gateway/consultas/#consulta-recorrente" target="_blank" class="linkPadraoVerde">consultarRecorrente</a> para receber o número do pedido, e assim, acionar a <a href="/gateway/consultas/#consultando-uma-transacao" target="_blank" class="linkPadraoVerde">consultarTransacao</a> para recebimento do status.

_Caso a URL de campainha estiver em HTTPS, informar ao Suporte Yapay, servicedesk@superpay.com.br_

Detalhamento dos campos retornados:

| Campo                 | Descrição                                                  | Tipo          |
|-----------------------|------------------------------------------------------------|---------------|
| numeroTransacao       | Código que identifica a transação dentro do SuperPay       | Numérico      |
| codigoEstabelecimento | Código que identifica o estabelecimento dentro do SuperPay | Numérico      |
| campoLivre1           | Campo Livre 1                                              | Alfa Numérico |
| campoLivre2           | Campo Livre 2                                              | Alfa Numérico |
| campoLivre3           | Campo Livre 3                                              | Alfa Numérico |
| campoLivre4           | Campo Livre 4                                              | Alfa Numérico |
| campoLivre5           | Campo Livre 5                                              | Alfa Numérico |
