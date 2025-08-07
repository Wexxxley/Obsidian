
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
