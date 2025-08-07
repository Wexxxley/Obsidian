
---
### **1. Controladores**
Controller é a classe responsável por lidar com requisições HTTP de determinada entidade. Essa classe atua como um intermediário entre as requisições feitas pelo cliente e a lógica de negócio que processa essas requisições. 

Estrutura básica de uma controller
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeIgrx--IlvMgIZ_DlyPh9yqBGoGwuHwWLJfXfr_TE0f-BVhcPPBqKtjD5xfhufZ9h7G6A3_HfGojW7x7Dzw8XYYbnostK4c9tXfyNyZ350SyELsn7TsQoNIAR-SJoHk9FF_25v_hoiWwzat27lah7qI5JY?key=SZHaDLu24DLXyFgiFaRNLA)

É preciso adicionar um serviço e um middleware ao seu Program.cs.
![600](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf3TYygkBGry2n8UBuqxGUR8NozjCT378gZ7LUdhjtmrzbOcWxIt1HbE_fzSNQkFixstLRijgspQBmRL2kZR48lMjpl-kHqCvdRBO0JC1yJ3TZXxJTkQMZ9tTfzSZKIomLbc3sPloYPJR9-45Ch7gPus-c?key=SZHaDLu24DLXyFgiFaRNLA)

---
### **2. Retornando todos os registros**
Esse método está dentro do controlador
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfSPwoGH6tHCqdDT_1YXr-iMeytjCiRYtxJCXVpwmoJr6XXjajzA4tyrBBdM1_6pkiz27IC_VYek79_mEH5qlS9la9Z2V27TXrbIbrWt9J6h2D2OLDHht4M51igwnOZOlDgdh4O_fEgqJPQhTVqZVfDhtGO?key=SZHaDLu24DLXyFgiFaRNLA)
1. **HttpGet**: Indica que o método responderá a requisições HTTP GET.
2. ``ActionResult<IEnumerable<Product>>``: O método retorna um ActionResult que contém um IEnumerable de objetos do tipo Product. 
3. **ToList():** Converte o`` DbSet<Product>`` em uma lista que implementa a interface IEnumerable.

---
### **3. Retornando um registro**
O processo para retornar um registro é muito parecido com o processo de retornar todos, a diferença é que o atributo HttpGet vai indicar que vai receber um parâmetro Id do tipo inteiro. ![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeGT-7ERZfpgPg7oQeKHx1IS2PuejqFahvN8-xvD6xXOPMVrpki-7Z9UM9e9JlotF_hSrDs4u1Hn5sUoDCGMvPio5wwZSuQUEFU74KJZ7bvwQBkpHUPQPSwbRArhuL9FHZggtwN1ldlRxGb0qTvRk-D3IfD?key=SZHaDLu24DLXyFgiFaRNLA)
O atributo também está renomeando o método.

---
### **4. Criando um registro**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeKwDiQ65_wO2jxGHmVK5ZQHOtEQAGfAKxPYM_ymrnE0tc54pa3sekCfHNzKYf0GNqq84FRHO7_OWg9-AfAKvLrGVDkvKf0V7Nbm7NGc93UarmV63TrF4kkVuY_vFc0NcuzSHGKxsfjZsuwBhhJH27sL0E?key=SZHaDLu24DLXyFgiFaRNLA)
1. **HttpPost:** Esse atributo indica que o método responderá a requisições POST.
2. **SaveChanges**:  Com o Add é inserido o produto somente no modelo, o SaveChanges é que salva no banco de dados.
3. **CreateAtRouteResult**:  Quando você cria um novo recurso em uma API, é uma boa prática retornar o status HTTP 201 junto com a URL para acessar o recurso recém-criadi.

---
### **5. Atualizando um registro**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe1vJAZ1GPqXdloKy3UVpsyNE3uDn9yqaTubU_slLV9fQsFcKrIATbt6ztcEl2wU1NGX05SgKUxKU2tJ_LOLZrZo1hjveg3bQBT3CXi-f2gkYWSy1A0qdlYhgE2sE5OhpIjl3ModH8fMetDRlSHuZ35VZQm?key=SZHaDLu24DLXyFgiFaRNLA) 
1. **HttpPut("{id:int}"):** Este atributo indica que o método responde a requisições HTTP PUT.
2. **Entry(product).State = EntityState.Modified**: Esta linha informa ao Entity Framework Core que a entidade product foi modificada.

---
### **6. Deletando um registro**
![600](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcp2FFmQPZ__EdjjzijmbS9TfiJcFn4eYG2Xc_vqAUyKbsjbR4zlmx66i0TRsnPh3psUW9ADimkEn08ftxHCgmkYz201U4Md2e3jY3YGZHPiTkZDJYWg4y28qaDBAHlin4yqTaRS_wNZlLW6ceGcfzkGrI?key=SZHaDLu24DLXyFgiFaRNLA)
Todos os endpoints para Products foram implementados, agora faltam os endpoints para Category.


7. 
 Vamos criar um outro endpoint que retorna uma lista de categorias e, em cada categoria, o campo Products contém todos os produtos de uma categoria.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXer-X_Q59aTO1z3PAOokki_cZ7T6yM4d-2FIos15ilpeIyg_w3XUQ4K3BQoqCNUZOpeHkAG7dxyzzlajz_2JkV7xc63RA-uJU2lrzMYR53sUw5kZF3piHR5x_gd7fvx4lmkAX_wuEcD4zGz4uHZLQjm52_I?key=SZHaDLu24DLXyFgiFaRNLA)

Include: O método Include é utilizado para carregar entidades relacionadas junto com a entidade principal em uma consulta. O Include permite que você especifique que entidades relacionadas também devem ser carregadas.

  

 Em uma aplicação que utiliza o Entity Framework Core, as entidades frequentemente têm relacionamentos uns com os outros como, por exemplo, uma entidade Category tem uma coleção de Products e cada Product possui uma referência de volta para a Category. Isso cria um ciclo de referência:

- Category -> Products -> Category
    

  

 Quando o JsonSerializer tenta serializar um objeto com ciclo de referência, ele pode entrar em um loop, porque cada referência continua levando a outra e, por isso, ele dá um erro avisando sobre esse possível ciclo. Mas para o nosso caso, queremos que somente Category retorne seus produtos (Um produto não deve retornar sua categoria). Então é necessário desabilitar essa opção do JsonSerializer no Program.cs.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcOmD0N-3tasjqK-GmMsJM3jEmGxu5nxgUPdSyrfWdw5cixY-kT82AUBdQNFdQmJR5QJOIfDZ8fVlBaSxa6DHe8kmngbrGrneGFfM-nDALuz9uhA30fhyXi48aTHYOUAHvnTAgEhgAFDabEuiS_3nRE_Qcc?key=SZHaDLu24DLXyFgiFaRNLA)

ReferenceHandler.IgnoreCycles: Essa opção diz ao JsonSerializer para ignorar possíveis ciclos de referência.

Ao executar getCategoriesWithProducts temos algo parecido com isto:

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeLuYQZy2G8Sv5ziwCFHRrmQ1x9k2s98D0SmhTZ5UCa1x1dwOaGgiq0pqKdbq1wiZVHoi_Kym4aNIjayMiJaNwKj1Ji4zFJYLTSf2-PlhRfL0wpU3xk3qHpk15jCf8hV3_xBjeQeFdTHVKNwkJAsbYMQISV?key=SZHaDLu24DLXyFgiFaRNLA)

#### 3.3.8 JsonIgnore![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfnTVfo2wrcVgdtrSOfSMUlH_ebuaxEWFE5cDalqTsAOxHsy1mTLsZmFt4g38lIec4eAg4JClrLDQq2XJUJ642o_3Mc2DKy6RRF6eNkFTMFSk_kZAnALp6pwgI10VMa4KGt5RIicZwAGKPMoxS3PVxiOKzd?key=SZHaDLu24DLXyFgiFaRNLA)

 Ao serializar objetos c#, por padrão, todos os atributos públicos são serializados. No exemplo abaixo, é mostrado o body de um post que precisa receber além do id de category o objeto em si. Isso não deve ocorrer, visto que category é apenas um objeto de navegação.

  

Para resolver isso basta adicionar o atributo JsonIgnore na classe Products.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdptpr07DiraMhJs4_YVJWqoV3D1n01ivO8jWnGAg0gnqy-JtEyUhFq6q-iglV45jrQxNeKFv3Wut4BnRYeBdDtEP7LVJ6FGjpD5W54AZFzHJnZzjMlcVG_Gads4TgJ8lAFwkFR0z8e_gcfrN8CdKjtVpZW?key=SZHaDLu24DLXyFgiFaRNLA)

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf1eYrQgGVmGFsOJ6GDWIufnTem6hlID3c_H7wLAC3JN5n_iiJz3tu_wFGyH5ex2l2vNEKqjpwa5J0t4-xGsQHSMj4PIEik06Xazi-zi_2BPfun_EgF4R2YXia5l24xb6gkOhsRwDdI3pPTD5NFEIz9bArG?key=SZHaDLu24DLXyFgiFaRNLA)

#### 3.3.9 Otimizando desempenho

AsNoTracking: Método usado para melhorar o desempenho ao realizar consultas que não precisam ser rastreadas pelo contexto de dados. Quando você utiliza AsNoTracking, o EF Core não mantém o estado das entidades carregadas em memória, o que resulta em melhorias na velocidade de consulta.

 O EF Core rastreia todas as entidades que são carregadas no contexto. Isso significa que ele armazena informações sobre o estado das entidades para permitir operações de atualização. Essa funcionalidade é útil quando você pretende modificar os dados.

Quando Usar AsNoTracking?

 Use AsNoTracking quando você estiver realizando consultas apenas para leitura que não precisam modificar os dados.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeSHeP6v3Yq1q1GWIxS7h5gfYQ-M-7wveeYcTb-3mhjt0-XosWTLE59X190wggyDoBBe6YIg0CJsPfoDM6-WZR5NMxucToev9FgXBZX-Ph5ImLueDo0QG9EFTZOxZOPH2SayLjAQm_xLf2hF5uXeTQAplXD?key=SZHaDLu24DLXyFgiFaRNLA)

Take: Vamos supor que você tenha 1500 produtos cadastrados, você nunca pode retornar todas as suas entidades de uma só vez. Por isso é preciso limitar a quantidade de dados retornados. E, para isso, existe o Take.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf1UkHRpWoy-uH0c-pXmIgX2yLK3BDa5T4dQ8Oa58-vI7XVIlEVnxOoI7lEUthIbZdFH89DtGObHyh2d2D9hr7hF7eAKaa5ZIhnp__Qx-95ozBh4TeEp5JTGsynjLS8F4V-olxlx3t29SQ-A092AQn8EZM?key=SZHaDLu24DLXyFgiFaRNLA)

**