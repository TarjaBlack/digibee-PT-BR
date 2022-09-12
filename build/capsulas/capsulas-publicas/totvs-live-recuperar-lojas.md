# Totvs Live: Recuperar Lojas

### Biblioteca <a href="#biblioteca" id="biblioteca"></a>

Totvs Live

### Serviço <a href="#servio" id="servio"></a>

Recuperar Lojas

### Descrição <a href="#descrio" id="descrio"></a>

Este conector encapsula a chamada do método RecuperarLojasLC\_Integracao\_Xml na API do Totvs Live.

### Parâmetros de configuração do conector <a href="#parmetros-de-configurao-do-conector" id="parmetros-de-configurao-do-conector"></a>

* **ws-live-url**: url da instância do Totvs Live.

### Entrada <a href="#entrada" id="entrada"></a>

```
{  
    "retornaTodasLojas": "true",  
    "chaveAcesso":"00000000-00000000-00000000-00000000",  
    "codigoSistemaSatelite":"000000000",  
    "manter" "qualquer valor que queira manter na saida do conector"
}
```

### Saída <a href="#sada" id="sada"></a>

#### Sucesso <a href="#sucesso" id="sucesso"></a>

```
{
  "encontrouRegistros": true,
  "status": 200,
  "data": 30052019,
  "hora": 191120,
  "codigoSistemaSatelite": 999999999,
  "numeroTicketSaida": 999999999999,
  "lojas": [],
  "manter": "qualquer valor que tiver sido passado aqui será mantido"
}
```

#### Erro <a href="#erro" id="erro"></a>

```
{   
    "timestamp": 1559243275088,   
    "error": "Não foi possível recuperar lojas.",   
    "code": 500,   
    "manter": "qualquer valor que tiver sido passado aqui será mantido"
}
```

\
