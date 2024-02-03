# Kubernetes: Pods & Containers

`imagePullPolicy`
- **Always**: sempre faz o pull da imagem toda vez que o container é iniciado. *Ao especificar a tag da imagem esta política se torna desnecessária e desperdiça tempo e largura de banda.*
- **IfNotPresent:** comportamento default e correto para a maioria das situações. Se a imagem não já estiver no node, ela será baixada e depois disso ela será usada toda vez que o container iniciar. Caso a imagem esteja presente, o k8s não vai refazer o download.
- **Never:** nunca vai atualizar a imagem e, com isso, o k8s nunca fará o fetch do registry da imagem. Se já estiver no node, será usado. Caso contrário o container vai falhar ao iniciar. *Provavelmente você não quer isso.*

`Non-Root User`
UID 1000 é atribuído ao primeiro usuário não root criado no sistema. Portanto é seguro escolher valores a partir de 1000 para os containers.

