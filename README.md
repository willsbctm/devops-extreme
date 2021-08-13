# Exemplos

## Lab 1
- Criar namespace
```
kubectl create namespace manual
``` 

- Aplicar criação de objetos
```
kubectl apply -f ./deploy-tradicional.yaml
```
OBS: deploy-tradicional.yaml

- Verificar histórico
```

kubectl rollout history deployment/deploy-manual
```

- Rollback
```
kubectl rollout history deployment/deploy-manual
```


## Lab 2
- Criar namespace
```
kubectl create namespace antifascismo
```

Passos:
- Adicionar repositório de charts da bitnami
```
helm repo add bitnami https://charts.bitnami.com/bitnami
```

- Instalar o chart do rabbitmq
```
helm install antifa bitnami/rabbitmq --set image.repository=rabbitmq --set image.tag=management
```
OBS: https://github.com/bitnami/charts/tree/master/bitnami/rabbitmq

- Acessando RabbitMq
```
kubectl port-forward svc/antifa-rabbitmq 8085:15672
```

- Verificando instalação do chart
```
helm list
helm history antifa
```

- Desinstalando RabbitMq
```
helm uninstall antifa
```

- Removendo repositorio
```
helm repo remove bitnami
```

## Lab 3

- Instalar grafana
```
helm install democracia bitnami/grafana --set admin.password=@1234
```
OBS: https://github.com/bitnami/charts/tree/master/bitnami/rabbitmq

- Verificar grafana
```
kubectl port-forward svc/democracia-grafana 8086:3000
```

- Tentar instalar novamente

- Realizar um upgrade
```
helm upgrade democracia bitnami/grafana --set admin.password=@1234 --set replicaCount=2 --set service.type=LoadBalancer
```

- Verificar grafana
```
127.0.0.1:3000
```

- Realizar outro upgrade
```
helm upgrade democracia bitnami/grafana --set admin.password=@1234 --set replicaCount=2
```

- Verificar valores perdidos

- Realizar outro upgrade
```
helm upgrade democracia bitnami/grafana --set admin.password=@1234 --set replicaCount=2 --set service.type=LoadBalancer
```

- Reutilizar valores
```
helm upgrade democracia bitnami/grafana --reuse-values --set replicaCount=1
```

- Verificar valores alterados

- Instalar/atualizar
```
helm upgrade --install democracia bitnami/rabbitmq --reuse-values
```

- Desinstalar
```
helm uninstall democracia --keep-history
```

- Visualizar e rollback
```
helm list -A
helm democracia antifa 1
```


## Lab 4
- Criando chart
```
helm create minnie
```

- Alterando values: 
    - hello-world
    - env: values

- Instalando
```
helm upgrade --install minninha .
```

- Informando novo valor com -f 
```
helm upgrade --install minninha . -f ./values.yaml
```

- Informando novo valor com --set env.versao=v2
```
helm upgrade --install minninha . -f values.yaml --set env.versao=cmd
```

- Observando funcões do helm

- Observando go templates

## Lab 5
- Empacotando
```
helm package minninha .
```

- Criando repo 
    - Criar repositório no github (extreme)
    - Criar branch
    - Alterar branch em pages pra /docs
    - Verificar se está com forçar https

- Publicando pacote
    - clonar repo
    - mudar para branch
    - criar pasta docs
    - mover pacote para pasta docs
    - commit

- Adicionando repo
```
helm repo add extreme https://github.com/willsbctm/extreme
```

- Instalando chart
```
helm install minninha extreme/minnie
```

## Lab 6
- Observar webhook de teste

- Rodar teste
```
helm teste minninha
```