  
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
    
- constr, conint, confloat: criam restrições como tamanho, valor mínimo/máximo
    

  

Field(): Permite validar as propriedades:

- Valor padrão
    
- Restrições (min_length, ge(valor minimo), le(valor maximo), etc.)
    
- Descrição e título do campo
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXehyP_RCVy118OkxWW-z8oC3Jq9ZXcu5NHqsIi2hVOFYeMjuwCLDCI8yX2VpEkBQr5hnFoCpbCmdo9Bl6MqUX8VJcBtm7C0IUH9pLlZTg6NXeGAyxmHXQ4j-bM_tZte5060oond?key=jnfZcvbkf1zKPUZCAbeT6ysv)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeK_-PHX4of73UOxASbsQ6I2FaVc18SixFYqt2N6FJ6WjLhs501qHegA8eFxzkUbHCG1ehc6-P-fcD2Zuh0YUk1AbDQu9tiqNZWiLYXmDYM0FaImaJo_ucmGJHeDNVcnmjOEYVrxQ?key=jnfZcvbkf1zKPUZCAbeT6ysv)

- model_dump(): Converte os dados recebidos em um dicionário.
    
- O ** desempacota esse dicionário como argumentos nomeados para o construtor da classe Book.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcW5T6-jcdYkIIaKdQ3YQ5Mt-c_fEaZEEo5pMM4O7oqQmGZtbqyVCRqSQpeepzh1haEcVjzwzi86Xff2BMwbzE9zs3G9QRxGQTcNDDn2i-LP6EQuVWTi6M3Sa6f1ru1QHbMoR53IQ?key=jnfZcvbkf1zKPUZCAbeT6ysv)

  

Validando os parâmetros de rota e de query

Para parâmetros de rota.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXc2nFeHEGc2Q7H5_WIiiMaeyhaETzAgANRlzMBn5MyMqXPyv913Q6ZDoSb8AP8fPGb-ebQe3wxLNyqa4Z1ipijjvVHoqIicYxLXzt00vQ3vTFYYKZnO7u4cyoyP36ktABbzh4G36Q?key=jnfZcvbkf1zKPUZCAbeT6ysv)

Para parâmetros de query string

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd43_3G43m6rGPae3nuOPIBXo1MTNeP2tzHPn9avjSIuJpNHuKb628aM_YkzmZkyzgQUUP2bilAqEoa1kBsXqQwnBioOMefJUBvq3aaO9pH87z25-5zJNDLagOv9eWBA0WlNdWpgw?key=jnfZcvbkf1zKPUZCAbeT6ysv)

Retornando status code

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeqqBe8RbHYSm4YaEpI7EZCFNdFfB5gc2vFr_nfDCAFEt3vH7SbaU87vKqWvfh5LqpS1xXE8Ki3WcdMREkW7NzteO2qYYlEqwUURIxdXtZMaMwu_y2mOBWDjgPYCz489Jm6y4DHVw?key=jnfZcvbkf1zKPUZCAbeT6ysv)

  

___________________________________________________________________________

### 5.3 Logging

 Logging é o processo de registrar eventos (logs) que ocorrem durante a execução de um software. 

  

Por que fazer logging?

1. Auditoria e Rastreabilidade: Registrar ações críticas. Ex: Em sistemas bancários, logs ajudam a investigar transações suspeitas.
    
2. Análise de Incidentes: Reconstruir o que aconteceu antes de uma falha.
    
3. Conformidade: Atender a regulamentações que exigem registro de atividades. Ex: Sistemas de saúde devem logar acessos a dados sensíveis.
    

  

Níveis de Log 

1. DEBUG: Detalhes técnicos para desenvolvedores.
    
2. INFO: Confirmações de operações normais (ex: "Usuário 123 logou").
    
3. WARNING: Eventos anormais não críticos (ex: "Disco com 90% de uso").
    
4. ERROR: Falhas em funcionalidades (ex: "Falha ao salvar arquivo").
    
5. CRITICAL: Problemas graves que podem parar o sistema.
    

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfm2eEi0sk98SXICCRQjRwvoRH2g7Uq-k3jzaFN1Kq9-BI1heEZ1C-199U5gCWo8LzDDEQY7xcukTr30rlSxdv3LTGzaD_tltxOLHvXqV-5dewnh90tckefLlSSnRh-vtcKlkTV?key=jnfZcvbkf1zKPUZCAbeT6ysv)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXflCNUArXeBWEiaVvFXQ-0jBgnvbFX0kJXn1mXrT0gKPCdD73fP2WwMAF2EKqw1150MB2CocxGyQ6VGnMLadHcOC-a6OEmrc0E3xHDa17QJDwiEVeswc5KuuTMEx3KQEoCpWRkR?key=jnfZcvbkf1zKPUZCAbeT6ysv)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcdVRsrrEjUzJ32Pit40GulhskUzXjPdIry90TFLWrkSfovZB2iJUFsnWHS71Zdz0IE6TFn6_sxkqszsaIVV-Mm2TSbB4BtoAXpmFVZsXLOcJ0bvRJKqY5zvaxqp8duJ2iSyumgCg?key=jnfZcvbkf1zKPUZCAbeT6ysv)

  
  
**