---
description: Saiba como baixar o arquivo de configuração do digibeectl.
---

# Como obter arquivo de configuração do digibeectl

Para iniciar o uso do _digibeectl_ é necessário baixar o arquivo de configuração criptografado que irá gerar um token único e exclusivo para acesso aos recursos do digibeectl.\
\
\
Para baixar o arquivo basta estar logado na Digibee Integration Platform e seguir este passo a passo:

1\. Clique no botão 'Administração'&#x20;

![](<../../.gitbook/assets/01 (3).png>)

\
2\. Clique em 'digibeectl' e em seguida clique no botão 'Criar'.

![](<../../.gitbook/assets/02 (21).png>)

3\. Atribua um título ao seu Token

![](<../../.gitbook/assets/03 (7).png>)

4\. Adicione as permissões desejadas ao token. Se houver dúvidas de quais fornecer, consulte todas as permissões necessárias para os comandos disponíveis clicando [aqui](./).

![](<../../.gitbook/assets/04 (4).png>)

5\. Selecione um prazo para a expiração do token. O prazo pode ser configurado para ter uma duração mínima de 1 hora e duração máxima de até 1 ano.

![](<../../.gitbook/assets/05 (5).png>)

\
6\. Salve as configurações de permissões e expiração.\


7\. Copie a chave de criptografia gerado pela plataforma através do botão de copiar e salve o conteúdo para utilizá-lo posteriormente.\
Em seguida, defina a senha de criptografia do seu arquivo.\
\
ATENÇÂO: Guarde a senha e chave em um local seguro pois elas não podem ser recuperadas.

![](<../../.gitbook/assets/06 (8).png>)

8\. Agora é só salvar e baixar o arquivo gerado.

9\. Após a instalação do digibeectl utilize o comando abaixo com os dados que você acabou de configurar:

```
digibeectl set config --file "path/file.json" --secret-key "chave-de-criptografia" --auth-key "senha-de-criptografia"
```

\


Para acessar o Guia de uso completo do digibeectl clique [aqui](./).
