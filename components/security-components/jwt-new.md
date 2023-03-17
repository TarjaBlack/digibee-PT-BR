---
description: Conheça o componente e saiba como utilizá-lo.
---

# JWT

O _**JWT**_ realiza criação de JWS e JWE assim como a verificação de JWS e decodificação de JWE.

Dê uma olhada nos parâmetros de configuração do componente:

* **Operation:** "_Generate JWS_" realiza a criação de _tokens_ JWS. "_Generate JWE_" realiza a criação de _tokens_ JWE. "_Verify JWS_" verifica a assinatura de um _token_ JWS e "_Decode JWE_" descriptografa o _token_ JWE e retorna o _payload_ desse _token_.
* **Public Key:** conta do tipo PUBLIC-KEY utilizada para assinar _tokens_ JWS com os seguintes algoritmos: RS256, RS384, RS512, PS256, PS384 e PS512. Utilizada também para criptografar _tokens_ JWE com os seguintes algoritmos: RSA1\_5, RSA-OAEP e RSA-OAEP-256. A chave pública deverá ser do tipo RSA e derivada de uma chave privada de no mínimo 2048 bits.
* **Private Key:** conta do tipo PRIVATE-KEY utilizada para verificar _tokens_ JWS com os seguintes algoritmos: RS256, RS384, RS512, PS256, PS384 e PS512. Utilizada também para descriptografar _tokens_ JWE com os seguintes algoritmos: RSA1\_5, RSA-OAEP e RSA-OAEP-256. A chave privada deverá ser do tipo RSA e de no mínimo 2048 bits.
* **Secret Key:** conta do tipo SECRET-KEY utilizada para assinar _tokens_ JWS com os seguintes algoritmos: HS256, HS384 e HS512. Utilizada também para criptografar e descriptografar _tokens_ JWE com os seguintes algoritmos: A128KW, A192KW, A256KW, A128GCMKW, A192GCMKW e A256GCMKW.
* **Key as Base64:** se habilitada, a conta _Secret Key_ deverá estar no formato base64; do contrário, deverá conter o valor da chave a ser utilizada.
* **Key Charset:** se a propriedade _Key as Base64_ estiver habilitada, o _charset_ da chave deve ser informado.
* **JWS Algorithm:** algoritmos utilizados para assinar e verificar _tokens_ JWS, sendo eles: HS256, HS384, HS512, RS256, RS384, RS512, PS256, PS384 e PS512.
* **JWE Algorithm:** algoritmos utilizados para criptografar e descriptografar _tokens_ JWE, sendo eles: A128KW, A192KW, A256KW, A128GCMKW, A192GCMKW, A256GCMKW, RSA1\_5, RSA-OAEP e RSA-OAEP-256.
* **Encrypted Payload Algorithm:** algoritmos utilizados para criptografar e descriptografar o payload dos tokens JWE, sendo eles: A128KW, A192KW, A256KW e A256GCM .
* **Issuer (iss):** a _claim_ "iss" (_issuer_) identifica o principal que emitiu o JWT. O processamento dessa _claim_ é geralmente específico da aplicação. O uso dessa _claim_ é opcional.
* **Expiration Time (exp):** a _claim_ "exp" (_expiration time_) identifica o tempo de expiração no qual ou após o qual o JWT NÃO DEVE ser aceito para processamento. O processamento da solicitação "exp" exige que a data / hora atual DEVEM ser anteriores à data / hora de vencimento listada na solicitação "exp". O uso dessa _claim_ é opcional.
* **Issued at (iat)**: a _claim_ "iat" (Issued at) identifica a hora em que o JWT foi emitido. Essa declaração pode ser utilizada para determinar a idade do JWT. O seu valor DEVE ser um número. O uso dessa _claim_ é opcional.
* **Subject (sub):** a _claim_ "sub" (subject) identifica o assunto do JWT. As afirmações em um JWT são normalmente afirmações sobre o assunto. O valor do assunto DEVE ter como escopo ser exclusivo localmente no contexto do emissor ou ser globalmente exclusivo. O processamento dessa _claim_ é geralmente específico da aplicação. O uso dessa _claim_ é opcional.
* **Token Id (jti):** a _claim_ "jti" (JWT ID) fornece um identificador exclusivo para o JWT. O valor do identificador DEVE ser atribuído de maneira a diminuir ao máximo as chances de que o mesmo valor seja acidentalmente atribuído a um objeto de dados diferentes. Se o aplicativo utilizar vários emissores, as colisões DEVEM ser evitadas também entre os valores produzidos por diferentes emissores. A _claim_ "jti" pode ser utilizada para evitar que o JWT seja repetido. O uso dessa _claim_ é opcional.
* **Audience (aud):** valor único. A _claim_ "aud" (público) identifica os destinatários do JWT. Cada principal que pretende processar o JWT DEVE se identificar com um valor na reivindicação dentro da _claim_. Se o responsável pelo processamento da _claim_ não se identificar com um valor na _claim_ "aud" quando essa _claim_ estiver presente, o JWT DEVE ser rejeitado. O uso dessa _claim_ é opcional.
* **Not Before (nbf):** a _claim_ "nbf" (não antes) identifica o tempo antes do qual o JWT NÃO DEVE ser aceito para processamento. O processamento da reclamação "nbf" requer que a data / hora atual SEJA posterior ou igual à data / hora não anterior listada na reclamação "nbf". Os implementadores PODEM prever uma pequena margem de segurança - geralmente não mais do que alguns minutos - para compensar a distorção do relógio. O seu valor DEVE ser um número. O uso dessa _claim_ é opcional.
* **Custom Claims:** para especificar _claims_ customizadas basta informar a chave (nome da _claim_) e o valor da _claim_.
* **Custom Headers:** para especificar _headers_ customizados, basta informar a chave e o valor do _header_ nos respectivos campos.
* **JWE:** campo para informar o _token_ JWE.
* **JWS:** campo para informar o _token_ JWS.
* **Payload Charset**: _charset_ do _payload_ utilizado na criação de _tokens_ JWE. Valor padrão: UTF-8
* **Payload**: _payload_ que será utilizado na criação do _token_ JWE.
* **Use JWK:** se a opção estiver habilitada, um JWK é esperado para verificar o _token_ JWT. Esta opção está disponível apenas se _Verify JWS_ estiver selecionada no parâmetro **Operation**. O **Use JWK** também desabilita todas as opções de conta (parâmetros **Secret Key, Private Key** e **Public Key**), além dos parâmetros **Key Charset, Key as Base64** e **JWS Algorithm**.
* **JWK:** JWK que será utilizado para verificar o _token_ JWS.
* **Fail On Error:** se a opção estiver habilitada, a execução do _pipeline_ com erro será interrompida; do contrário, a execução do _pipeline_ continua, mas o resultado vai mostrar um valor falso para a propriedade "success".

Alguns dos parâmetros acima aceitam _Double Braces_. Para entender melhor como funciona essa linguagem, leia a [documentação](../../build/double-braces/).

## Fluxo de mensagens <a href="#h_a232432467" id="h_a232432467"></a>

### **Entrada** <a href="#h_eec5380fa4" id="h_eec5380fa4"></a>

Não é esperado uma mensagem de entrada específica, bastando apenas preencher os campos necessários de cada operação.

### Saída <a href="#h_cd13e15440" id="h_cd13e15440"></a>

Para as operações “_Generate JWS_”:

```
{
"success": true,
"jws": "<JWS TOKEN>",
}
```

Para as operações “_Generate JWE_":

```
{
"success": true,
"jwe": "<JWE TOKEN>",
}
```

Para as operações “_Verify JWS_":

```
{
"success": true,
"verified": true,
"claims": [
"subject": ".....",
"issuedAt": 11111111
]
}
```

Para as operações “_Decode JWE_":

```
{
"success": true,
"payload": "<PAYLOAD DESCRIPTOGRAFADO>"
}
```

