


___
# **1. Position** 

A propriedade position é usada para especificar o método de posicionamento de um elemento em relação ao seu contêiner.

Os elementos são posicionados com as propriedades top, bottom, left e right. Mas, essas propriedades so irão funcionar se a propriedade **position** for definida antes.
1. **static (Padrão):** O elemento segue o fluxo da página. As propriedades não surtem efeito.
2. **relative:** O elemento permanece no fluxo normal da página.  Mas pode ser deslocado em relação à sua posição original, porém isso pode gerar conflito com outros elementos.
![Pasted image 20250513095359](../../../attachments/Pasted%20image%2020250513095359.png)
![300](../../../attachments/Pasted%20image%2020250513095413.png)Os elementos dentro de um container relativo ficam posicionados com base nele. Muito útil se usado junto com absolute.

3. **absolute:** Um elemento com ``position: absolute`` é posicionado de forma fíxa ao seu container pai (que tem que ser relative). 

**Relative + absolute:** Podemos ter um contêiner externo com relative e os containers internos com absolute. Dessa forma temos controle dos containers internos, e o externo vai seguir o fluxo normal do html.
![300](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeO_7EB6F12MjRRvDXRYH2fxcf1-bhqXSjaQrnf0AvGIYmqMByVvYw55bTy0L7neGDMOeiCwIObETmnxjnXXVkgMIPdLVeFDWqIsoOn8e3z9FuMtrT2g9a0ducxGmNA2Vc05qQXig?key=VYJVAqKhTdZyHt8enJbiwA)![300](https://lh7-rt.googleusercontent.com/docsz/AD_4nXe8fNxUNvSkbqhBY-E8srpAI28GZpNuugPlMCOX00o5fiz_kTkoZEVauL8y1AaA4xGQFXOgqXqVORdiglu-A90rBTuh0xpFxmPuVTlYFv6nO-8BmnXyZFi_ZSULZgCbPeMihpdL?key=VYJVAqKhTdZyHt8enJbiwA)![300](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeC-SUontTWMDLeIqf0k4ZDaHBb04b-UR2hVJCcw6fbrAmrhq_a4cOyTIujT3UbUCeHaSBNcHRR1bzTdeZpuX_yzyE8NWCg_dcvGpt2WJRPVQCv0hrRI6XUvBrjZ7aWmtUeCQWx?key=VYJVAqKhTdZyHt8enJbiwA)![300](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeK2Jj278Q_zUxHZ_YxeQ7VPgJlfj9nDt5d_cYoa2085ujVjutcNbBfh98OqhjSybmT8Sb7sas8_8syDZfUWQMsz72RZV3yF0eHK5ngwZh9AazKpPJc_nYMaaSYXRboKvAm918x?key=VYJVAqKhTdZyHt8enJbiwA)
4. **fixed:** O elemento é removido do fluxo normal da página. É posicionado em relação à janela do navegador (viewport). Permanece fixo na posição mesmo durante o scroll.

5. **sticky:** Combina características de relative e fixed. O elemento é tratado como relativo até o scroll passar por ele, ai se torna fixo na tela.  


----
# 2. z-index
Controla o eixo Z (profundidade), determinando qual elemento deve aparecer à frente e qual deve permanecer ao fundo quando ocorre uma sobreposição visual de caixas (boxes) no layout.
![500](../../../attachments/Pasted%20image%2020260817134527.png)![300](../../../attachments/Pasted%20image%2020260817134504.png)![](../../../attachments/Pasted%20image%2020260817134454.png)