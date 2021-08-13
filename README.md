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

- Verificar histórico
```
kubectl rollout history deployment/deploy-manual
```

- Rollback
```
kubectl rollout undo deployment/deploy-manual --to-revision 1
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

- Instalar grafana
```
helm install democracia bitnami/grafana --set admin.password=@1234
```
OBS: https://github.com/bitnami/charts/tree/master/bitnami/rabbitmq

- Verificar grafana
```
kubectl port-forward svc/democracia-grafana 8086:3000
```

- Realizar um upgrade
```
helm upgrade --install democracia bitnami/grafana --set admin.password=@1234 --set replicaCount=2
```

- Visualizar e rollback
```
helm list
helm rollback democracia 1
```

- Desinstalar
```
helm uninstall democracia
```


## Lab 3
- Criar namespace
```
kubectl create namespace democracia
```

- Criando chart
```
helm create minnie
```

- Alterando values: 
    - hello-world
    - env: values

- Instalando
```
helm upgrade --install minninha . --dry-run
helm upgrade --install minninha .
```
OBS: Enfatizar como obter valores. Falar sobre valores pré-definidos

- Informando novo valor com -f (monstrar values)
```
helm upgrade --install minninha . -f ./values.yaml
```

- Informando novo valor com --set env.versao=v2
```
helm upgrade --install minninha . -f values.yaml --set env.versao=cmd
```

- Observando funcões
    - If
    - Range
    - With
    - Variável

## Lab 4
- Empacotando
```
helm package minninha .
```

- Criando repo 
    - Criar repositório no github (helm-repo)
    - Criar branch
    - Alterar branch em pages pra /docs
    - Verificar se está com forçar https
    - Criar arquivo index dentro da pastas docs
        helm repo index docs

- Publicando pacote
    - clonar repo
    - mudar para branch
    - criar pasta docs
    - mover pacote para pasta docs
    - commit

- Adicionando repo
```
helm repo add extreme https://github.com/willsbctm/helm-repo
```

- Instalando chart
```
helm install minninha extreme/minnie
```

## Lab 5
- Observar webhook de teste

- Rodar teste
```
helm teste minninha
```