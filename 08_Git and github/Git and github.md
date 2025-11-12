


---
### **1. Fluxo básico**

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf7_55WBfYQZKkMPobGSjeXrfoes34gdmd8LrM2sJvX8en_zWSEIRbskh7J_majyrp-QjNq3xghsnUkhCg8nFTq6ICcYRZMTqghF9FBaK65IZV5MjXlmePTXSL67tJvj5b6quSrEw?key=yiMe1b2VwU1jpN7Jf4vtog)

**Diretório de Trabalho:** É onde você realmente edita os arquivos do projeto.
- `add`: Move os arquivos modificados do diretório para a área de staging.  

**Staging**: É onde você prepara os arquivos que deseja enviar para o repositório.
- `commit`: Grava os arquivos preparados no repositório local.

**Repositório Local:** Contém o histórico de commits da sua máquina.
- `push`: Envia os commits para o repositório remoto.
- `git fetch`: Baixa o histórico recente do repositório remoto sem aplicar ao seu código.
- `git merge`: Mescla as mudanças que vieram do fetch ao seu repositório local.
- `git pull`: Faz fetch + merge de uma vez: traz e aplica atualizações do rep remoto.
- `checkout`: Alterna entre branches diferentes do projeto no repositório local. 

**Repositório Remoto:** É onde o código fica hospedado online.
- `git clone`: Copia um repositório remoto para a sua máquina, criando um repositório local com diretório de trabalho.  

**Git status**: Mostra os estados dos arquivos.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXerJgctqNG1vAFPYLkfjohm3BpEFZrhOIpovTRphPEoDI0Uy4czesw3kPA95IZYMeIrspyhkQT514YL1CZSkZgY-JUSoscwDYes8ybMmuCcFvqDOnhQNBYZi4fxv_ydSDABdEUxXibIC-foZ6DkWHj8LVWS?key=yiMe1b2VwU1jpN7Jf4vtog)
### 1.3.1 Stage
**Colocando em stage**: “`git add NameFile`” ou “`git add .`” para adicionar tudo.
**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdi_Q2COuyKA-NWGe5mboOlmWhxrUlJxd1CD9pTP1jXyjyxF3jiU9Urm225OREUbNmEeFUh1WSoI_hx4qDLmS7fK484Rt39OJzUDnpiOb3gR4HaLDdC9VKDUbKB5Gsj3rieQ2p1goZXtXgqE5RhvOsUmTWR?key=yiMe1b2VwU1jpN7Jf4vtog)
Para retirar do Staging: “rm –cached file".
### 1.3.2 Commit

Funciona como um marco histórico no seu projeto. É interessante realizar depois de uma mudança relevante.

****![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXf1L32Yoh4EWGmXZ5gRLj5A-HFqbSd8E5mgwXnu1blU2mQZDIP1ndmp1z23-YjVY4EUYLIKsyE1NFb6azCdVgDrpao3s3er602SQ4CQFwCgTDIxKvBL1RsctyLO2Fakrba_rdks-T7L8h8ee-dTjx2w-xg?key=yiMe1b2VwU1jpN7Jf4vtog)

Para você ver o histórico de commits basta usar o comando “`git log`”.

**Desfazendo alterações**

  

**<Desfazendo .git**

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcpM4IDA-6p7rSn2dt6CjT7TR_NDZJM4FJM9s33QTcTBE3B3c3rsFwq_M1Z9snKl5cnyDBOaPIOYSLf9rcxa8lEwdQCFJnoS0c3N1iYML205DbT9g2rWYCZUXDIpYi01vy5pojMjeyD1gFIn_6cHxttdcQ?key=yiMe1b2VwU1jpN7Jf4vtog)**

  

**<Desfazendo alteração de um arquivo**

 **Usa-se o git restore file.**

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfzFc86pAUA_cmIXPb3L3BZNYDBKjeBaC2gGu5EXXAu7lWMSP5DUxILu2csdN5wg900gzZy5HluHTT1xTHosCS0qMf4D0-9FnesZlV1tdLhduVYs8GEDir5PP4F36m7tpU3AqcUybvLNEAGXIHIBmoOzmpi?key=yiMe1b2VwU1jpN7Jf4vtog)**

  

**<Renomeando o último commit**

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfqnS5ieTRhbIyiOr2cZqXma6a37gWv_8GcK2Si4DErrllIlF3YPgwnJZ3rHyc_ah0g63gMyR-NRBKcWdCz1oDz0EhME8F0votizKolCFn033oJgHM02izlsnEOQBy4shMI6rDNvLs9VLVUt0Fctg6niiKx?key=yiMe1b2VwU1jpN7Jf4vtog)**

  

**<Desfazendo commit**

  

**1. Git reset –soft: Desfaz commits até o ponto especificado, mas mantém as alterações dos arquivos dos commits desfeitos na área de preparação (staging area).**

**- As alterações desfeitas ainda estão prontas para serem commitadas.**

**- Útil quando você deseja desfazer commits e reutilizar as alterações em novos commits sem ter que refazê-las.**

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe1LHyRzynWt-1aecZrRY1ND5feTQhK7Ru0ahVk5qo9TrTYM9S9VazLxrKPQHNOJ0aeYjL_0UUbcm8k-noqRCQX51wS1UPBAcyP_yOpS3ax3XLRjhBoZXR042Gt3WgpQhSaTMmNTZjIYBNuoK2LlHVzMbso?key=yiMe1b2VwU1jpN7Jf4vtog)**

  
  

**2. Git reset mixed: Ele desfaz commits até o ponto especificado e remove as alterações dos arquivos dos commits desfeitos da área de preparação.**

**- Isso significa que as alterações desfeitas permanecem nos arquivos modificados, mas não estão na área de preparação para um novo commit.**

**- Útil quando você deseja desfazer commits e reavaliar quais alterações devem ser incluídas no próximo commit.**

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeMjlenbMuqJaSJGxQpL3gKJTb-Uk5H1QBoSxZkrqChTBKBurgkMWdwko8ScNv57UFBZ8vtA5JTB5JnHxaOYcA8ikyl9cdszu_bM3bNBVU6oAbVvTMYN2uGR0eXDAXmPESOlmEBDfpNxZ5283KNjGonQoI?key=yiMe1b2VwU1jpN7Jf4vtog)**

  

**3. Git reset hard: Desfaz commits até o ponto especificado e descarta todas as alterações dos arquivos dos commits desfeitos.**

**- Todas as alterações desfeitas são perdidas e não podem ser recuperadas.**

**- Tenha cuidado, pois ele pode causar perda irreversível de alterações não confirmadas.**

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeLgpOqVvp23Pgld9-_hRHAmHgR105nNQht4XXT3DG68NR3GyR-cAp4G13-FiWRbeDvQjFp2h9Pmowcylzpul_U_8CFfYNhw4khXDYBMEjm2rhrgHI9MaM51SXEqw4llwVHd8iCnwKBxWy1w9p6hStMwlM?key=yiMe1b2VwU1jpN7Jf4vtog)**

  

**<Retirando arquivos do Staging**

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe8A0fXX5B22rM02HQ96SDukA9FSLxKl55l6WGwJtGdrj_38RC3d_827NTeQeyilcCtTMSR4ZQkO0ia--ZRaLsEZa1rxs3n01zFF_WbWxUWyIrAgfxZx3kiFs1XUI-8YaScwIA8QyEgjY5mPqjoNfnzqqF3?key=yiMe1b2VwU1jpN7Jf4vtog)**

  
  

**<Git reflog**

**Mostra todo o histórico de alterações do projeto**

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfnZTUBTss2LlWkWu-zB2CxdI_DWO80nGuc9hQ6SPWG5X8NrEBWFjOLEV8aLpMRLlpQHtpU946qo7O0_4nu5IxEZksPq37-nJKc6rg1JeKFR6_S0CxC-OX4jMrCRMDXTO-uiszB-SzQJwM9L3esUjdxjvKr?key=yiMe1b2VwU1jpN7Jf4vtog)**

**___________________________________________________________________________**

**<Enviando e baixando alterações**

  

**1. Enviando alterações para o repositório remoto**

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcTlUqqeDiGSsj-x2n5FmGb2JKzwVIepRwmB_ZzP8yrpF39s_on0U8-pS7vvQLdthlfo9cINeGnxJEWgWV66PkQDBkXXVNxNHIXBTiSTXoSQdsCx2ky3lDAOzh4yosxUXCbw9q4D9f1iGeqXHi2dAxECZI?key=yiMe1b2VwU1jpN7Jf4vtog)**

  

**2. Baixando alterações do repositório remoto**

**![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXctgvwfr9Mu1iWR_u2FfqSTQbtIFWCQ-o9PNcdZQNcA5gtQO22o3P7lL2Tzrp3z4xxrVMO4KRLrvNlvaK3c-Sga0E62xkoNxnzidzZoig4gDkqi9DOS2WwoSwDygNhjDuHvXxN6insQkRHSxo48X7X_l_4?key=yiMe1b2VwU1jpN7Jf4vtog)**

**___________________________________________________________________________**

  
  
  
  
  
  
  
  
  
