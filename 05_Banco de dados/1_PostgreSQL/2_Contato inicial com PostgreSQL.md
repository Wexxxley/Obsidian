
---



___________________________________________________________________________
## 7. Join

 É usado para combinar duas ou mais tabelas com base em uma condição relacionada. Isso permite que você recupere dados de várias tabelas em uma única consulta.

  

1. Left join: Retorna todos os registros da tabela à esquerda e os registros correspondentes da tabela à direita, mesmo os que são nulos.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfPn3NC7nEwMjZ9vdO07ijlMQh6kuzfvj56i7m4M-u99ZSr4VTDarUFbycL2fLb8bMN2NWHX4sWBPxzJ6k-kOOBydV7otD8zQBwAqF8seH9r97Yy-SXgLSDvmdAYeiEUzSr7ojlm2WMKVQna6BD0GaMIIW4?key=jqcuw0c7mMfsTTEWWceZSw)

2. Inner Join: Retorna apenas os registros que têm correspondências em ambas as tabelas. Não retorna registros com valores nulos

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfjpPUztMzxitKDtHwq-cM80DtCyBs_ZpLR0QT8q1x9zXY2mjy5cECbvduAEV81KrwDTr0ipuNFCnQQPZiIaG43amYpeNr2iP7_4DFZznTB6DkEwh53CJ8mgmJaSG2LgEhRgnzUKhWs5E35CZ7jjaVPDHfq?key=jqcuw0c7mMfsTTEWWceZSw) 

  

3. Mais exemplos

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeZQvz7VLsRw6_P4dpQd71Os3cdg0C7jEAI6UhJAfw3u_1SGZhWDicnpBcVLODttDN-LAU4as1dLjIsSAcJ31gr4hs2TCriA8RgghVihcy0nx7SGanYEhMSF9hkD4UUsh8bxcIQA1Fw3Btfm_HI8QrP8-g?key=jqcuw0c7mMfsTTEWWceZSw)

___________________________________________________________________________

## 8. Comandos adicionais

<Extract: Usado para extrair partes específicas de um valor de data ou hora. Ela pode ser útil para recuperar informações como ano, mês, dia e hora.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXd5TbsMHwREAnOoGBxS4RRpEkR0NmaPjBGKzlkcxtojlkGy90jsLNKEcAA1m1sg4cxh4BKCqtjFRLcNV20vT1ZsePV0bni5B7cR8TvlJ13Ja9897xyDmuDW5WUCHrDNtlzR4mX2hiM-tv2fjdEnaYtTkqA?key=jqcuw0c7mMfsTTEWWceZSw)

  
  

<Substring: usada para extrair uma substring de uma string da tabela

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdvbYh5WA8zGlVkUEWkfgSfVebzKeSGQoTHp8hLjmzDM2DOMBlMWKvz9US6h5B8QiOtdZAFKhLWWK7MSxZQNOXUj5ifzT3foM8eDNQkaUu2iM4pS6tMjHWnVcRhlacOVjwcuqaNmTICWcSnZ2Yf2KACUbBt?key=jqcuw0c7mMfsTTEWWceZSw)

  

<Upper e lower

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcAsd-1xITHejOWHPapWxP57lY8pBGUU19iMcrvXhbOx7iFI_Hw6eQ-wjuJoNiQMH1eCIsOnqAlb8sQMxWG4qHwVcG_t6KncLf1kw_wON9G7aS0FuGaEQcMLcFec_BtQTjKTast4xNkQ593YhVgoE1jbx7V?key=jqcuw0c7mMfsTTEWWceZSw)

  

<Coalesce: cria mensagens personalizadas quando o valor é null

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe2whR2jzvsNlkGx1nobm-LeMQdw9IxMsGjjTu5wvzX63DYecwCAGP7qntvx0Bpd0npt5S_uN1uGAM5V5FP8PukfUGBIuU-mzt9w1rJ6jKalODbXwxirG9BIIkm6ZntYWF4R7WlFqfBd3GksGavVpT9oQWu?key=jqcuw0c7mMfsTTEWWceZSw)

  
  
  
  
  
  
  

<Case: é uma forma condicional de controlar o fluxo de uma consulta SQL. Ela permite que você execute diferentes ações com base em diferentes condições.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXexdYQLPL8c_WRTEBu98CV3rTAyvNXxSxgsi_84aPf6HxCDkto9dxzOPyKqYLi3TZp53i7dtr6mfklp816SIHwpOVUPCMkZlG1HZn9uAkXQPN1Dx7GSmjXXLhCsJop5McuMjxSuab8g5h2Rm4KgeGSOo3Y?key=jqcuw0c7mMfsTTEWWceZSw)

___________________________________________________________________________

## 9. View

 Uma view é como uma tabela virtual. Ela não armazena dados, mas sim uma consulta que é executada quando a view é acessada. A view simplifica consultas complexas e reutilização de consultas.

- As views permitem que você salve consultas SQL complexas com múltiplas junções, subconsultas ou filtros. Assim, em vez de escrever a consulta completa todas as vezes, você pode consultar diretamente a view.
    
- Se a lógica da consulta precisar ser alterada, você altera a view uma vez, e todos que a utilizam verão as mudanças automaticamente.

    

  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfmSd68X3f8fcbY0Z17wvI1f6Gb0ppRMkf8Y_TEXyEpBb1BucAIyC_H29YfH8nj_zBPu27bTKopunMhsA-gXT_tHrRI14D8fYvmPTJkAGnf7YJB9JNQxJEOgotis_sXmgEM803DZXFE3p5PEOwLJBeUImm6?key=jqcuw0c7mMfsTTEWWceZSw)

  

___________________________________________________________________________

## 10. Campo autoincremento

 O tipo SERIAL no PostgreSQL é utilizado para gerar automaticamente valores incrementais em uma coluna, geralmente utilizado para criar chaves primárias. Ele simplifica o processo de criação de IDs sequenciais sem que o desenvolvedor precise inserir esses valores manualmente.

  

Usando serial

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeQGOTTjkymL8zvmbOgwmETGBU_TzY8B9gAATaaJ0Hvbi_TSIx89LYtcl95aJTFpPfuY04qT9vz1vd1kH6N22sUkpqbN7gXFpoOfhuQj9slrVQ_MrmGS-i8FUgYzaVFaCMzgf6dARFQaXNv5ycMr5TRnpU?key=jqcuw0c7mMfsTTEWWceZSw)

  

Como funciona o SERIAL

 Internamente, quando você define uma coluna como SERIAL, o PostgreSQL cria uma sequência associada a essa coluna. A cada inserção, o próximo valor da sequência é atribuído automaticamente à coluna.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeHFaNIjPFdw5klrE1AGPg__MIdQagkH5uup9VGV8a196gyN7xz_nxz4wZBoz8xDUGcR_CmRIj8goGixMmPRPwfOrdQpqCFaypBI39gAtynGSTWPIriIMlv7MVvBK5ars9jy8OaCLjtzPtI56fE8YKeCGgj?key=jqcuw0c7mMfsTTEWWceZSw)

  

Variantes de SERIAL

- SERIAL: Um inteiro de 32 bits
    
- BIGSERIAL: Um inteiro de 64 bits
    
- SMALLSERIAL: Um inteiro de 16 bits
    

  

Cuidados necessários

- Reinicialização de Sequências: Se os registros forem deletados, a sequência continuará a gerar IDs a partir do último valor, deixando "lacunas". Se você quiser ajustar a sequência, é necessário usar o comando ALTER SEQUENCE.
    
- Overflow: O tipo SERIAL é um inteiro de 32 bits que pode gerar até 2,1 bilhões de valores. Se você precisar de mais, deve usar BIGSERIAL.
    
- Inserções Manuais: É possível inserir valores manualmente em colunas SERIAL, o que pode gerar inconsistências.
    
- Remoção da Tabela: Quando uma tabela que usa SERIAL é excluída, a sequência associada não é excluída. Se você remover uma tabela e quiser excluir a sequência associada, isso precisa ser feito manualmente.
    

Usando serial em tabelas já existentes

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcVif04WOyi1WhggLniwn9EHBd6IROFIhW8oYb5UBstXMgnz-GExdSst_QatEqI-dpN7ptvQt2SXYC1bSRnmN3ENX5Lrqa25DGyhCPefgadYRqpZjKeRixB8lv-n5Pfic4oc-j2QqZnypwZkpIJjfwwAMuV?key=jqcuw0c7mMfsTTEWWceZSw)

  

Campo default

 Como mostrado no exemplo anterior é possível definir um valor padrão para cada coluna caso um valor não seja passado.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfOSuXIolkoR8QrdrQKUn8sI5ptImxyTh3h_fSZvvzGao7RtLzNxY1BuQlnydn9myf42GJq7cgC6JNhFgnymBPbUarkDOeTpPoOpnMsvPrwHf4mkVi_M-pOIsMfLpx2WTmqX0N-4nJckW3eR21gRPl4_XQK?key=jqcuw0c7mMfsTTEWWceZSw)

  

___________________________________________________________________________

## 11. Índices

 Índices são estruturas que aceleram consultas, facilitando a busca em tabelas. Os índices são recomendados em tabelas com muitos valores que precisam ser buscados com frequência. Sem a utilização de índices, quando é feita uma busca, é percorrido por todos os dados da sua tabela e isso é bastante ineficiente.

  

- Duas principais estruturas de dados são utilizadas para melhorar o desempenho de busca: árvores b e tabelas hash.
    
- Índices ocupam mais espaço em disco e gera um custo de inserção maior visto que os índices precisam ser atualizados.
    

  

Definindo um índice para o atributo nome de cliente.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcr4OEKf0WYfGbFltmB1AqWFV_Vr64jXR4R33-r28S3O9sQhwHRRpFoftn8zNrUIFbkrQZ12QqvTu18loxc3V8A3Yn6lsOe5OLxqVurBhW07AjZD2WO5FUt1D-e2B4HLDS1H5GrpXoYJsnj_E_v7EIFweo?key=jqcuw0c7mMfsTTEWWceZSw)

  
  
  
  
  
  
  
  
  
  
