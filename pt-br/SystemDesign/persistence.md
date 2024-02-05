
# Persistência

## Database (Banco de Dados)
Servidores que usam disco ou memória para armazenar dados e permitir a busca desses dados. Possuem alto tempo de duração e que interage com aplicações por meio de chamadas de rede.

## Disco
Geralmente usamos disco para nos referir a HDD (hard-disk drive) ou SSD (solid-state drive). O Disco é um storage não volátil. Devido ao preço, geralmente usamos SSD para dados que precisam de constante atualização e acesso enquanto que o HD para dados raramente acessados ou atualizados.

## BD Relacional
Tipo de BD estruturado de forma que o dado é armazenado segundo um formato tabular; geralmente suporta queries poderosas usando SQL.

## BD Não-Relacional (NoSQL)
Tipo de BD livre da estrutura tabular existente no BD Relcional.

## BD Não-Relacional
Em contraste com BD relacional.

## ACID
Propriedades de transações de BD:
1. Atomicidade: as operações que constituem a transação vão todas acontecer com sucesso ou todas irão falhar. Não existe estado intermediário.

2. Consistência (ou Consistência Forte): A transação não pode levar o BD a um estado inconsistente. Uma vez commitado ou rollback, as regras aplicadas terão efeito.

3. Isolamento: A execução de múltiplas transações de forma concorrente terá o mesmo efeito delas terem sido executadas sequencialmente.

4. Durabilidade: Qualquer transação commited será escrita em um armazenamento não volátil e não será desfeita por um crash, perda de energia ou partição de rede.

## Database Index
Estrutura de dados auxiliar que permite ao BD executar algumas queries de forma muito mais rápida. Na prática criamos um índice em uma ou mais colunas para melhorar as queries de leitura mas com a desvantagem de aumentar um pouco o tempo de escrita no BD, pois as escritas também precisam ir para o índice.

## Consistência Eventual
Ao contrário da consistência forte, nesse modelo as leituras podem retornar uma visão do sistema que está obsoleta. Um BD com consistência eventual vai dar garantias que o estado do BD EVENTUALMENTE irá refletir as escritas dentro de um período de tempo (pode ser 10s ou minutos)

## Cache
Software ou hardware que armazena dados que são destinados a serem buscados de forma muito rápida. Componente que armazena dados de forma que a busca desse dado seja a mais rápida possível. O objetivo é tornar o acesso muito rápido a dados frequentemente usados. Atenção, geralmente o cache é volátil.

## Cache Hit
Termo usado quando o dado é encontrado no cache.

## Cache Miss
Quando o dado requisitado não foi encontrado no cache.

## Cache Eviction Policy
Política que especifica qual a estratégia de remoção dos dados do cache. Algumas políticas famosas são LRU (least-recently used), FIFO (first in first out) e LFU (least-frequently used).

## Memória
Nome curto para RAM (Random Access Memory) e que armazena dados para acesso rápido. Dados são perdidos quando o processo morre.

## Persistent Storage
Geralmente refere-se a disco, mas é um termo genérico para qualquer armazenamento que é persistente, ou seja, não provoca perda de dados quando o processo morre.
