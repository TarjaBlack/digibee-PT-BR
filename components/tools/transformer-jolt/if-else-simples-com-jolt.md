---
description: Aplicando Conditions em um JSON
---

# IF - ELSE simples com JOLT

Ao realizarmos um DE-PARA em um fluxo de integração, é muito comum precisarmos preencher um campo no lado PARA que não possui seu correspondente direto no lado DE.\
\
Entretanto, em algumas situações, podemos resolver esse tipo de problema com um simples "IF-ELSE", a partir dos próprios dados vindos do lado DE.&#x20;

### **Exemplo**

Tenho um JSON com dados de Cliente:

```
{  
    "cliente": {    
        "nome": "Cliente Fictício",    
        "idade": "32",    
        "estadoCivil": "Solteiro",    
        "paisOrigem": "Brasil"  
    }
}
```

\
A partir do JSON acima, preciso criar um novo JSON contendo apenas informações de **Nome** e **Nacionalidade** do Cliente:

```
{
  "cliente" : {
    "nome" : "Cliente Fictício",
    "nacionalidade" : "Brasileira"
  }
}
```

\
Para o campo **Nacionalidade** são aceitos apenas 2 valores:

* **Brasileira**
* **Estrangeira**

Entretanto, o primeiro JSON de Cliente não possui um campo Nacionalidade, apenas nos informa o país de origem do cliente.

Neste caso, conseguimos definir a nacionalidade do cliente a partir de seu país de origem.

Segue abaixo uma forma simples de resolvermos essa situação usando apenas um **Transformer Connector**.

### **Transformação e "IF-ELSE" com JOLT:**

```
[
  {
    "operation": "shift",
    "spec": {
      "cliente": {
        "nome": "cliente.nome",
        "paisOrigem": {
          "Brasil": {
            "#Brasileira": "cliente.nacionalidade"
          },
          "*": {
            "#Estrangeira": "cliente.nacionalidade"
          }
        }
      }
    }
  }
]
```

\
Na transformação acima, usamos o mesmo princípio de um **IF-ELSE** para verificar o valor de "paisOrigem".\
\
Caso seja "Brasil", preenchemos o campo "nacionalidade" com o valor "Brasileira".\
\
Caso o valor de "paisOrigem" seja qualquer país diferente de "Brasil", preenchemos "nacionalidade" com o valor "Estrangeira".

### **JSON final com Nome e Nacionalidade do Cliente:**

```
{
  "cliente" : {
    "nome" : "Cliente Fictício",
    "nacionalidade" : "Brasileira"
  }
}
```

\
