# Kubernetes: Labels & Selectors

## Labels
Pares de chave-valor que são associados a **objetos** e tem a intenção de identificar atributos significativos desses objetos que são relevantes para o usuário mas não necessariamente implicam em uma semântica para o K8s.

Labels funcionam como filtros. Por exemplo, podem ser usados para o ReplicaSet monitorar o mínimo de replicas que uma determinada aplicação deve ter por nó.

```yaml
# replicaset-definition.yml
[...]
selector:
    matchLabels:
        tier: front-end
[...]
```

```yaml
# pod-definition.yml
[...]
metadata:
    name: myapp-pod
    labels:
        tier: front-end
[...]
```

## Selectors

Expressão que dá match em uma ou mais labels. Além de serem usados para conectar Services e Pods, também podem ajudar em queries:

```
kubectl get pods --all-namespaces --selector app=demo
```

```yaml
selector:
    matchExpressions:
    - {key: environment, operator: In, values: [staging, production]}

selector:
    matchExpressions:
    - {key: environment, operator: NotIn, values: [production]}
```

**OBS-1:** É possível usar Labels para fazer Canary Deployments.

**OBS-2:** Labels vs Annotations

- Labels identificam recursos. Annotations servem a ferramentas externas ao K8s.