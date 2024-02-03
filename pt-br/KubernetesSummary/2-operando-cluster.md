# Kubernetes: Operando Cluster

**Planejando a Capacidade:** pense em quantos servidores tradicionais você precisa para rodar as aplicações.

**Tamanho Mínimo:** Se você está testando o serviços, comece com um cluster pequeno. Se você for utilizar um serviço gerenciável (*e.g.* GKE), comece com 1 node pois ele já gerencia a master pra você. Porém, se você for gerenciar seu cluster, 3 masters é o mínimo que você precisa para ter alta disponibilidade.

**O maior cluster:** Para máxima confiança, mantenha seu cluster menor que 5k nodes e 150k pods. Se você precisa de mais recursos, rode múltiplos clusters.

**Clusters Federados:** Se você tem demandas de carga muito extremas ou precisa operar em larga escala, os limites do cluster podem se tornar um problema pra você. Nesse caso, execute múltiplos clusters e, se necessário, faça a federação deles, de forma que workloads possam ser replicados pelos clusters. Federação permite termos dois ou mais clusters sincronizados, executando workloads idênticos. Isso é útil para termos diferentes cloud providers (resiliência). Um grupo de clusters federados pode continuar em execução mesmo que um cluster individual falhe. Porém, a maioria dos usuários não precisa de Federação e, na prática, a maioria deles em grande escala lidam com seus workloads em múltiplos clusters não federados.

**Preciso de múltiplos clusters?** Provavelmente não. A menos que você opere em uma escala muito grande.

**Boa prática:** use um único cluster para produção e um para staging, a menos que você realmente precise de isolamento completo entre times. Para particionar o cluster para fácil gerenciamento, use namespaces.

**Nodes e Instances:** Use o melhor custo benefício em termos de máquina que o seu cloud provider oferece. Geralmente nodes maiores são mais baratos. Leve em consideração que em cada node roda componentes do k8s (*e.g.* kubelet) **que consome um pouco da capacidade. Portanto, nodes muito pequenos podem não ser o ideal.**

Nodes heterogêneos: Você pode precisar de nodes com características diferentes (*e.g.* GPU) e usar a funcionalidade de *resource limits* para especificar que um Pod precisa de ao menos uma GPU.

Bare metal: K8s pode rodar também em servidores bare-metal. Se você ainda está migrando para a Cloud, você pode usar essa capacidade ociosa.

**Escalando o Cluster:** Você pode adicionar novas instâncias através do *kops* ou da interface do seu cloud provider (*e.g.* node pools no GKE). Em caso de *scaling down nodes*, não termine os nodes que você não precisa. Use o *drain* (*kubectl drain*) para garantir que os workloads desse node serão migrados para outro node. Com isso você garante que tem capacidade suficiente de sobra.

**Autoscaling:** Pode levar um tempo para que você consiga ajustar a regra ideal de autoscaling (seja por uso de recurso ou por período do dia). A melhor prática é: não habilite autoscaling só porque está lá, você provavelmente não vai precisar a menos que sua demanda seja extremamente variável. Escale seu cluster manualmente até você ter rodado ele por um tempo e ter captado a forma como a escalabilidade dele muda ao longo do tempo.

**Ferramentas para Conformidade:** Sonobuoy, K8Guard, Copper, kube-bench, Kubernetes Audit Logging, Chaos Testing (chaoskube, kube-monkey, powefulseal).