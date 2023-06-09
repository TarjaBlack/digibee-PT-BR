---
description: Veja a seguir um exemplo de uso do componente For Each.
---

# For Each: exemplo de uso

O objetivo do componente _**For Each**_ é percorrer um _array_ JSON e, para cada item do _array_, acionar um _subpipeline_.

**1) Obtenha um exemplo de JSON **_**array**_** através de uma chamada ao seguinte endereço**: [https://viacep.com.br/ws/RS/Porto%20Alegre/Domingos/json/](https://viacep.com.br/ws/RS/Porto%20Alegre/Domingos/json/)

Para este passo, utilize também o componente REST.

**2)** **O resultado da execução descrita no passo anterior deve retornar uma lista de endereços**. Esses endereços estão contidos no objeto "body". Observe:

![](<../../../.gitbook/assets/for each usos.png>)



**3)** **Com uma lista para o **_**For Each**_** percorrer, arraste o ícone do componente até a área de construção do **_**pipeline**_.

**4) Clique no ícone do **_**For Each**_** para abrir as suas configurações e especificar a expressão JSON Path**. É por meio dessa expressão que:

* se especifica o _array_ a ser iterado;
* se adicionam filtros para iterar outros itens.

**Exemplos**

* **$.body:** percorre o _array body_ inteiro.
* **$.body.\[?(@.bairro == 'Cristo Redentor')]:** percorre o _array_ somente quando o atributo "bairro" for igual a "Cristo Redentor".

**5) Acesse o ícone do **_**For Each**_** novamente para configurar o **_**subpipeline**_** de execução para cada linha.**

![](<../../../.gitbook/assets/for each usos1.png>)



{% hint style="info" %}
É necessário existir ao menos um componente no _subpipeline_.
{% endhint %}

**6)** **Após desenhar o fluxo, execute o **_**pipeline**_** e observe que na saída do JSON é demonstrado um totalizador de execução**. Para que a execução seja contabilizada como "sucesso", adicione a mensagem _"success" : true_ no último passo do _subpipeline_.

**Exemplo**

Copie o conteúdo abaixo e cole na sua área de construção do _pipeline_ utilizando o comando "Ctrl + v" (se utilizar Windows) ou "Command + v" (se utilizar MAC).

```
[{"data":{"type":"connector","name":"rest-connector","stepName":"chamada a serviço que retorna lista","params":{"url":"https://viacep.com.br/ws/RS/Porto%20Alegre/Domingos/json/","header:content-type":"application/json","operation":"GET","connectTimeout":30000,"readTimeout":30000,"advanced":false},"accountLabel":"","id":"0cbd5b18-ac1b-47b4-9060-559fa8f1cd65","key":"component@connectorrest-connector"},"position":{"x":173,"y":66.5},"group":"nodes","removed":false,"selected":true,"selectable":true,"locked":false,"grabbable":true,"pannable":false,"classes":"eh-preview-active"},{"data":{"type":"connector","name":"for-each-connector","onProcessTrack":{"edges":[{"removed":false,"classes":"","position":{"x":0,"y":0},"locked":false,"data":{"source":"start-track","target":"7d0ab0cc-88b8-41ed-96e3-911cd9699b45","data":{"id":"3a7420c1-1c7b-4204-bda4-539416bfed20","type":"default"},"id":"aa4bd7f0-b70d-484c-8d81-98d386172d0c"},"pannable":true,"grabbable":true,"selectable":true,"selected":false,"group":"edges"},{"removed":false,"classes":"","position":{"x":0,"y":0},"locked":false,"data":{"source":"7d0ab0cc-88b8-41ed-96e3-911cd9699b45","target":"7c389a95-cbde-4ec0-9ce2-70916d1352c2","data":{"id":"fb250837-fd43-45ce-87bc-4cf5c58fe6c8","type":"default"},"id":"29527300-6a86-4975-b377-8407672ba2ec"},"pannable":true,"grabbable":true,"selectable":true,"selected":false,"group":"edges"},{"removed":false,"classes":"","position":{"x":0,"y":0},"locked":false,"data":{"source":"eb7bbaa4-0036-4ff3-b1fa-46d346e0817f","target":"7fd5e6be-6757-4c3d-8507-b77020179b02","data":{"id":"7239c7fa-2c8e-4868-be6d-b4d55f7ee712","type":"default"},"id":"244b736a-98e5-4e99-8e6e-fb838958c9ab"},"pannable":true,"grabbable":true,"selectable":true,"selected":false,"group":"edges"},{"removed":false,"classes":"","position":{"x":0,"y":0},"locked":false,"data":{"source":"3146be4d-5901-4494-b58e-4650e012fb13","target":"a8593f14-50e7-4bd5-a4d1-7bfd305986e7","data":{"id":"63e548b1-471f-43d6-8a85-18ebf92f98e7","type":"default"},"id":"735aad8e-038d-40d1-a15d-5a24d37078f0"},"pannable":true,"grabbable":true,"selectable":true,"selected":false,"group":"edges"},{"removed":false,"classes":"","position":{"x":0,"y":0},"locked":false,"data":{"source":"7c389a95-cbde-4ec0-9ce2-70916d1352c2","target":"eb7bbaa4-0036-4ff3-b1fa-46d346e0817f","data":{"id":"eccb5c57-34c6-425f-acdf-35cf1c8aa453","type":"default"},"id":"877094e9-3b29-46ef-a485-90d5be2db5d4"},"pannable":true,"grabbable":true,"selectable":true,"selected":false,"group":"edges"},{"removed":false,"classes":"","position":{"x":0,"y":0},"locked":false,"data":{"source":"7fd5e6be-6757-4c3d-8507-b77020179b02","target":"3146be4d-5901-4494-b58e-4650e012fb13","data":{"id":"092b7411-3c12-4665-8c24-c1450cb3f85e","type":"default"},"id":"bc307fbd-99f6-4f0d-9d02-12bb239bcab6"},"pannable":true,"grabbable":true,"selectable":true,"selected":false,"group":"edges"}],"nodes":[{"removed":false,"classes":"","position":{"x":41,"y":80},"locked":false,"data":{"type":"start-track","id":"start-track","key":"start-track@not-configured"},"pannable":false,"grabbable":true,"selectable":false,"selected":false,"group":"nodes"},{"removed":false,"classes":"","position":{"x":188,"y":80},"locked":false,"data":{"type":"transformer","stepName":"Pega o Campo CEP e modifica a estrutura, colocando no objeto 'url'","transformSpec":"[\n  {\n    \"operation\": \"shift\",\n    \"spec\": {\n      \"cep\": \"url.cep\"\n    }\n  }\n]","id":"7d0ab0cc-88b8-41ed-96e3-911cd9699b45","key":"component@transformertransformer"},"pannable":false,"grabbable":true,"selectable":true,"selected":false,"group":"nodes"},{"removed":false,"classes":"","position":{"x":497,"y":80},"locked":false,"data":{"type":"connector","name":"rest-connector","stepName":"chamada ao um serviço externo","params":{"url":"https://viacep.com.br/ws/$EXPAND{:cep,}/json/","header:content-type":"application/json","operation":"GET","connectTimeout":30000,"readTimeout":30000,"advanced":false},"accountLabel":"","id":"eb7bbaa4-0036-4ff3-b1fa-46d346e0817f","key":"component@connectorrest-connector"},"pannable":false,"grabbable":true,"selectable":true,"selected":false,"group":"nodes"},{"removed":false,"classes":"","position":{"x":799,"y":80},"locked":false,"data":{"type":"connector","name":"log-connector","stepName":"Log-Connector","params":{"logLevel":"INFO","message":"cepParam: #{url.cep} ; response: #{body}"},"id":"3146be4d-5901-4494-b58e-4650e012fb13","key":"component@connectorlog-connector"},"pannable":false,"grabbable":true,"selectable":true,"selected":false,"group":"nodes"},{"removed":false,"classes":"","position":{"x":344,"y":80},"locked":false,"data":{"type":"session-management","stepName":"salva dados relevantes para este fluxo","operation":"PUT","sessionType":"LOCAL","scoped":true,"fields":["url"],"id":"7c389a95-cbde-4ec0-9ce2-70916d1352c2","key":"component@session-managementsession-management"},"pannable":false,"grabbable":true,"selectable":true,"selected":false,"group":"nodes"},{"removed":false,"classes":"","position":{"x":651,"y":80},"locked":false,"data":{"type":"session-management","stepName":"recupera informações salvas no fluxo.","operation":"GET","sessionType":"LOCAL","scoped":true,"fields":["url"],"id":"7fd5e6be-6757-4c3d-8507-b77020179b02","key":"component@session-managementsession-management"},"pannable":false,"grabbable":true,"selectable":true,"selected":false,"group":"nodes"},{"removed":false,"classes":"","position":{"x":956,"y":80},"locked":false,"data":{"type":"transformer","stepName":"adicionar success para contabilizar o registro","transformSpec":"[\n  {\n    \"operation\": \"default\",\n    \"spec\": {\n      \"success\": true\n    }\n  }\n]","id":"a8593f14-50e7-4bd5-a4d1-7bfd305986e7","key":"component@transformertransformer"},"pannable":false,"grabbable":true,"selectable":true,"selected":false,"group":"nodes"}]},"stepName":"itera os registros de body","params":{"jsonPath":"$.body","parallel":false,"onProcess":"start-track"},"id":"c26a2684-610c-44cf-b5f1-1ca093cc9bb4","key":"component@connectorfor-each-connector"},"position":{"x":319,"y":66.5},"group":"nodes","removed":false,"selected":true,"selectable":true,"locked":false,"grabbable":true,"pannable":false,"classes":""},{"data":{"id":"47080cfd-e0f1-4310-af7f-9c8eef40e54c","source":"0cbd5b18-ac1b-47b4-9060-559fa8f1cd65","target":"c26a2684-610c-44cf-b5f1-1ca093cc9bb4","data":{"type":"default","conditionType":null,"conditionRule":null,"condition":null,"label":null}},"position":{"x":0,"y":0},"group":"edges","removed":false,"selected":true,"selectable":true,"locked":false,"grabbable":true,"pannable":true,"classes":""}]
```

\
