![[1*-zkqfnQqG99F09dPDLJF5w.png]]
Nodes de trabalho (Worker Nodes) são os componentes de um cluster Kubernetes responsáveis por executar as aplicações e cargas de trabalho. Eles são os "músculos" do cluster, fornecendo a capacidade computacional necessária para rodar os containers organizados em pods. Aqui estão mais detalhes sobre sua função, componentes e gerenciamento
## Conceito e Função
### Execução de [[Pods]]
A principal função de um node de trabalho é executar pods, que são conjuntos de um ou mais containers. Os containers dentro de um pod compartilham o mesmo namespace de rede e podem se comunicar entre si usando `localhost`.
### Gerenciamento de Recursos
Nodes de trabalho gerenciam recursos de hardware como CPU, memória, armazenamento e rede para os containers.
### Comunicação
Eles se comunicam com os nodes mestres para receber instruções sobre quais [[Pods]] executar e reportam o estado e o progresso da execução dos pods de volta aos mestres.
## Gerenciamento e Manutenção
### Autossuficiência
Nodes de trabalho são projetados para serem autossuficientes e resilientes. Eles podem se auto-recuperar de falhas de software e continuar a executar cargas de trabalho com pouca ou nenhuma intervenção manual.
### Escalabilidade
O Kubernetes permite a adição ou remoção de nodes de trabalho para ajustar a capacidade computacional do cluster conforme necessário. Isso é feito manualmente por administradores ou automaticamente por soluções de escalabilidade automática.
## Segurança
### Isolamento de Workload
Embora múltiplos pods possam ser executados no mesmo node de trabalho, o Kubernetes oferece mecanismos para isolar workloads uns dos outros, se necessário, utilizando políticas de rede, namespaces, e outros controles de acesso.
### Atualizações e Patches
Manter o software dos nodes de trabalho, incluindo o sistema operacional, o runtime de containers e os componentes do Kubernetes, atualizados e com patches aplicados é vital para a segurança e estabilidade do cluster.
## Componentes Principais
Cada node de trabalho contém os seguintes componentes essenciais para funcionar dentro de um cluster Kubernetes:
### [[kubelet]]
É um agente que roda em cada node de trabalho. Ele garante que os containers estão rodando em um Pod. O Kubelet recebe um conjunto de especificações chamadas PodSpecs, que descrevem um pod, e garante que os containers descritos estejam corretamente executando e saudáveis.
### [[Proxy]]
Roda em cada node de trabalho, o Kube-Proxy gerencia o roteamento de rede e a comunicação para os pods, permitindo a comunicação entre pods dentro do cluster ou com a internet.
### Container Runtime
É o software responsável por rodar os containers. O Kubernetes suporta vários runtimes de containers, como Docker, containerd, e CRI-O.
## Links Uteis
Documentação oficial - [Nodes](https://kubernetes.io/docs/concepts/architecture/nodes/)
