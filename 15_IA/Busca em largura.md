
![](attachments/Pasted%20image%2020251031091210.png)


```
 BUSCA(problema){
	 iniciar borda com estado inicial
	 iniciar explorados com vazio
	 repita
	 se borda está vazia
	 retorne falha
	 nó ← remover um nó da borda
	 se nó contém um estado objetivo então
	 retorne solução
	 adicionar nó a explorados.
	 expandir o nó se não estiver na borda ou em explorados.
 }
```