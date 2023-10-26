## Exemplo básico de uso do K8S
Vamos utilizar o [Kind](https://kind.sigs.k8s.io/) numa máquina local, apenas para fins didáticos.<br>
O primeiro passo é criar um __Cluster__

Criando o Cluster<br>
   ```kind create cluster```<br><br>
   Para checar se o cluster foi criado:<br>
   ```kubectl get nodes```<br><br>
   
A saída no terminal deve ser parecer com essa:<br>
   ```shell
NAME                 STATUS   ROLES           AGE   VERSION
kind-control-plane   Ready    control-plane   89m   v1.27.3
```


<br>Criando um __Pod__<br>
Lembrando que um Pod é uma espécie de container runtime do K8S.<br><br>
Nesse exemplo vamos criar o arquivo [pod.yaml](https://github.com/ericolvr/K8S/blob/master/pod.yaml).<br>
Com o arquivo criado vamos executar esse Pod no nosso cluster com o comando:<br>
```kubectl apply -f pod.yaml```<br><br>
A saída no terminal deve ser parecer com essa:<br>
   ```shell
pod/nginx created
```
<br>Para listar o(s) pod(s) use o comando:<br>
```kubectl get pods```<br><br>
A saída no terminal deve ser parecer com essa:<br>
   ```shell
NAME                     READY   STATUS    RESTARTS   AGE
nginx                    1/1     Running   0          4m6s
```

<br>Para deletar o(s) pod(s) use o comando:<br>
```kubectl delete pod <pod_name>```<br><br>
A saída no terminal deve ser parecer com essa:<br>
   ```shell
pod "nginx" deleted
```

<br>Criando um __Replica Set__<br>
Lembrando que um Replica Set é quem gerencia/orquestra nossos pods, com base em algumas pre-definições.<br><br>
Nesse exemplo vamos criar o arquivo [replicaset.yaml](https://github.com/ericolvr/K8S/blob/master/replicaset.yaml).<br>
Iremos definir 10 réplicas/pods do Nginx <br>
```kubectl apply -f replicaset.yaml```<br><br>
A saída no terminal deve ser parecer com essa:<br>
   ```shell
replicaset.apps/nginx-replicaset created
```

<br>Para listar o(s) replicaset use o comando:<br>
```kubectl get pods```<br><br>
A saída no terminal deve ser parecer com essa:<br>
   ```shell
NAME               DESIRED   CURRENT   READY   AGE
nginx-replicaset   10        10        10      63s
```

<br>Agora se fizermos um get pods:<br>
```kubectl get pods```<br><br>
A saída no terminal deve ser parecer com essa:<br>
__Note que agora temos 10 réplicas/pods do Nginx.yaml__
   ```shell
NAME                     READY   STATUS    RESTARTS   AGE
nginx-replicaset-5xrlm   1/1     Running   0          4m11s
nginx-replicaset-68pzw   1/1     Running   0          4m11s
nginx-replicaset-c4w7b   1/1     Running   0          4m11s
nginx-replicaset-k74jr   1/1     Running   0          4m11s
nginx-replicaset-l49nr   1/1     Running   0          4m11s
nginx-replicaset-qpwqv   1/1     Running   0          4m11s
nginx-replicaset-ts7wt   1/1     Running   0          4m11s
nginx-replicaset-twfhr   1/1     Running   0          4m11s
nginx-replicaset-xzbs5   1/1     Running   0          4m11s
nginx-replicaset-z2q2h   1/1     Running   0          4m11s
```


<br>Vamos deletar alguns pods/réplicas para observar o comportamento:<br>
```kubectl delete pod nginx-replicaset-5xrlm nginx-replicaset-68pzw nginx-replicaset-c4w7b```<br><br>


<br>Vamos rodar o get pods novamente:<br>
```kubectl get pods```<br><br>

Antes tínhamos 10 pods com status __Running__.<br>
Deletamos 3 pods/réplica, o Replica Set se encarregou de recriar 3 novos pod/réplicas.<br>
Observe que agora temos 3 replicas com status __ContainerCreating__
   ```shell
NAME                     READY   STATUS              RESTARTS   AGE
nginx-replicaset-6vn54   0/1     ContainerCreating   0          1s
nginx-replicaset-6xtl5   0/1     ContainerCreating   0          2s
nginx-replicaset-k74jr   1/1     Running             0          11m
nginx-replicaset-l49nr   1/1     Running             0          11m
nginx-replicaset-ns744   0/1     ContainerCreating   0          1s
nginx-replicaset-qpwqv   1/1     Running             0          11m
nginx-replicaset-ts7wt   1/1     Running             0          11m
nginx-replicaset-twfhr   1/1     Running             0          11m
nginx-replicaset-v7dmz   1/1     Running             0          71s
nginx-replicaset-xzbs5   1/1     Running             0          11m
```
<br>


