
#Concluded 

---
O ciclo de vida de uma Activity é um conjunto de estados pelos quais a tela do aplicativo passa, desde o momento em que é lançada até ser destruída 

- **onCreate()**:Aqui você deve realizar as inicializações estáticas, como inflar o layout, inicializar ViewModels e vincular dados a listas. Ele recebe um objeto **Bundle** que pode conter o estado anterior da UI para restauração.
    
- **onStart()**: Torna a Activity visível para o usuário. É o momento ideal para inicializar códigos que mantêm a interface atualizada.
    
- **onResume()**: A Activity entra em primeiro plano e torna-se interativa. Neste estado, você deve ativar componentes que precisam de foco exclusivo, como a câmera ou sensores (GPS).
    
- **onPause()**: É o primeiro sinal de que o usuário está saindo da tela, embora ela ainda possa estar parcialmente visível. Deve-se pausar operações que não devem continuar sem o foco do usuário.
    
- **onStop()**: A Activity não está mais visível para o usuário. É o ponto correto para liberar recursos intensivos e salvar dados persistentes no banco de dados.
    
- **onRestart()**: Chamado quando a Activity estava no estado _Stopped_ e o usuário volta para ela. Após este método, o sistema sempre chama o onStart().
    
- **onDestroy()**: A etapa final antes da destruição total da Activity. Ocorre quando o usuário termina a atividade ou o sistema a destrói para liberar memória.

Para otimizar o desempenho, siga estas diretrizes de implementação:
- **Recursos Interativos (Câmera, GPS)**: Devem ser iniciados no `onResume()` e liberados no `onPause()`. Isso garante que o recurso só esteja ativo enquanto o usuário interage diretamente com a tela, economizando bateria.
    
- **Recursos Visuais**: Podem ser iniciados no `onStart()` e liberados no `onStop()`. Isso é particularmente importante para suportar o modo **multi-janela**, onde sua Activity pode estar visível (no estado _Paused_), mas não ter o foco principal.

![](../../../attachments/Pasted%20image%2020260428140844.png)

![400](../../../attachments/Pasted%20image%2020260408135237.png)
![](../../../attachments/Pasted%20image%2020260408135349.png)
