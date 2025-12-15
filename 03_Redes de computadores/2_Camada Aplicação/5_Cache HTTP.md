

---
O cache HTTP armazena uma resposta associada a uma solicitação e reutiliza a resposta armazenada para solicitações subsequentes. O exemplo mais típico é quando o próprio navegador armazena um cache para solicitações do navegador.

Além disso, quando uma resposta é reutilizável, o servidor de origem não precisa processar a solicitação, portanto, não precisa analisar e rotear a solicitação, consultar o banco de dados. Isso reduz a carga no servidor.

Existem dois tipos principais de caches: **caches privados** e **caches compartilhados**.

---
### **1. Caches privados**

Um cache privado é um cache vinculado a um cliente específico, normalmente um cache de navegador. Como a resposta armazenada não é compartilhada com outros clientes, um cache privado pode armazenar uma resposta personalizada para esse usuário.

Se uma resposta contém conteúdo personalizado e você deseja armazenar a resposta apenas no cache privado, você deve especificar uma diretiva `private`.

```http
Cache-Control: private
```

Os conteúdos personalizados são geralmente controlados por cookies, mas a presença de um cookie nem sempre indica que é privado e, portanto, um cookie por si só não torna a resposta privada.

---
### **2. Cache compartilhado**

O cache compartilhado está localizado entre o cliente e o servidor e pode armazenar respostas que podem ser compartilhadas entre os usuários. E os caches compartilhados podem ser subdivididos em **caches de proxy** e **caches gerenciados**.
#### **2.1 Caches de proxy**
Além da função de controle de acesso, alguns proxies implementam cache para reduzir o tráfego fora da rede. Isso geralmente não é gerenciado pelo desenvolvedor do serviço, portanto, deve ser controlado por cabeçalhos HTTP apropriados e assim por diante. No entanto, no passado, implementações de cache de proxy desatualizadas — como implementações que não entendem adequadamente o padrão HTTP Caching — geralmente causavam problemas para os desenvolvedores.

**Kitchen-sink headers** como os seguintes são usados para tentar contornar implementações de "cache de proxy antigo e não atualizado" que não entendem as diretivas atuais de especificação de cache HTTP, como `no-store`.

httpCopy

```
Cache-Control: no-store, no-cache, max-age=0, must-revalidate, proxy-revalidate
```

No entanto, nos últimos anos, à medida que o HTTPS se tornou mais comum e a comunicação cliente/servidor tornou-se criptografada, os caches de proxy no caminho só podem encapsular uma resposta e não podem se comportar como um cache, em muitos casos. Portanto, nesse cenário, não há necessidade de se preocupar com implementações de cache de proxy desatualizadas que nem conseguem ver a resposta.

Por outro lado, se um proxy de ponte [TLS](https://developer.mozilla.org/pt-BR/docs/Glossary/TLS) descriptografa todas as comunicações de maneira intermediária instalando um certificado de uma [CA (entidade certificadora)](https://developer.mozilla.org/en-US/docs/Glossary/Certificate_authority) gerenciada pela organização no PC e executa o controle de acesso, etc. — é possível ver o conteúdo da resposta e armazená-la em cache. No entanto, como [CT (transparência do certificado)](https://developer.mozilla.org/en-US/docs/Web/Security/Defenses/Certificate_Transparency) se tornou comum nos últimos anos e alguns navegadores permitem apenas certificados emitidos com um SCT (carimbo de data e hora do certificado assinado), esse método exige a aplicação de uma política empresarial. Em um ambiente tão controlado, não há necessidade de se preocupar com o cache do proxy estar "desatualizado e não atualizado".

#### Caches gerenciados

Os caches gerenciados são implantados explicitamente por desenvolvedores de serviços para descarregar o servidor de origem e fornecer conteúdo com eficiência. Os exemplos incluem proxies reversos, CDNs e service workers em combinação com a API de cache.

As características dos caches gerenciados variam dependendo do produto implementado. Na maioria dos casos, você pode controlar o comportamento do cache através do cabeçalho `Cache-Control` e seus próprios arquivos de configuração ou painéis.

Por exemplo, a especificação HTTP Caching essencialmente não define uma maneira de excluir explicitamente um cache — mas com um cache gerenciado, a resposta armazenada pode ser excluída a qualquer momento por meio de operações de painel, chamadas de API, reinicializações e assim por diante. Isso permite uma estratégia de cache mais proativa.

Também é possível ignorar os protocolos de especificação de cache HTTP padrão em favor da manipulação explícita. Por exemplo, o seguinte pode ser especificado para desativar um cache privado ou cache proxy, ao usar sua própria estratégia para armazenar em cache apenas em um cache gerenciado.

httpCopy

```
Cache-Control: no-store
```

Por exemplo, o Varnish Cache usa VCL (Varnish Configuration Language, um tipo de lógica [DSL](https://developer.mozilla.org/en-US/docs/Glossary/DSL/Domain_specific_language)) para lidar com o armazenamento em cache, enquanto os service workers em combinação com a Cache API permitem que você crie essa lógica em JavaScript.

Isso significa que se um cache gerenciado ignorar intencionalmente uma diretiva `no-store`, não há necessidade de percebê-lo como "não compatível" com o padrão. O que você deve fazer é evitar o uso de cabeçalhos de pia de cozinha, mas leia atentamente a documentação de qualquer mecanismo de cache gerenciado que estiver usando e verifique se está controlando o cache adequadamente da maneira fornecida pelo mecanismo escolhido para usar.

Observe que alguns CDNs fornecem seus próprios cabeçalhos que são eficazes apenas para esse CDN (por exemplo, `Surrogate-Control`). Atualmente, o trabalho está em andamento para definir um cabeçalho [`CDN-Cache-Control`](https://httpwg.org/specs/rfc9213.html) para padronizá-los.