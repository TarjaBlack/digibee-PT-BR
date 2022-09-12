# Totvs Live: Consultar Status Ticket

### Biblioteca <a href="#biblioteca" id="biblioteca"></a>

Totvs Live

### Serviço <a href="#servio" id="servio"></a>

Consultar Status Ticket

### Descrição <a href="#descrio" id="descrio"></a>

Este conector encapsula a chamada do método ConsultarStatusTicketLC\_Integracao na API do Totvs Live.

### Parâmetros de configuração do conector <a href="#parmetros-de-configurao-do-conector" id="parmetros-de-configurao-do-conector"></a>

* **ws-live-url**: url da instância do Totvs Live.

### Entrada <a href="#entrada" id="entrada"></a>

```
{  
    "chaveAcesso":"00000000-00000000-00000000-00000000",  
    "codigoSistemaSatelite":"000000000",  
    "numeroTicket": "0999999999999999",  
    "manter":"qualquer valor que queira manter na saída do conector"
}
```

### Saída <a href="#sada" id="sada"></a>

#### Sucesso <a href="#sucesso" id="sucesso"></a>

```
{
   "encontrouRegistros": true|false,
   "status": 200,
   "processStatus": "ERROR|PROCESSING|SUCCESS",
   "items": [],
   "numeroTicket"
   "manter": "qualquer valor que tiver sido passado aqui será mantido"
}

Regras de Process Status
------------------------
- Se algum item está aguardando processamento PROCESSING
- Se algum item (está com erro ou foi processado mas está com mensagem de erro) e não há nenhum em processamento ERROR
- Se foi processado com erro inexistente e não está em processamento SUCCESS

```

**Erro**

```
{   
    "timestamp": 1559243275088,   
    "error": "Não foi possível consultar ticket.",   
    "code": 500,   
    "manter": "qualquer valor que tiver sido passado aqui será mantido"
}
```

\
