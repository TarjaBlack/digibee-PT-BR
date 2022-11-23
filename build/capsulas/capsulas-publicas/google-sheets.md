---
description: Saiba quais são as Cápsulas disponíveis nessa Coleção.
---

# Google Sheets

Leia dados e escreva informações na sua planilha Google.

### Pré requisitos <a href="#h_2a61515a36" id="h_2a61515a36"></a>

#### 1) Ativação do Serviço Google Sheet API <a href="#h_a711816954" id="h_a711816954"></a>

Para utilizar os serviços Google Sheets, você precisa ativar o recurso _**Google Sheets API**_ no seu console GCP (_Google Cloud Platform_). Para saber mais sobre ativação de serviços, leia o artigo [Como ativar e desativar serviços](https://cloud.google.com/service-usage/docs/enable-disable).

#### 2) Autenticação <a href="#h_3ac164272d" id="h_3ac164272d"></a>

É necessário ter uma conta Digibee do tipo **google-key**. Se você ainda não possui, clique [aqui](https://console.cloud.google.com/iam-admin/serviceaccounts?hl=pt-br) para acessar as contas de serviço no seu [Console GCP](https://console.cloud.google.com/iam-admin/serviceaccounts?hl=pt-br) e criar uma nova chave. Para obter mais informações sobre como gerar uma nova chave de autenticação, leia o artigo [Criar e gerenciar chaves de contas de serviço](https://cloud.google.com/iam/docs/creating-managing-service-account-keys?hl=pt-br#iam-service-account-keys-list-console).

#### 3) Compartilhamento <a href="#h_75f8b6b3cc" id="h_75f8b6b3cc"></a>

A conta de serviço gerada anteriormente possui um _service account email_. Utilize o endereço para compartilhar, em modo edição, a planilha que receberá os dados.

#### 4) Tratamento de erros <a href="#h_66215462e8" id="h_66215462e8"></a>

Todas as Cápsulas possuem retornos padronizados. Sempre que a solicitação for processada com sucesso, será devolvido o campo “success” do tipo booleano na raiz do JSON. Utilize essa informação para realizar os tratamentos de erro no seu _pipeline_.

## Cápsulas Google Sheets <a href="#h_6d29387461" id="h_6d29387461"></a>

### Get Spreadsheets By Id <a href="#h_c3f95ada97" id="h_c3f95ada97"></a>

Esta Cápsula possibilita a consulta de metadados de uma Planilha Google.

**Exemplo:**

* **URL:** endereço para acesso através do navegador
* **Sheets:** lista das páginas existentes dentro da planilha
* **Title:** nome da planilha

### Get Rows Values by Range <a href="#h_eedd5427c7" id="h_eedd5427c7"></a>

Esta Cápsula tem a capacidade de ler dados da Planilha Google. É necessário especificar o nome da página, o intervalo de colunas e os parâmetros para controle de paginação.

**Exemplo:**

Para ler os dados das colunas A, B, C, D, E, F, G, H, I, J, K, L da linha 1 até a linha 100, estes devem ser os parâmetros:

* **First Column**: A
* **Last Column:** L
* **Start Row:** 1
* **Limit Row:** 100

### Append Data <a href="#h_4c8d1e9c75" id="h_4c8d1e9c75"></a>

Esta Cápsula simplifica a gravação de dados na sua Planilha Google graças a sua capacidade de gravar uma única linha ou uma lista.

É necessário especificar o nome da página onde os dados serão gravados. Se não houver essa especificação, a gravação será feita na primeira página encontrada.

Não é necessário especificar o intervalo de colunas. No entanto, é preciso informar a partir de qual coluna e linha a escrita dos dados deve ser feita. Os valores serão adicionados sempre depois da última linha.

**Exemplo:**

_Array_ passado para a Cápsula por meio de expressões _Double Braces_.

![](<../../../.gitbook/assets/01 (14).png>)

{% hint style="info" %}
**IMPORTANTE:** a Cápsula “Append Data” possui características que impossibilitam a escrita de dados na mesma página da sua planilha. Em caso de escritas realizadas simultaneamente, os dados podem ser sobrescritos pelas requisições. Não utilize em fluxos que permitam o paralelismo.
{% endhint %}

Os dados do JSON serão transformados em colunas, respeitando a ordem dos atributos enviados e não a nomenclatura. Caso precise reorganizar os campos, utilize um de nossos componentes de transformação, assim como o [Transformer (JOLT)](../../../components/tools/transformer-jolt/).

Veja o exemplo a seguir:

```
[
  {
    "operation": "sort",
    "spec": {
      "*": ""
    }
  }
] 
```

\
