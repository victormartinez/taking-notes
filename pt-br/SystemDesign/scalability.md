
# Escalabilidade

## Latência
Tempo que uma determinada operação em um sistema leva para completar. Geralmente medido em tempo (miliseconds ou seconds).

Existem sistemas que são otimizados para latência (e.g. games online).

## Ordens de Magnitude de Latência
- Ler 1MB da RAM: 0.25ms (250µs)
- Ler 1MB do SSD: 1ms (1000µs)
- Ler 1MB do HD: 20ms (20000µs)
- Transferir 1MB pela rede: 10ms (10000µs)
- Round Trip (ida e volta) Inter-Continental: 150ms (150000µs)

É muito mais rápido fazer acesso a dados do que a volta ao mundo

## Throughput (Vazão)
Número de operações que um sistema pode devidamente tratar por unidade de tempo. Exemplo: quantas requisições por segundo em um servidor (RPS / QPS).

Quantos bits o servidor aguenta por segundo? Como otimizar? Aumentar o TP não necessariamente resolve um determinado problema no sistema pois provavelmente existe um ponto que é o gargalo. Talvez múltiplos servidores seja a solução.

Você não pode tomar qualquer suposição de TP baseado em Latencia ou vice-versa. Eles não necessariamente estão correlacionados.

## SLA (Service-Level Agreemen
Coleção** de garantias dadas a um cliente acerca da disponibilidade (e outras coisas) do sistema.

## SLO (Service-Level Objectiv
Garantia** dada a um cliente acerca da disponibilidade (e outras coisas) do sistema. SLOs formam a SLA.

## Modelo Cliente-Servidor
Paradigma no qual sistemas modernos são desenhados e que consiste em clientes requisitando dados/serviços e servidores provendo dados/serviços a esses clientes.

## Cliente
Máquina ou processo que requisita dado/serviço do servidor.

## Servidor
Máquina ou processo que fornece dado/serviço para um cliente, geralmente escutando chamadas de entrada de rede.

*Uma máquina/processo pode ser cliente e servidor ao mesmo tempo (e.g. servidor para usuários e cliente para o BD).*

## Forward Proxy
aka Proxy.** Servidor posicionado entre o cliente e os servidores e que atua em nome do cliente para mascarar a identidade dele (IP) pois o IP utilizado na nova request será do Proxy. VPNs funcionam de forma similar.

## Reverse Proxy
Servidor posicionado entre o cliente e os servidores e atua em nome dos servidores, tipicamente para log, Load Balance, adicionar metadata/headers em requests, cache, filtrar requests que você não quer lidar.

## NGINX
Popular como Reverse Proxy e LB.

## Redundância
Processo de replicação de partes do sistema como um esforço de torná-lo mais confiável.

## CDN
aka PoPs (Points of Presence).Serviço de terceiros que funciona como cache para nossos servidores. Algumas aplicações web podem estar lentas para usuários em determinadas regiões do planeta devido aos servidores estarem muito distante deles. Servidores CDN estão espalhados no mundo a fim de entregar dados com uma latência menor.

Serviço de terceiros que funciona como Cache para os servidores. Algumas aplicações web podem ser lentas para usuários de uma determinada região se o seu servidor estiver em outra. O CDN tem servidores espalhados no mundo de forma que a latência para eles é menor do que acessar diretamente o seu servidor.

## Load Balancers
É um tipo de Proxy Reverso que distribui tráfego pelos servidores. São encontrados nos mais diversos cenários, desde a camada DNS até o BD.

LB geralmente fazem healthchecks para saber a saúde dos servidores, recursos usados, Response Time médio, etc.

## Server-Selection Strategy
Estratégia utilizada pelo LB para selecionar os servidores que recebem o tráfego. Ex: Round-Robin, Random Selection, Performance-based Selection (fastest response time, least amount of traffic), IP-based routing.

## Availability
Um servidor que tem 99% de disponibilidade será operacional em 99% do tempo (ou seja, dois noves de disponibilidade).

## High Availability (HA)
Alta Disponibilidade descreve sistemas que possuem alto nível de disponibilidade, geralmente 5 noves ou mais. How to achieve HA? You want to avoid Single Points of Failure. Using Redundancy is the way to get rid of that.

## Nines (Noves)
Tipicamente refere-se a porcentagens de *uptime*. Por exemplo, cinco 9s indica 99.999% do tempo up.

- 99%: 87.7h
- 99.9%: 8.8h
- 99.99%: 52.6m
- 99.999%: 5.3m

| Availability (%)         | Downtime / year     | Downtime / month    | Downtime / week     | Downtime / day      |
|--------------------------|---------------------|---------------------|---------------------|---------------------|
| 90% (one nine)           | 36.53 dias          | 73.05 horas         | 16.80 horas         | 2.4 horas           |
| 99% (two nines)          | 3.65 horas          | 7.31 horas          | 1.68 horas          | 14.40 minutos       |
| 99.9% (three nines)      | 8.77 horas          | 43.83 minutos       | 10.08 minutos       | 1.44 minutos        |
| 99.99% (four nines)      | 52.60 minutos       | 4.38 minutos        | 1.01 minutos        | 8.64 segundos       |
| 99.999% (five nines)     | 5.26 minutos        | 26.30 segundos      | 6.05 segundos       | 864 milisegundos    |
| 99.9999% (six nines)     | 31.56 segundos      | 2.63 segundos       | 604.80 milisegundos | 86.40 milisegundos  |
| 99.99999% (seven nines)  | 3.16 segundos       | 262.98 milisegundos | 60.48 milisegundos  | 8.64 milisegundos   |
| 99.999999% (eight nines) | 315.58 milisegundos | 26.30 milisegundos  | 6.05 milisegundos   | 864 microsegundos   |
| 99.9999999% (nine nines) | 31.56 milisegundos  | 2.63 milisegundos   | 604.80 milisegundos | 86.40 microsegundos |