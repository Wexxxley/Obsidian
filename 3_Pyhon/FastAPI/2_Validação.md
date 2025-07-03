  
___
### **1.1 Pydantic e validação completa**
 O Pydantic permite criar classes com validação de dados automática baseada em anotações de tipo.

**BaseModel**: Classe base para definir modelos de dados com validação automática. Ao herdar dela, seus atributos são automaticamente verificados quanto ao tipo, obrigatoriedade, etc.  
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe3kLWjpvO57LRpg-VtM4mQLxGogPIUh0bxbLzwzKp86sDPLZhDVu67SKU-PV_YweDW_JqB7CJeb1Dr9U_bn2k84t1SuuV_HvExu2q8cyrJ0vKX16VLnp5fogZUUx4-e56whNIIug?key=jnfZcvbkf1zKPUZCAbeT6ysv)

Validações automáticas: O Pydantic já valida tipos básicos: str, int, bool, float, list, etc.Também converte tipos automaticamente se possível (ex: "25" → 25).
  
Validações prontas: 
- EmailStr: valida e-mails
- HttpUrl: valida URLs
- PositiveInt, NegativeInt: restringem sinal de inteiros

**Field():** Permite validar as propriedades:
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXehyP_RCVy118OkxWW-z8oC3Jq9ZXcu5NHqsIi2hVOFYeMjuwCLDCI8yX2VpEkBQr5hnFoCpbCmdo9Bl6MqUX8VJcBtm7C0IUH9pLlZTg6NXeGAyxmHXQ4j-bM_tZte5060oond?key=jnfZcvbkf1zKPUZCAbeT6ysv)

**Retornando status code**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeqqBe8RbHYSm4YaEpI7EZCFNdFfB5gc2vFr_nfDCAFEt3vH7SbaU87vKqWvfh5LqpS1xXE8Ki3WcdMREkW7NzteO2qYYlEqwUURIxdXtZMaMwu_y2mOBWDjgPYCz489Jm6y4DHVw?key=jnfZcvbkf1zKPUZCAbeT6ysv)
