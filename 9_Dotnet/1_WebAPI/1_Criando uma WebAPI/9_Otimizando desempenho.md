
---
**AsNoTracking**: Método usado para melhorar o desempenho ao realizar consultas que não precisam ser rastreadas pelo contexto. Quando você utiliza AsNoTracking, o EF Core não mantém o estado das entidades carregadas em memória.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeSHeP6v3Yq1q1GWIxS7h5gfYQ-M-7wveeYcTb-3mhjt0-XosWTLE59X190wggyDoBBe6YIg0CJsPfoDM6-WZR5NMxucToev9FgXBZX-Ph5ImLueDo0QG9EFTZOxZOPH2SayLjAQm_xLf2hF5uXeTQAplXD?key=SZHaDLu24DLXyFgiFaRNLA)

Take: Vamos supor que você tenha 1500 produtos cadastrados, você nunca pode retornar todas as suas entidades de uma só vez. Por isso é preciso limitar a quantidade de dados retornados. E, para isso, existe o Take.
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf1UkHRpWoy-uH0c-pXmIgX2yLK3BDa5T4dQ8Oa58-vI7XVIlEVnxOoI7lEUthIbZdFH89DtGObHyh2d2D9hr7hF7eAKaa5ZIhnp__Qx-95ozBh4TeEp5JTGsynjLS8F4V-olxlx3t29SQ-A092AQn8EZM?key=SZHaDLu24DLXyFgiFaRNLA)
