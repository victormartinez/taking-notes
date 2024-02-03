# System Design

📝 **Modelo Cliente-Servidor**
Paradigma no qual sistemas modernos são desenhados e que consiste em clientes requisitando dados/serviços e servidores provendo dados/serviços a esses clientes.

📝 **Cliente**
Máquina ou processo que requisita dado/serviço do servidor.

📝 **Servidor**
Máquina ou processo que fornece dado/serviço para um cliente, geralmente escutando chamadas de entrada de rede.

*Uma máquina/processo pode ser cliente e servidor ao mesmo tempo (e.g. servidor para usuários e cliente para o BD).*

📝 **Porta**
Número inteiro entre 0 e 65535 (2^16 portas) que permite programas escutarem novas conexões de rede na mesma máquina sem colidir. Algumas portas são reservadas ao sistema (0-1023) e são bem conhecidas (22 secure shell, 53 DNS lookup, 80 HTTP, 443 HTTPS).

📝 **Latência**
Tempo que uma determinada operação em um sistema leva para completar. Geralmente medido em tempo (miliseconds ou seconds).

Existem sistemas que são otimizados para latência (e.g. games online).

📝 **Ordens de Magnitude de Latência**
- Ler 1MB da RAM: 0.25ms (250µs)
- Ler 1MB do SSD: 1ms (1000µs)
- Ler 1MB do HD: 20ms (20000µs)
- Transferir 1MB pela rede: 10ms (10000µs)
- Round Trip (ida e volta) Inter-Continental: 150ms (150000µs)

É muito mais rápido fazer acesso a dados do que a volta ao mundo

📝 **Throughput (Vazão)**
Número de operações que um sistema pode devidamente tratar por unidade de tempo. Exemplo: quantas requisições por segundo em um servidor (RPS / QPS).

Quantos bits o servidor aguenta por segundo? Como otimizar? Aumentar o TP não necessariamente resolve um determinado problema no sistema pois provavelmente existe um ponto que é o gargalo. Talvez múltiplos servidores seja a solução.

Você não pode tomar qualquer suposição de TP baseado em Latencia ou vice-versa. Eles não necessariamente estão correlacionados.

📝 **Cache**
Software ou hardware que armazena dados que são destinados a serem buscados de forma muito rápida.

📝 **Cache Hit**
Termo usado quando o dado é encontrado no cache.

📝 **Cache Miss**
Quando o dado requisitado não foi encontrado no cache.

📝 **Cache Eviction Policy**
Política pela qual um determinado dado é removido do cache. Exemplos: LRU (least-recently used), FIFO (first in first out) e LFU (least-frequently used).

📝 **Cache Eviction Policy**
Política pela qual um determinado dado é removido do cache. Exemplos: LRU (least-recently used), FIFO (first in first out) e LFU (least-frequently used).

📝 **BD Relacional**
Tipo de BD estruturado de forma que o dado é armazenado segundo um formato tabular; geralmente suporta queries poderosas usando SQL.

📝 **BD Não-Relacional (NoSQL)**
Tipo de BD livre da estrutura tabular existente no BD Relcional.

📝 **BD Não-Relacional**
Em contraste com BD relacional.

📝 **ACID**
Propriedades de transações de BD:
1. Atomicidade: as operações que constituem a transação vão todas acontecer com sucesso ou todas irão falhar. Não existe estado intermediário.

2. Consistência (ou Consistência Forte): A transação não pode levar o BD a um estado inconsistente. Uma vez commitado ou rollback, as regras aplicadas terão efeito.

3. Isolamento: A execução de múltiplas transações de forma concorrente terá o mesmo efeito delas terem sido executadas sequencialmente.

4. Durabilidade: Qualquer transação commited será escrita em um armazenamento não volátil e não será desfeita por um crash, perda de energia ou partição de rede.

📝 **Database Index**
Estrutura de dados auxiliar que permite ao BD executar algumas queries de forma muito mais rápida. Na prática criamos um índice em uma ou mais colunas para melhorar as queries de leitura mas com a desvantagem de aumentar um pouco o tempo de escrita no BD, pois as escritas também precisam ir para o índice.

📝 **Consistência Eventual**
Ao contrário da consistência forte, nesse modelo as leituras podem retornar uma visão do sistema que está obsoleta. Um BD com consistência eventual vai dar garantias que o estado do BD EVENTUALMENTE irá refletir as escritas dentro de um período de tempo (pode ser 10s ou minutos)

📝 **Endereço IP**
Endereço dado a uma máquina que está conectada na internet pública. IPV4 consistem em 4 números separados por números (**a.b.c.d**) entre 0 e 255. Casos especiais incluem **127.0.0.1** que é sua máquina local (localhost) e **192.168.x.y** que corresponde a sua rede privada.

📝 **DNS (Domain Name System)**
Descreve entidades e protocolos envolvidos na tradução de nomes de domínio para endereços IP.

📝 **Database**
Servidores que usam disco ou memória para armazenar dados e permitir a busca desses dados. Possuem alto tempo de duração e que interage com aplicações por meio de chamadas de rede.

📝 **Disco**
Geralmente usamos disco para nos referir a HDD (hard-disk drive) ou SSD (solid-state drive). O Disco é um storage não volátil. Devido ao preço, geralmente usamos SSD para dados que precisam de constante atualização e acesso enquanto que o HD para dados raramente acessados ou atualizados.

📝 **Memória**
Nome curto para RAM (Random Access Memory) e que armazena dados para acesso rápido. Dados são perdidos quando o processo morre.

📝 **Persistent Storage**
Geralmente refere-se a disco, mas é um termo genérico para qualquer armazenamento que é persistente, ou seja, não provoca perda de dados quando o processo morre.

📝 **Availability**
Um servidor que tem 99% de disponibilidade será operacional em 99% do tempo (ou seja, dois noves de disponibilidade).

📝 **High Availability (HA)**
Alta Disponibilidade descreve sistemas que possuem alto nível de disponibilidade, geralmente 5 noves ou mais.

📝 **Nines (Noves)**
Tipicamente refere-se a porcentagens de *uptime*. Por exemplo, cinco 9s indica 99.999% do tempo up.

- 99%: 87.7h
- 99.9%: 8.8h
- 99.99%: 52.6m
- 99.999%: 5.3m

📝 **Redundância**
Processo de replicação de partes do sistema como um esforço de torná-lo mais confiável.

📝 **SLA (Service-Level Agreement)
Coleção** de garantias dadas a um cliente acerca da disponibilidade (e outras coisas) do sistema.

📝 **SLO (Service-Level Objective)
Garantia** dada a um cliente acerca da disponibilidade (e outras coisas) do sistema. SLOs formam a SLA.

📝 **Forward Proxy
aka Proxy.** Servidor posicionado entre o cliente e os servidores e que atua em nome do cliente para mascarar a identidade dele (IP) pois o IP utilizado na nova request será do Proxy. VPNs funcionam de forma similar.

📝 **Reverse Proxy**
Servidor posicionado entre o cliente e os servidores e atua em nome dos servidores, tipicamente para log, Load Balance, adicionar metadata/headers em requests, cache, filtrar requests que você não quer lidar.

📝 **NGINX**
Popular como Reverse Proxy e LB.

![Untitled](https://prod-files-secure.s3.us-west-2.amazonaws.com/c266ba40-ee22-4bd3-81a5-110b123849ef/fcfb6f0a-69ec-44be-9b5f-c60b3b9c4212/Untitled.png)

📝 **Hashing**
Ação que consiste em transformar um dado em um valor de tamanho fixo, geralmente um número inteiro. O dado pode ser qualquer coisa: endereço IP, username, HTTP Request, etc.

Ex de caso de uso: fazer o hash do username de quem está fazendo a request e com a função MOD rotear a request para um servidor específico. Entao o mesmo usuário sempre vai bater no mesmo servidor. Esse servidor pode, então, implementar um cache em memória para otimizar a resposta.

Uma boa função hash vai balancear os dados.

📝 **Hashing Function**
Função que aceita como entrada um dado e joga pra fora um número. Uma boa função tenta minimizar *hash collisions* (o que é equivalente a maximizar **uniformidade**).

📝 **Consistent Hashing**
Tipo de hash que minimiza o número de chaves que precisam ser remapeadas quando a hash table é redimensionada. É geralmente usado por LB para distribuir tráfego; minimiza o número de requisições que são redirecionadas para diferentes servidores quando novos servidores são adicionados ou quando servidores existentes são derrubados.

📝 **Rendezvous Hashing**
Tipo de hash também chamado de *Highest Random Weight* hashing. Permite re-distribuição mínima de mapeamentos quando um server cai.

📝 **SHA**
Nome curto para Secure Hash Algorithms. SHA é uma coleção de funções hash criptográficas usadas na indústria.

📝 **IP (Internet Protocol)**
Protocolo de rede** que desenha como todas as comunicações máquina-máquina devem acontecer ao redor do mundo. Protocolos como TCP, UDP e HTTP são construídos em cima do IP.

📝 **TCP**
Protocolo de rede** construído em cima do IP e que permite entrega ordenada e confiável de dados entre máquinas conectadas na internet. TCP adiciona um TCP header dentro pacote IP para garantir a entrega. Geralmente TCP é implementado no kernel e expõe **sockets** para aplicações que desejam fazer streaming de dados via conexão aberta.

📝 **HTTP (HyperText Transfer Protocol)**

**Protocolo de rede** comum construído em cima do TCP para troca de texto cliente-servidor. Implementa o paradigma request/response. IP e TCP são protocolos bem utilizados para transporte de dados enquanto que o HTTP traz a possibilidade de adicionar uma camada de regras de negócio por meio da exposição de rotas que podem receber dados/headers/etc.
****

📝 **IP Packet**
Também chamado genericamente de pacote de rede, corresponde a menor unidade usada para descrever dados enviados por IP. Consiste em um cabeçalho (que contém endereços de IP de origem e destino e metadados) e um payload (2^16 bytes) (que é o dado sendo enviado pela rede).

📝 **Cache**
Componente que armazena dados de forma que a busca desse dado seja a mais rápida possível. O objetivo é tornar o acesso muito rápido a dados frequentemente usados. Atenção, geralmente o cache é volátil.

📝 **Cache Hit**
Termo para indicar que um determinado dado foi encontrado no cache.

📝 **Cache Miss**
Termo para indicar que um determinado dado NÃO foi encontrado no cache.

📝 **Cache Eviction Policy**
Política que especifica qual a estratégia de remoção dos dados do cache. Algumas políticas famosas são LRU (least-recently used), FIFO (first in first out) e LFU (least-frequently used).

📝 **CDN**
aka PoPs (Points of Presence).Serviço de terceiros que funciona como cache para nossos servidores. Algumas aplicações web podem estar lentas para usuários em determinadas regiões do planeta devido aos servidores estarem muito distante deles. Servidores CDN estão espalhados no mundo a fim de entregar dados com uma latência menor.

Serviço de terceiros que funciona como Cache para os servidores. Algumas aplicações web podem ser lentas para usuários de uma determinada região se o seu servidor estiver em outra. O CDN tem servidores espalhados no mundo de forma que a latência para eles é menor do que acessar diretamente o seu servidor.

📝 **Load Balancers**
É um tipo de Proxy Reverso que distribui tráfego pelos servidores. São encontrados nos mais diversos cenários, desde a camada DNS até o BD.

LB geralmente fazem healthchecks para saber a saúde dos servidores, recursos usados, Response Time médio, etc.

📝 **Server-Selection Strategy**
Estratégia utilizada pelo LB para selecionar os servidores que recebem o tráfego. Ex: Round-Robin, Random Selection, Performance-based Selection (fastest response time, least amount of traffic), IP-based routing.

📝 **Hot Spot**
Ao distribuir uma carga entre os servidores ela pode acabar sendo distribuída de forma desigual. Isso pode acontecer se a *sharding key* ou a *hashing function* não forem ótimas ou se sua carga é naturalmente desbalanceada. Alguns servidores vão receber muito mais tráfego do que outros, criando assim um *hot spot*.