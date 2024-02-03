# Kubernetes: Affinity
Existem casos em que um Pod tem requisitos especiais (*e.g.* mais uso de CPU, mais uso de memória, ou mesmo é mais caro para reiniciar) e você não quer correr o risco dele cair em um node preemptivo. Node Affinity permite que você expresse essa preferência de forma soft ou hard.


## Affinity

- `requiredDuringSchedulingIgnoredDuringExecution (hard)`: A regra DEVE ser satisfeita para escalonar o pod.

```yaml
apiVersion: v1
kind: Pod
...
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: "failure-domain.beta.kubernetes.io/zone"
            operator: In
            values: ["us-central1-a"]  
```

- `preferredDuringSchedulingIgnoredDuringExecution (soft)`: Preferível, mas não é crítica.

```yaml
apiVersion: v1
kind: Pod
...
spec:
  affinity:
    nodeAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        nodeSelectorTerms:
        - matchExpressions:
          - key: "failure-domain.beta.kubernetes.io/zone"
            operator: In
            values: ["us-central1-a"]  
```

```
⚠️ **Cuidado:** essas regras são válidas em tempo de Escalonamento, não de execução. A mudança nessa regra não faz com que os pods que já foram escalonados sejam movidos para outros nodes.
```

## Anti-Affinity

Hard

```yaml
...
spec:
  affinity:
    podAffinity:
      requiredDuringSchedulingIgnoredDuringExecution:
        labelSelector:
        - matchExpressions:
          - key: app
            operator: In
            values: ["cache"]
        topologyKey: kubernetes.io/hostname
```

Soft

```yaml
spec:
  affinity:
    podAntiAffinity:
      preferredDuringSchedulingIgnoredDuringExecution:
      - weight: 1
        podAffinityTerm:
          labelSelector:
          - matchExpressions:
            - key: app
              operator: In
              values: ["cache"]
          topologyKey: kubernetes.io/hostname
```