# K8S
Exemplo usando __Kind__ na minha máquina

1) Criar um __cluster__
  Para ver o número de máquinas no cluster, usar o comando:<br>
  cmd __kubectl get nodes__ <br>

2) __kind create cluster__
3) Criar um __Pod__<br>
   Criar um arquivo chamado pod.yaml ( Um pod é o menor objeto do K8, um container runtime)<br>
   Criado, vamos coloca-los para funcionar, com o comando:<br>
   cmd __kubectl apply -f <nome_do_pod.yaml>__<br><br>
   Para listar os pods, usamos o comando:<br>
   cmd __kubectl get pods__<br><br>
   Para deletar, usamos o comando:<br>
   cmd __kubectl delete pod <nome_do_pod>__<br><br>


2) Para criar um __replica Set__<br>
   Replica set é o cara que gerencia os pods no cluster, criando ou apagando pods conforme o número de replicas que setamos.<br>
   Arquivo criado, usamos o comando:<br>
   cmd __kubectl apply -f <nome_do_replicaset.yaml>__<br><br>
   Para listar o replicaset usamos:<br>
   cmd __kubectl get rs__<br><br>

   Um exemplo de como podemos ver/usar esses pods que estão rodando dentro do replicaset.<br>
   Os containers tem portas diferentes das portas dos computadores. Para acessar diretamente um container
   <br>temos de fazer um __port-forward__. Ou seja, apontar a porta do computador para a porta do container.<br><br>
   cmd __kubectl port-forward pod/<nome-pod> <porta-container>:<porta_computador>__ <br><br>

    Um bom exemplo para ver o replicaset em funcionamento é deletar um pod e observar o rs recria-lo<br>
    primeiro vamos listar os pods do replicaset<br>
    cmd __kubectl get pods__, termos essa saida para um rs de 10 pods<br>

nginx-replicaset-459n9   1/1     Running   0          54s
nginx-replicaset-4vdcf   1/1     Running   0          54s
nginx-replicaset-5x75s   1/1     Running   0          54s
nginx-replicaset-75jj8   1/1     Running   0          54s
nginx-replicaset-gbjp8   1/1     Running   0          54s
nginx-replicaset-k6fl2   1/1     Running   0          54s
nginx-replicaset-pjn7n   1/1     Running   0          54s
nginx-replicaset-qfvtm   1/1     Running   0          2m41s
nginx-replicaset-sgfml   1/1     Running   0          54s
nginx-replicaset-tsj4h   1/1     Running   0          54s
  
