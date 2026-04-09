

---

Pequenas distribuidoras (água, gás, bebidas, materiais de construção com carga leve) O dono (gestor) perde dinheiro com rotas ineficientes, falta de controle de combustível e manutenções corretivas que interrompem o faturamento.

**O produto**
Um SaaS de logística e manutenção, focado em três pilares: **Controle de Gastos**, **Saúde do Veículo** e **Otimização de Entregas**.

### A. Interface do Entregador (Mobile-First / PWA)
- **Check-in de Abastecimento:** O motorista digita o valor, litros e odômetro ao abastecer.
- **Lista de Entregas Otimizada:** Visualização dos pedidos do dia em ordem de proximidade.
- **Registro de Ocorrências:** Campo rápido para reportar problemas mecânicos.

### B. Painel do Gestor (Web)
- **Dashboard de Custos:** Gráficos de consumo real ($km/l$) por veículo e por motorista.
- **Módulo de Manutenção Preventiva:** Alertas automáticos (ex: "Moto 02 precisa trocar óleo em 100km").
- **Roteirizador de Pedidos:** Tela onde o gestor insere os endereços e o sistema gera a melhor sequência para as motos.
- **Histórico de Ativos:** Relatório completo de cada veículo para facilitar a revenda ou substituição.

### **C. Definições Técnicas** 

- **Backend (API):** Desenvolvido em **Python (FastAPI)**. Gerencia o banco de dados e processa os cálculos de consumo e intervalos de manutenção.
    
- **Frontend (PWA):** Desenvolvido em **React**. Utiliza _Media Queries_ para detectar se o acesso é via celular (mostra interface de motorista) ou computador (mostra painel administrativo).
    
- **Geocodificação e Rotas:** Integração com **Google Maps API** para transformar endereços em coordenadas e bibliotecas de **TSP (Traveling Salesperson Problem)** para ordenar as paradas.
    
- **Persistência Offline:** Uso de **Service Workers** para que o motorista possa registrar dados mesmo em áreas de sombra de sinal, sincronizando assim que recuperar a conexão.

### **D. Modelo de Negócio**

- **Assinatura Mensal (SaaS)**
- **Público-Alvo:** Distribuidoras de água, depósitos de gás, pequenas transportadoras de e-commerce local e serviços de entrega de materiais de construção.



