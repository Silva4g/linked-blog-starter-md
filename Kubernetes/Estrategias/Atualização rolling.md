A atualização rolling, ou atualização contínua, é uma estratégia de atualização de software aplicada em ambientes de produção, especialmente útil em sistemas distribuídos como clusters Kubernetes. Esta estratégia permite a atualização de nodes ou aplicações com mínimo impacto na disponibilidade do serviço. No contexto do Kubernetes, uma atualização rolling é frequentemente usada para atualizar as versões dos containers rodando nas pods sem downtime.

### Funcionamento da Atualização Rolling no Kubernetes

Quando você aplica uma atualização rolling a um Deployment no Kubernetes, o processo ocorre de maneira gradual e controlada, seguindo estes passos:

1. **Criação de Novas Pods:** O Kubernetes inicia a atualização criando uma ou mais pods com a nova versão do container, enquanto ainda mantém algumas das antigas pods rodando para garantir que o serviço continue disponível.
    
2. **Remoção Gradual das Pods Antigas:** À medida que as novas pods são confirmadas como saudáveis e prontas para servir tráfego (baseado em verificações de saúde, como liveness e readiness probes), o Kubernetes gradualmente desliga e remove as pods antigas, substituindo-as pelas novas versões.
    
3. **Manutenção do Serviço:** Durante todo o processo de atualização, o serviço permanece disponível, pois o Kubernetes garante que o número de replicas especificado no Deployment seja mantido. A estratégia de atualização pode ser configurada para determinar quantas pods podem ser atualizadas simultaneamente e quantas pods antigas podem ser mantidas em execução durante a atualização.
    

### Vantagens da Atualização Rolling

- **Zero Downtime:** As aplicações podem ser atualizadas sem afetar a disponibilidade do serviço, o que é crucial para ambientes de produção onde o tempo de inatividade afeta diretamente a experiência do usuário e a receita.
- **Reversibilidade:** Se algo der errado durante a atualização, o processo pode ser facilmente revertido para o estado anterior, reduzindo o risco associado a lançamentos de novas versões.
- **Flexibilidade e Controle:** Administradores têm controle sobre a velocidade e o processo da atualização, permitindo ajustes baseados na capacidade do sistema e na tolerância a riscos.

### Desvantagens da Atualização Rolling
- As atualizações rolling podem introduzir complexidade quando se lida com aplicações stateful (que mantêm estado). A sincronização de estado entre versões antigas e novas pode ser desafiadora, especialmente se as alterações envolverem formatos de dados incompatíveis ou mudanças significativas no esquema de banco de dados.
- Durante o processo de atualização, as instâncias antigas e novas da aplicação coexistem, o que pode dobrar o uso de recursos, como CPU e memória, temporariamente. Isso requer planejamento e capacidade adicional para evitar impacto no desempenho.
- A garantia de que a nova versão da aplicação é totalmente compatível e funcionará sem problemas em produção depende significativamente de testes rigorosos e abrangentes. Há um risco de problemas não detectados afetarem a produção até que a atualização esteja completa.
- Apesar de uma das vantagens da atualização rolling ser a capacidade de fazer rollback, na prática, reverter para a versão anterior pode ser complicado, especialmente se houver mudanças no estado que não são facilmente reversíveis.
- A gestão de tráfego entre versões pode ser complexa, necessitando de balanceadores de carga inteligentes ou de uma configuração específica de serviço para direcionar o tráfego adequadamente entre as versões durante a atualização.
- Dependendo do tamanho da aplicação e do número de instâncias, a atualização rolling pode levar mais tempo para ser concluída em comparação com outras estratégias, como a atualização blue-green, onde a troca para a nova versão pode ser feita quase instantaneamente.
- Como a atualização rolling substitui gradualmente as instâncias antigas pelas novas, há um período em que ambas as versões estarão ativas simultaneamente. Se a nova versão contiver bugs críticos, isso pode afetar progressivamente a estabilidade e a disponibilidade da aplicação até que a atualização seja pausada ou revertida.
- Manter a consistência de configuração entre as versões durante a atualização pode ser desafiador, especialmente em ambientes complexos com múltiplas dependências e configurações específicas.
### Considerações

- **Recursos:** Durante a atualização, tanto as pods antigas quanto as novas estarão consumindo recursos. É importante garantir que o cluster tenha recursos suficientes para suportar esse período de transição.
- **Monitoramento:** Deve-se monitorar cuidadosamente o processo de atualização para detectar qualquer problema o mais rápido possível. Ferramentas de CI/CD e monitoramento do Kubernetes podem facilitar esse acompanhamento.

Em resumo, a atualização rolling é uma estratégia eficaz para aplicar atualizações com mínimo impacto na disponibilidade do serviço, tornando-a ideal para ambientes críticos de produção.