## Padrão de Multi-Containers (Sidecar, Ambassador, e Adapter)
Aplicações complexas muitas vezes exigem funcionalidades complementares como monitoramento, logging, comunicação de rede, que podem poluir o código da aplicação principal se integradas diretamente.
Utilizar múltiplos contêineres dentro de um único Pod, cada um com sua responsabilidade específica, mantendo o contêiner principal focado na aplicação:

- **Sidecar**: Executa uma função de suporte ao contêiner principal, como log ou sincronização de arquivos.
- **Ambassador**: Gerencia as comunicações de rede, agindo como um proxy para o contêiner principal.
- **Adapter**: Padroniza e expõe métricas de diferentes contêineres de forma uniforme para monitoramento. 