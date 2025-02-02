
# Validação de Telefones e Celulares com REGEX em JavaScript

Este projeto apresenta uma expressão regular (REGEX) para validação de números de telefone e celular no Brasil, incluindo suporte para DDI (+55) e DDD.





Regex para Javascript:
```javascript
let Regex = /(?:(?:^|\s)(?:[+]?55[-\.\ ]?)?(?:\(?[0]?(?:[14689][1-9]|2[12478]|3[1234578]|5[1345]|7[134579])\)?[-\.\ ]?)?(?:(?:[2-8]|9[-\.\ ]?[0-9]?)[0-9]{3}[.\-\ ]?[0-9]{4})(?=\.|\,|\s|$)))/gm;
```


## Telefones válidos 
- +55 (11) 98765-4321
- 55 21 2234-5678
- (31)98765.4321
- 4002-8922
- 40028922
- 01140028922
- 91239485




## Representação:


```mermaid
     graph TD;
A[DDI +55 Opcional] -->|Separador Opcional| B[DDD Opcional];
B -->|Separador Opcional| C[Início do Número]; C --> D[2 a 8];
C --> E[9];
E -->|Separador Opcional| F[1 dígito 0-9];
D --> G[3 dígitos 0-9];
F --> G;
G -->|Separador Opcional| H[4 dígitos 0-9];
   ```



# Estrutura do Regex

><strong>**`/`** : Início da expressão do Regex</strong>
>___
><strong>**`(?:`** : Grupo não capturante: Geral</strong>
>
><strong>**`(?:^|\s)`** : Considera apenas números que estão no ínicio do texto ou após um espaço.</strong>
>>---
>><strong>DDI: </strong>
>>Para reconhecer o DDI quando houver:
>>
>>```javascript
>>... (?:[+]?55[-\.\ ]?)? ...
>>```
>>
>>```
>>| (?:           | Início do grupo não capturante
>>| [+]?          | (Opcional ) Caractér "+"
>>| 55            | Código DDI
>>| [-\.\ ]?      | (Opcional) Caractér separador, podendo ser:
>>|               | -   Hífen (`-`),
>>|               | -   Ponto (`.`),
>>|               | -   Espaço (  ).
>>| )?            | Fim do grupo não capturante, o grupo é opcional
>>```
>>
>>`+` (usado para o código internacional)
>>Apenas funciona para o DDD 55 (Brasil).
>>
>>Exemplos válidos para o DDI:
>>-   `+55`: DDI iniciado com o "+";
>>-   `+55-`: DDI iniciado com "+" e com carácter separador ("."; "-"; "")
>>-   `55`: DDI sem ser iniciado com "+" sem caráter separador;
>>-   '55 '. DDI sem ser iniciado com "+" e separado por "( )"
>>---
> 
>>---
>><strong>Código DDD: </strong>
>>Para reconhecer o código DDD, quando houver:
>>```javascript
>>... (?:\(?[0]?(?:[14689][1-9]|2[12478]|3[1234578]|5[1345]|7[134579])\)?[-\.\ ]?)? ...
>>```
>>
>>```
>>| (?:           | Início do grupo não capturante
>>| \(?           | (Opcional ) Caractere "("
>>| [0]?          | (Opcional ) "0" - zero
>>| (?:           | Início do grupo de validação do DDD
>>| [14689][1-9]  | Iniciado por (1,4,6,8 ou 9) e seguido por (1 a 9).
>>| |2[12478]     | Iniciado por 2, e (1,2,4,7 ou 8).
>>| |3[1234578]   | Iniciado por 3, e (1,2,3,4,5,7 ou 8).
>>| |5[1345]      | Iniciado por 5, e (1,3,4 ou 5).
>>| |7[134579]    | Iniciado por 7, e (1,3,4,5,7 ou 9).
>>| )             | Fim do grupo de validação do DDD
>>| \)?           | (Opcional) Caractere  ")" 
>>| [-\.\ ]?      | (Opcional) Caractere separador, podendo ser:
>>|               | -   Hífen (`-`),
>>|               | -   Ponto (`.`),
>>|               | -   Espaço (  ).
>>| )?            | Fim do grupo não capturante, o grupo é opcional
>>```
>>Valida os estados abaixo:
>>
>>### DDD por Estado 
>>- **São Paulo:** 11 a 19 
>>- **Rio de Janeiro:** 21, 22, 24
>>- **Espírito Santo:** 27, 28
>>- **Minas Gerais:** 31 a 35, 37, 38
>>- **Paraná:** 41 a 46
>>- **Santa Catarina:** 47 a 49
>>- **Rio Grande do Sul:** 51, 53, 54, 55
>>- **Distrito Federal/Goiás:** 61
>>- **Goiás:** 62
>>- **Tocantins:** 63
>>- **Goiás:** 64
>>- **Mato Grosso:** (65, 66)
>>- **Mato Grosso do Sul:** (67)
>>- **Acre:** (68)
>>- **Rondônia:** (69) 
>>- **Bahia:** (71, 73 a 75, 77)
>>- **Sergipe:** (79) 
>>- **Pernambuco:** (81)
>>- **Alagoas:** (82)
>>- **Paraíba:** (83)
>>- **Rio Grande do Norte:** (84) 
>>- **Ceará:** (85)
>>- **Piauí:** (86)
>>- **Pernambuco:** (87)
>>- **Ceará:** (88) 
>>- **Piauí:** (89)
>>- **Pará:** (91)
>>- **Amazonas:** (92)
>>- **Pará:** (93, 94)
>>- **Roraima:** (95)
>>- **Amapá:** (96)
>>- **Amazonas:** (97) 
>>- **Maranhão:** (98, 99)
>>---
>
>>---
>><strong>Número do Telefone ou Celular: </strong>
>> Valida o número do telefone ou celular
>>
>>```javascript
>>... (?:(?:[2-8]|9[-\.\ ]?[0-9])[0-9]{3}[.\-\ ]?[0-9]{4}) ...
>>```
>>
>>>---
>>><strong>Início do número:</strong>
>>> O Início do número, pode ser (2 a 8) para telefones ou 9 para celular.
>>> Se 9, pode ter um caractere separador e deve ser seguido por um número de (0 a 9):
>>> Ou pode ser um celular sem o nono dígito.
>>>
>>>```
>>>| (?:              | Início do grupo não capturante do número
>>>| (?:              | Início do grupo não capturante início do número
>>>| [2-8]            | O telefone pode iniciar pelos números de (2 a 8),
>>>| |9[-\.\ ]?[0-9]?  | Ou, iniciado por 9, pode ter um caractere separador  ('-', '.' ou ' ') e pode ou não ser seguido por um número de (0 a 9).
>>>| )                | Fim do grupo não capturante início do número
>>>| )                | Fim do grupo não capturante do número
>>>```
>>>---
>>
>>>---
>>><strong>Meio do número:</strong>
>>>```
>>>[0-9]{3}[.\-\ ]?
>>>```
>>>Após o início do número, tem 3 números que pode ser de (0 a 9), e pode ter um caractere separador ('-', '.' ou ' ').
>>>---
>>
>>>---
>>><strong>Fim do número:</strong>
>>>```
>>>[0-9]{4}
>>>```
>>>Deve ter 4 dígitos de (0 a 9).
>>>
>>
>
>---
>
><strong>**`(?=\.|\,|\s|$))`** : Considera apenas números que estão no fim do texto, anterior a um espaço, virgula ou ponto final.</strong>
>
>`)` :  Fim do Grupo Não Gapturante: Geral
>
>---
>`/gm`** : Fim da expressão do Regex

## Referências
[Imaginamundo - # Regex para telefones do Brasil](https://gist.github.com/imaginamundo/d689b211e640f40d445a9146fdace407)

[Blog.dp6.com.br](https://blog.dp6.com.br/regex-o-guia-essencial-das-express%C3%B5es-regulares-2fc1df38a481)
Guia de expressões

## Utilidades

[Stackedit.io](https://stackedit.io/app#)
Editor de Markdown

[RegexR](https://regexr.com/)
Testador de expressões regulares com destaque de sintaxe.

[Regex101](https://regex101.com/)
Testador de expressões regulares.

[Markdownguide](https://www.markdownguide.org/basic-syntax/#links)
Referências de Markdown

[Commonmark.org](https://commonmark.org/help/)
Referências de Markdown

[Luong-komorebi/Markdown-Tutorial](https://github.com/luong-komorebi/Markdown-Tutorial/blob/master/README_pt-BR.md)
Referências de Markdown
