


---
Caso base, um unico servidor, um unico db

quando o serviço chegar em muitos users naturalmente ele vai ficar lento. muitos podem pensar em criar um cache (redis), e faz sentido

se a cache n der conta:
1. Faz sentido criar replicas de leitura? (consistencia ou disponibilidade)(leitrua é mais comum, mas existe sistemas onde a escrita é mais comum?)
2. Indices no db ajudaria? faz sentido somente quando um campo é muito buscado (quais os difernetes tipos e quais os casos de uso) e os pontos negativos(escrita mais lenta, armazenamento)?
3. normalização denormalização. quando fazer e quais vantagens e desvantagens
4. ou sharding faz mais sentido? traz bem mais complexidade, queries complexas
5. connecction polling (já é o padrão?)
6. Otimização de queries
7. materialized view (pontos negativos, quando faz sentido?)
8.  Batching e pagination

- Estretegias para priorizar leituras e escritas (escritas sao mais custosas por conta dos locks?)
- Uncomitted vs committed reads
- Locks pessimistas e otimistas