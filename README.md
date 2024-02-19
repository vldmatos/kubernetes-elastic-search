# Elastic Search Stack - Kubernetes


## Requisitos
- Cluster Kubernetes 1.20 ou superior
- Versão do Elastic e demais componentes utilizada neste exemplo: 7.17.9
- Kubectl configurado para conexão com cluster e execução dos manifestos
- Um storage-class configurado (este exemplo utiliza longhorn)
## Diagrama

Abaixo o exemplo de implementação do elastic stack com os componentes

- elastic serach
- logstash
- apm-server
- kibana

![result](/images/elastic-stack.png)  


## Preparação

Primeiro passo executar o yaml para criar o namespace no cluster kubernetes

```bash
kubectl apply -f .\manifests\namespace.yaml
```

## Instalação
Cada componente pode ser utilizado de forma separada.  
Foram separados em arquivos unicos.


### Elastic-Search
```bash
kubectl apply -f .\manifests\elastic-search.yaml
```

### Logstash
```bash
kubectl apply -f .\manifests\logstash.yaml
```

### APM-Server
```bash
kubectl apply -f .\manifests\apm-server.yaml
```

### Kibana
```bash
kubectl apply -f .\manifests\kibana.yaml
```

## Opcional
Caso tenha configurado algum Loadbanceler no ambiente, você poderá utilizar o ingress para acesso as aplicações
```bash
kubectl apply -f .\manifests\ingress.yaml
```
Caso não tenha um Loadbanceler, poderá executar um **port-forward** nos serviços das aplicações instaladas.

## Observação.
Para este exemplo o Volume Persistent criado foi baseado no storage-class do loghorn, caso utilize outro, altere as linhas abaixo do arquivo elastic-search.yaml baseando-se no seu storage-class  

![result](/images/persistent-volume.png)  

## Autenticação
As credenciais do Elastic esta na elastic-secret