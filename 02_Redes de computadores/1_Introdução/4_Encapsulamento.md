
#Concluded 

---

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfXDxDj8GdgLtFqpgESr7V211Ij_eflTjcu7TGmJPmWbHVgKl3nyTo7oGCvHfGQmf9RAsBDhGbJRqwAuKYkPsA4qHkgvenmcHmo6KOLdgcm8wHsx0WU_--fsg_nmyjROetFATgu?key=HrOhHC0_-ked6RNCpQ0o3PZn)

À medida que os dados descem pelas camadas, cada camada adiciona um cabeçalho ao dado original (a mensagem). Isso é chamado de **encapsulamento**.

1. **Camada de Aplicação:**
    - **Protocolos:** HTTP, HTTPS, SMTP, FTP, DNS.
    - A Mensagem original (M).
        
2. **Camada de Transporte:**
    - **Protocolos:** TCP ou UDP.
    - **Encapsulamento:** A Camada de Transporte adiciona o cabeçalho de transporte (Ht). A unidade resultante é chamada de **segmento/datagrama**.
        
3. **Camada de Rede:**
    - **Protocolos:** IP (Pv4 ou IPv6)
    - **Encapsulamento:** A Camada de Rede pega o Segmento/Datagrama e adiciona o cabeçalho de rede. A unidade resultante é chamada de **Pacote**.
        
4. **Camada de Enlace:**
    - **Protocolos:** Ethernet (para cabos), Wi-Fi (para redes sem fio).
    - **Encapsulamento:** A Camada de Enlace pega o pacote e adiciona o cabeçalho de enlace (Hl). A unidade resultante é chamada de **Quadro**.
        
5. **Camada Física:**
    - **Protocolos:** (Não há protocolos de software aqui, apenas padrões de hardware).
    - **Encapsulamento:** O Quadro é convertido em uma sequência de bits.
