
#Concluded 

---
### **1. Carregando entidades dentro de outras.**
Vamos criar um outro endpoint que retorna uma lista de categorias e, em cada categoria, o campo Products contém todos os produtos de uma categoria.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXer-X_Q59aTO1z3PAOokki_cZ7T6yM4d-2FIos15ilpeIyg_w3XUQ4K3BQoqCNUZOpeHkAG7dxyzzlajz_2JkV7xc63RA-uJU2lrzMYR53sUw5kZF3piHR5x_gd7fvx4lmkAX_wuEcD4zGz4uHZLQjm52_I?key=SZHaDLu24DLXyFgiFaRNLA)

**Include**: O método Include é utilizado para carregar entidades relacionadas junto com a entidade principal em uma consulta. O Include permite que você especifique que entidades relacionadas também devem ser carregadas.

---
### **2. Ciclos de referencia**
As entidades frequentemente têm relacionamentos uns com os outros como, por exemplo, uma entidade Category tem uma coleção de Products e cada Product possui uma referência de volta para a Category. Isso cria um ciclo de referência

Quando o **JsonSerializer** tenta serializar um objeto com ciclo, por isso, ele dá um erro avisando sobre esse possível ciclo. 

No nosso caso, queremos que somente Category retorne seus produtos (Um produto não deve retornar sua categoria). Então é necessário desabilitar essa opção no Program.cs.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcOmD0N-3tasjqK-GmMsJM3jEmGxu5nxgUPdSyrfWdw5cixY-kT82AUBdQNFdQmJR5QJOIfDZ8fVlBaSxa6DHe8kmngbrGrneGFfM-nDALuz9uhA30fhyXi48aTHYOUAHvnTAgEhgAFDabEuiS_3nRE_Qcc?key=SZHaDLu24DLXyFgiFaRNLA)

**ReferenceHandler.IgnoreCycles:** Essa opção diz ao JsonSerializer para ignorar possíveis ciclos de referência.

Ao executar getCategoriesWithProducts temos algo parecido com isto:

![400](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeLuYQZy2G8Sv5ziwCFHRrmQ1x9k2s98D0SmhTZ5UCa1x1dwOaGgiq0pqKdbq1wiZVHoi_Kym4aNIjayMiJaNwKj1Ji4zFJYLTSf2-PlhRfL0wpU3xk3qHpk15jCf8hV3_xBjeQeFdTHVKNwkJAsbYMQISV?key=SZHaDLu24DLXyFgiFaRNLA)

---
### **3. JsonIgnore**
Ao serializar objetos c#, por padrão, todos os atributos públicos são serializados. No exemplo abaixo, é mostrado o body de um post que precisa receber além do id de category o objeto em si. Isso não deve ocorrer, visto que category é apenas um objeto de navegação.

![350](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfnTVfo2wrcVgdtrSOfSMUlH_ebuaxEWFE5cDalqTsAOxHsy1mTLsZmFt4g38lIec4eAg4JClrLDQq2XJUJ642o_3Mc2DKy6RRF6eNkFTMFSk_kZAnALp6pwgI10VMa4KGt5RIicZwAGKPMoxS3PVxiOKzd?key=SZHaDLu24DLXyFgiFaRNLA)

Para resolver isso basta adicionar o atributo JsonIgnore na classe Products.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdptpr07DiraMhJs4_YVJWqoV3D1n01ivO8jWnGAg0gnqy-JtEyUhFq6q-iglV45jrQxNeKFv3Wut4BnRYeBdDtEP7LVJ6FGjpD5W54AZFzHJnZzjMlcVG_Gads4TgJ8lAFwkFR0z8e_gcfrN8CdKjtVpZW?key=SZHaDLu24DLXyFgiFaRNLA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf1eYrQgGVmGFsOJ6GDWIufnTem6hlID3c_H7wLAC3JN5n_iiJz3tu_wFGyH5ex2l2vNEKqjpwa5J0t4-xGsQHSMj4PIEik06Xazi-zi_2BPfun_EgF4R2YXia5l24xb6gkOhsRwDdI3pPTD5NFEIz9bArG?key=SZHaDLu24DLXyFgiFaRNLA)

