![[components-of-kubernetes 1.svg]]
Em resumo, os nodes mestres desempenham um papel crítico na gestão e operação de um cluster Kubernetes. Eles não são apenas um conjunto de componentes; representam a fundação para a orquestração de contêineres, gerenciamento de recursos, escalabilidade e segurança do cluster. Administrar os nodes mestres com cuidado é essencial para manter a saúde e a eficiência do cluster Kubernetes.
## Conceito e Função dos Nodes Mestres
Os nodes mestres, ou o plano de controle, são os cérebros por trás do cluster Kubernetes. Eles gerenciam o estado do cluster, tomando decisões globais sobre o cluster, como o agendamento de [[Pods]], e respondendo a eventos do cluster. Os nodes mestres garantem que o estado atual do cluster Kubernetes sempre corresponda ao estado desejado especificado pelas definições de recursos.
## Arquitetura e Design
Em um ambiente de produção, os nodes mestres são configurados em um modo de alta disponibilidade (High Availability (HA)), normalmente usando múltiplos servidores para evitar um ponto único de falha. A configuração HA assegura que o cluster permaneça operacional mesmo em caso de falha de um node mestre.
## Comunicação e Segurança
O acesso ao [[API Server]], que roda nos nodes mestres, é rigorosamente controlado usando autenticação e autorização (por exemplo, através de [[RBAC]] - Role-Based Access Control). Além disso, a comunicação entre os nodes mestres e os [[Nodes de Trabalho]] (ou nodes workers) é frequentemente criptografada e autenticada para garantir a integridade e a confidencialidade dos dados.
## Escalabilidade
Node mestres são criticos mas e por isso escalaveis, para isso temos que escalar o API Server horizontalmente adicionando mais instâncias para lidar com um aumento no volume de solicitações.
## Manutenção e Atualizações
A manutenção dos nodes mestres é crucial para a segurança , desempenho e estabilidade do cluster. As atualizações podem ser desafiadoras, dada a importância dos nodes mestres para a operação do cluster, mas ferramentas e práticas recomendadas, como a [[Atualização rolling]], minimizam o tempo de inatividade e os impactos nas cargas de trabalho do cluster
## Componentes dos Nodes Mestres
- [[API Server]] (`kube-apiserver`) - Atua como a porta de entrada para a API do Kubernetes, permitindo a comunicação entre os diversos componentes do cluster e a gestão dos recursos do Kubernetes.
- [[Scheduler]] (`kube-scheduler`) - Responsável por agendar pods nos nodes, levando em consideração os requisitos de recursos e outras restrições.
- [[Controller Manager]] (`kube-controller-manager`) -  Executa os processos de controle do Kubernetes, como o controlador de nodes, de endpoints, e de namespace.
- [[Cloud Controller Manager]] - 
- [[etcd]] - Banco de dados de chave-valor que armazena todas as informações do cluster, atuando como a fonte de verdade para o estado do cluster.
## Links Uteis
- Documentação Oficial do Kubernetes: [Componentes do Cluster](https://kubernetes.io/docs/concepts/overview/components/)
- Guia de Alta Disponibilidade para Kubernetes: [Configurando Alta Disponibilidade](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/)