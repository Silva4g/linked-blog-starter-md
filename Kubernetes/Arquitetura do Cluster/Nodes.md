## O Que São Nodes

Nodes são as unidades fundamentais de computação do Kubernetes, representando as máquinas físicas ou virtuais sobre as quais os containers são executados. Eles são essenciais para a escalabilidade e resiliência do cluster, dividindo-se em:
- **[[Nodes Mestres]]**: Coordenam o cluster, gerenciando sua operação e estado desejado.
- **[[Nodes de Trabalho]]**: Hospedam os containers das aplicações, efetivamente realizando o trabalho computacional.
## Importância dos Nodes
A arquitetura distribuída do Kubernetes permite que as aplicações sejam executadas de forma confiável e sem interrupções, mesmo quando alguns nodes falham. Isso é essencial para sistemas em produção que requerem alta disponibilidade.
## Instalação e Configuração de Nodes
### Pré-Requisitos
Antes de adicionar um node ao cluster, certifique-se de que a máquina atende aos seguintes pré-requisitos:
- Sistema operacional compatível (preferencialmente Linux)
- Conexão de rede adequada
- Requisitos de hardware específicos (dependendo da carga de trabalho)
### Adicionando um Node ao Cluster
1. **Preparação do Node**:
    - Atualize o sistema operacional:
        `sudo apt-get update && sudo apt-get upgrade -y`
    - Instale os pré-requisitos para o Docker ou outro container runtime.
2. **Instalação do Kubelet e Kube-proxy**:
    - Siga as instruções específicas da sua distribuição Kubernetes para instalar o `kubelet` e o `kube-proxy`, que são essenciais para registrar o node no cluster e gerenciar containers.
3. **Conectando o Node ao Cluster**:
    - Utilize o comando `kubeadm join` fornecido pelo seu Node Mestre para conectar o novo node ao cluster:
        `kubeadm join <MASTER_NODE_IP>:<PORT> --token <token> --discovery-token-ca-cert-hash sha256:<hash>`
## Manutenção de Nodes
### Monitoramento de Nodes
É crucial monitorar regularmente a saúde e o desempenho dos nodes utilizando ferramentas como `kubectl top nodes` para observar a utilização de CPU e memória.
### Atualização de Nodes
Para atualizar o software do Kubernetes em seus nodes:
1. **Drene o node** para remover as workloads de forma segura:
    `kubectl drain <NODE_NAME> --ignore-daemonsets --delete-local-data`
2. **Atualize o Software**:
    - Proceda com a atualização do Kubernetes e do container runtime conforme necessário.
3. **Retorne o Node ao Serviço**:
    `kubectl uncordon <NODE_NAME>`
### Remoção de um Node
Para remover um node do cluster de forma segura, execute:
`kubectl drain <NODE_NAME> --delete-local-data --force --ignore-daemonsets kubectl delete node <NODE_NAME>`
## Troubleshooting
### Node não está Ready
Se um node não está marcado como `Ready`, verifique o status do `kubelet` e logs para possíveis erros.
`systemctl status kubelet journalctl -u kubelet`
### Problemas de Rede
Problemas de rede podem impedir que o node comunique-se com o cluster. Verifique as configurações de rede e firewalls.
### Alta Utilização de Recursos
Monitore a utilização de CPU e memória nos nodes para evitar a degradação do desempenho.
`top htop kubectl top nodes`
## Links Úteis
- Documentação Oficial do Kubernetes - [Nodes](https://kubernetes.io/docs/concepts/architecture/nodes/)
- Guia de Troubleshooting do Kubernetes