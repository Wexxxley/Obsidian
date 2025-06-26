
---

Um dos problemas ao lidarmos com uma aplicação web é a necessidade de estarmos sempre disponíveis para responder a requisições enviadas pelos clientes. Quando recebemos uma requisição, normalmente precisamos processá-la: validar, conectar ao banco de dados, realizar algumas operações e, finalmente, retornar o recurso solicitado.

Em um cenário síncrono, enquanto processamos uma requisição, não conseguimos processar outra até que a primeira seja concluída. Esse fluxo de execução é chamado de blobueante, pois a aplicação fica "parada", aguardando a resposta de sistemas externos. Esse tempo de espera é conhecido como **bloqueio por I/O (Input/Output)** 