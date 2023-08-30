 # estudo_kubernetes

https://kubernetes.io/pt-br/docs/tutorials/kubernetes-basics/explore/explore-intro/

### Para que serve o Kubernetes

<p>O kubernetes resolve o problema de escalabilidade horizontal, dividindo o poder computacional das máquinas e trabalhando em paralelo. O Kubernetes 
é capaz de fazer isso, ele gerencia uma ou múltiplas máquinas trabalhando em conjunto, que nós vamos chamar de cluster. O Kubernetes é capaz de criar 
esse cluster e o gerenciar para nós.</p>
<p>O Kubernetes consegue criar e gerenciar um cluster para que nós consigamos manter a nossa aplicação escalável sempre que nós quisermos adicionar 
novos containers, sempre que nós quisermos reiniciar a nossa aplicação de maneira automática, caso ela tenha falhado. Então nós chamamos isso de 
orquestração de containers.</p>

<img width="686" alt="Screen Shot 2023-07-24 at 7 00 23 PM" src="https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/6a917580-92aa-4268-b9d7-9a3a44e8a6df">

### Como o Kubernetes funciona

<p>O Kubernetes vai gerenciar um cluster, e as máquinas dentro de um cluster recebem denominações diferentes.</p>

<p>Elas podem ser master, onde o master é responsável por coordenar e gerenciar todo o nosso cluster e nós temos os notes que são responsáveis pela 
<p>Execução do trabalho duro, para executar os nossos pods em capsulas containers, por assim dizer</p>
    
<img width="686" alt="Screen Shot 2023-07-24 at 7 31 35 PM" src="https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/24ba9bd1-613b-4ca1-8d83-15feb05138a4">

<img width="686" alt="Screen Shot 2023-07-24 at 7 34 45 PM" src="https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/8ac69a4c-2cb1-477c-9135-678195f9c9f7">

### Quais são os principais componentes da ferramenta

<p>Os resources do kubernetes já têm soluções ali implementadas para determinadas tipos de caso. Então nós temos, por exemplo: pods, ReplicaSets, 
Deployments, Volumes.</p>

<p>Então, por exemplo: se eu quero lidar com a questão de persistência de dados eu posso utilizar um recurso já pronto, que é o Persistent Volume. Então,
se eu quero e devo utilizar e encapsular um container para utilizar no Kubernetes, eu utilizo um pod.</p>

<p>Utilizando esses recursos nós conseguimos construir aplicações bem elaboradas; onde, por exemplo, nós recebemos um tráfego de dados no nosso session,
no nosso serviço e ele consegue fazer o balanceamento de cargas entre os pods que nós temos dentro da nossa aplicação.</p>

<p>Esses pods podem estar sendo gerenciados por um ReplicaSet que pode estar sendo gerenciado por um deployment e pode ser escalado. Nós podemos aumentar
o número de pods, um horizontal pod autoscaler.</p>
 
<img width="686" alt="Screen Shot 2023-07-24 at 7 05 49 PM" src="https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/6a812e0c-e8ba-48c7-aeb6-cee85915524d">

### O que é, e para o que serve a API

<p>A API, além de receber as ordens do mundo externo e do que nós queremos fazer com o nosso cluster, ela é responsável por manter a comunicação com 
Controller Manager, um ETCD, com Scheduler e também os nossos nodes. Então através dela, nós conseguimos criar um pod, editar um ReplicaSet, ler os 
dados no Deployment, deletar um Volume - tudo isso através da API, nós nunca vamos nos comunicar diretamente com os outros componentes; vai ser sempre 
através da API.</p>

![image](https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/1dc36309-0fe9-45f4-b366-9ac396556808)

### O que é, e para o que serve o kubectl

<p>O Kubectl, que nos provê as funcionalidades de criar, ler, atualizar e remover os dados do nosso cluster, os componentes do nosso cluster, os 
nossos recursos.</p>

<p>Então, através do Kubectl nós conseguimos fazer isso de maneira declarativa ou imperativa. Nós podemos criar arquivos de definição, ou executarmos 
comandos, que simplesmente vão fazer essa mágica acontecer.</p>

<p>E tudo isso ainda vai ser enviado um request do nosso Kubectl para a nossa API REST, que vai fazer a mágica acontecer dentro do nosso cluster.</p>

### O que é Nodes

<p>Um nó é a menor unidade de hardware de computação no Kubernetes. É uma representação de uma única máquina no seu cluster.
Na maioria dos sistemas de produção, um nó provavelmente será uma máquina física em um datacenter ou uma máquina virtual hospedada em um provedor 
de nuvem, como o Google Cloud Platform.</p>

### Criando e entendendo pods

#### Entendendo o que são pods

<p>No Docker nós trabalhamos com container. E a partir de agora no Kubernetes nós vamos criar, produzir, manipular e gerir, não mais os containers 
diretamente, e sim os nossos pods. Então o mundo kubernetes, pods, o mundo Docker e containers.</p>

<img width="686" alt="Screen Shot 2023-07-25 at 6 17 39 PM" src="https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/e2a92159-29cd-4dd8-9c14-ab3fbad2c6e0">

<p>Um pod é um conjunto de um ou mais containers, então quando nós tivermos aqui a comunicação da nossa máquina com o kubectl para API, nós não vamos 
pedir pela criação diretamente de um container, e sim de um pod, que pode conter um ou mais containers dentro dele.</p>
<p>Isso sempre de maneira declarativa ou imperativa.</p>

<img width="686" alt="Screen Shot 2023-07-25 at 6 18 57 PM" src="https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/0c6a9576-8b32-4eb0-afc9-d4a23019d350">
<img width="686" alt="Screen Shot 2023-07-25 at 6 19 18 PM" src="https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/33e500de-094d-4ad3-95cd-341e692f7e67">

<p>Dentro de um pod nós temos liberdade, para termos mais containers, mas sempre que nós criamos um pod ele ganha um endereço IP.</p>

<p>Então o endereço IP não é mais do container, e sim do nosso pod. Dentro do nosso pod nós temos total liberdade de fazermos um mapeamento de 
portas para os IPs que são atribuídos a esse pod.</p>

<p>No momento em que nós fazemos a requisição aqui, por exemplo, para o IP 10.0.0.1, repare que é o mesmo IP que nós estamos a fazer requisição 
para o IP do pod na porta 8080. Nós estamos nos referindo nesse momento ao nosso container dentro da porta :8080 no nosso pod.</p>

<img width="686" alt="Screen Shot 2023-07-25 at 6 20 29 PM" src="https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/686622a8-4ff2-4b0a-8203-5523b4c48905">

<p>Nós vimos que nós temos um container ou mais dentro de um pod. Caso esse container falhe, o que vai acontecer?</p>

<p>Nesse momento, esse pod vai parar de funcionar. Ele morreu para sempre e o kubernetes tem total liberdade de criar um pod para substituir 
o antigo, mas não necessariamente com o mesmo IP que ele tinha antes, nós não temos controle sobre isso.</p>

<img width="686" alt="Screen Shot 2023-07-25 at 6 22 36 PM" src="https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/dbd66a37-b7b1-43f7-93e8-413709b65e47">

<p>Por quê? Porque os pods são efémeros, eles estão ali para serem substituídos a qualquer momento e toda criação de um novo pod é um novo pod 
efetivamente, não é o mesmo pod antigo renascido.</p>

<img width="686" alt="Screen Shot 2023-08-02 at 6 30 17 PM" src="https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/64488144-57b0-46ce-aab5-94d6bfa0a0c7">

<p>E caso nós tivéssemos mais de um container no mesmo pod, o que iria acontecer se esse pod falhasse? Para ele falhar efetivamente nós 
teríamos que ter a seguinte condição:</p>

<p>O primeiro container falhou dentro de um pod. Caso ainda tenha algum container em funcionamento sem nenhum problema dentro desse mesmo pod, 
ele ainda está saudável; mas caso nenhum container mais esteja a funcionar dentro desse pod, esse pod foi finalizado e outro vai ser criado no lugar dele.</p>

<img width="686" alt="Screen Shot 2023-07-25 at 6 22 52 PM" src="https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/87a5873d-565c-4f64-a1a1-98b52ddafc80">

<p>O IP pertence ao pod, e não aos containers. Isso quer dizer que no fim das contas, eles vão compartilhar os mesmos namespaces de rede e de processo, 
de comunicação entre o processo e eles também podem compartilhar volume.</p>

<img width="686" alt="Screen Shot 2023-07-25 at 6 24 22 PM" src="https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/d7cb7f16-cb6f-4a0b-854b-68ed58758873">

<p>Qual é a grande vantagem deles compartilharem o mesmo IP? A grande vantagem é que agora eles podem fazer essa comunicação diretamente entre eles 
via localhost, porque eles têm o mesmo IP, sendo 10.0.0.1, nesse caso.</p>

<p>Então, agora nós temos essa capacidade de fazer uma comunicação de maneira muito mais fácil entre containers de um mesmo pod e isso, é claro, 
nós também vamos ter total capacidade de comunicar pods entre diferentes IPs. Eu tenho um pod com IP 10.0.0.1, ele pode começar com pod de IP 10.0.0.2. 
Por exemplo:</p>

<img width="686" alt="Screen Shot 2023-07-25 at 6 24 45 PM" src="https://github.com/DyaneAraujo/estudo_kubernetes/assets/114944655/2badf158-8c4e-4edc-981b-01dc59409a95">


### Criando cluster

<p>Ambiente virtualizado com cluster com driver do docker ou virtualbox</p>

```shell
sudo install minikube

minikube start --vm-driver=docker

minikube start --vm-driver=virtualbox
```

* Para rodar o novo cluster após criado 

```shell
minikube start
```

* Comando para consultar os nodes

```shell
~ % kubectl get nodes                
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   8d    v1.27.3
```

### Criando pod - interativa

* Comando para criar um pod com a image nginx versão latest

```shell
kubectl run nginx-pod --image=nginx:latest
```

* Comando para consultar os pods

```shell
kubectl get pods
```

* Para acompanhar a criação do pod em tempo real

```shell
kubectl get pods --watch
```

* Comando para exibir detalhes sobre o pod, como inicialização, IP, porta, container, versão, labels, etc.

```shell
kubectl describe pod nginx-pod
```

<p>O pod é somente criado após a inicialização do container.</p>

* Comando para editar um pod

kubectl edit pod nginx-pod

<p>Após dar enter no comando, apertar a tecla <b>i</b> para entrar no modo <b>INSERT</b>, após editar o arquivo aperta a tecla <b>ESC</b>
e escrever <b>:wq</b> para salvar e sair do modo vim.</p>

### Criando pod - declarativa

<p>Criar um arquivo yaml com as específicações básicas para criar um pod.</p>

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: first-pod-declarative
spec:
    containers:
      - name: nginx-container
        image: nginx:latest
```

<p>Após criar o arquivo, no diretório raiz, usar o comando a seguir para aplicar as configurações e rodar o pod. O <b>-f</b> significa file.</p>


```shell
kubectl apply -f ./arquivo-pod.yaml
```

<p>Nós centralizamos diversas dessas ações de inicialização do pod, como se comunicar com a API, através desse único comando kubectl apply, ou seja, 
o kubectl foi responsável por fazer a comunicação com a API.</p>

<p>Conseguimos criar, gerenciar e manipular recursos por um único comando de uma maneira que é bem mais usada em produção e 
tendo um registro de como está o nosso estado atual.</p>

### Iniciando o projeto

* Como deletar um pod

````shell
kubectl get pods
kubectl delete pod nginx-pod
````

* Como deletar um pod criado de maneira declarativa, existem duas formas
* O nome do arquivo é o mesmo que está escrito no campo name do metadata do arquivo yaml


```shell
kubectl delete -f .\arquivo-pod.yaml
kubectl delete pod news-portal

```

-f significa file/arquivo

* Crie um arquivo yaml **news-portal.yaml**

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: news-portal
spec:
    containers:
      - name: news-portal-container
        image: aluracursos/portal-noticias:1
```

* Depois aplice as configurações com seguinte comando

````shell
kubectl apply -f .\news-portal.yaml
````

* Para acompanhar a criação do pod

````shell
kubectl get pods --watch
````

* Para consultar o IP do pod

````shell
kubectl describe pod news-portal
````

<p>Exemplo de <b>IP: 10.244.0.13</b></p>
<p>Copia o IP e teste acessar pelo navegador, vai ver que não é possível.</p>

* Executar o container de maneira interativa
* O comando irá permitir acessar o terminal de dentro do container

```shell
kubectl exec -it news-portal -- bash
```

* Tentando acessar o localhost pelo terminal do container

```shell
curl localhost
```

<p>O comando irá exibir todo o conteúdo html da página que era esperado ser exibido no navegador.</p>

* Para sair do terminal do container digite **exit**


<p>Esse IP disponibilizado só serve para acessar dentro do cluster, somente as aplicações dentro do cluster, 
irão conseguir se comunicar, através deste pod com este IP.</p>

<p>E não fizemos nenhum tipo de mapeamento para deixar o IP acessível fora do cluster.</p>

### Conhecendo os services

* Todos os pods se comunicam através dos seus respectivos IPs, no mesmo cluster.
* Se caso um dos pods pare de funcionar, o mesmo será substituído por um novo com outro IP.

<p>Não temos controle sobre a criação dos IPs dos pods, eles são gerados automáticamente</p>

<img width="508" alt="Screenshot 2023-08-20 at 9 59 47 AM" src="https://github.com/MulherMarav/estudo_kubernetes/assets/101612046/9994eb0e-158c-41b6-b57e-2fd9f595828a">

<img width="682" alt="Screenshot 2023-08-20 at 10 00 31 AM" src="https://github.com/MulherMarav/estudo_kubernetes/assets/101612046/6459f94f-4d0b-414f-877a-3729298b2159">

* Comando para exibir os pods formatado, de maneira wide que a saída/output, irá exibir o IP do pod, como: 10.1.0.9

```shell
kubectl get pods -o wide
```

<p>Como os demais pods do mesmo cluster sabe qual é o IP do novo pod que eles devem se comunicar quando este pod for gerado novamente pela API?</p>

<p>Eles conseguem se comunicar por um recurso do Kubernetes chamado Service/SVC.</p>

<img width="833" alt="Screenshot 2023-08-20 at 10 01 13 AM" src="https://github.com/MulherMarav/estudo_kubernetes/assets/101612046/234caadf-df69-40d8-80b6-456ff770893c">

<p>Cada pod prover de um IP fixo, imutável. É por este IP que os outros pods se comunicam com ele.</p>
<p>Os serviços sempre vão possuir IPs fixos que nunca vão mudar. Os serviços provem de um DNS para se comunicar com um ou mais pods.</p>

<p>Os pods nunca vão se comunicar diretamente com os outros pods, sempre será através do serviço, o serviço irá possuir um IP fixo e um DNS.</p>
<p>Os serviços também faz balanceamento de carga entre os pods.</p>

<img width="760" alt="Screenshot 2023-08-20 at 10 01 59 AM" src="https://github.com/MulherMarav/estudo_kubernetes/assets/101612046/602616af-fc29-4be6-a286-3d0aea4767a3">

* Os serviços possuem esses três tipos:

<img width="542" alt="Screenshot 2023-08-20 at 10 02 36 AM" src="https://github.com/MulherMarav/estudo_kubernetes/assets/101612046/a287d1d7-0d8c-4263-b095-81b53329d1da">

### Criando um serviço ClusterIP

<p>Este tipo de serviço permite fazer a comunicação entre diferentes pods dentro de um mesmo cluster.</p>

<p>Nesse cenário que nós estamos visualizando, todo e qualquer pod. Esse de final .2, .4 e .3 eles vão conseguir fazer a comunicação para este pod de final .1 a partir desse serviço, 
utilizando o IP e o DNS desse serviço.</p>

<img width="903" alt="Screenshot 2023-08-20 at 10 03 50 AM" src="https://github.com/MulherMarav/estudo_kubernetes/assets/101612046/1b2ce4a9-41ef-4e4b-9021-9f387a9fe201">


<p>O pod com o service não consegue se comunicar com os outros pods, por conta que os outros pods não possuem serviços atrelados a eles.</p>
<p>Não é possível acessar esse pod fora do ClusterIP, por conta que a comunicação é apenas interna entre os pods pelo ClusterIP.</p>

<img width="908" alt="Screenshot 2023-08-20 at 10 04 30 AM" src="https://github.com/MulherMarav/estudo_kubernetes/assets/101612046/969adefd-9e92-4094-8194-69a63f9be2ff">

#### ClusterIP na prática

* Criar dois pods atrelados ao tipo de serviço ClusterIP
* Por boas práticas, devemos definir a porta do pod
* Os dois podem ter a mesma porta 8080, por conta que cada um tem seus respectivos IP.

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: pod-1
spec:
    containers:
        - name: container-pod-1
          image: nginx:latest
          ports:
            - containerPort: 80
```

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: pod-2
spec:
    containers:
        - name: container-pod-2
          image: nginx:latest
          ports:
            - containerPort: 80
```

* Comando para criar os dois pods


```shell
kubectl apply -f .\pod-1.yaml
kubectl apply -f .\pod-2.yaml
```

<p>Em nosso Cluster temos os seguintes pods criados, mas ainda está faltando criarmos o serviço para o pod-2.</p>

* Crie um arquivo de configuração chamado **svc-pod-2.yaml**

```yaml
apiVersion: v1
kind: Service
metadata:
  name: svc-pod-2
spec:
  type: ClusterIP
```

### Labels 

<p>As labels permitem definir que o serviço irá se comunicar apenas com os pods que tem suas respectivas labels</p>

<img width="875" alt="Screenshot 2023-08-20 at 10 08 45 AM" src="https://github.com/MulherMarav/estudo_kubernetes/assets/101612046/826d7a4f-60ed-4285-b80f-96b72db0c8e9">


<p>Podemos colocar quantas labels quisermos, com qualquer nome.</p>

```yaml
apiVersion: v1
kind: Pod
metadata:
    name: pod-2
    labels:
        app: segundo-pod
spec:
    containers:
        - name: container-pod-2
          image: nginx:latest
    ports:
        - containerPort: 80
```
<p>Na configuração do serviço, devemos informar o nome da label que o serviço deve monitorar, em todas as requisições que ele receber, deve encaminhar para o <b>segundo-pod</b>.</p>

<p>Além disso, precisa mapear para qual porta iremos receber as requisições e para qual porta iremos encaminhar para o pod.</p>

* Iremos receber e encaminhar as requisições pela porta 80, de qualquer pod que tenha label **segundo-pod**.

````yaml
apiVersion: v1
kind: Service
metadata:
    name: svc-pod-2
spec:
    type: ClusterIP
    selector:
        app: segundo-pod
    ports:
    - port: 80
````

* Após definir as configurações do service, devemos atualizar o pod:

````shell
kubectl apply -f .\pod-2.yaml
````

* E depois criar o serviço

````shell
kubectl apply -f .\svc-pod-2.yaml
````

* Para consultar os serviços

````shell
kubectl get service
kubectl get svc
````

* Comando para executar o terminal do **news-portal**

````shell
kubectl exec -it news-portal -- bash
````

* Dentro do terminal do pod-1, executar um curl/uma requisição para o pod-2
* Com IP do pod-2 e a porta 80

````shell
root@pod-1:/var/www/html# curl 10.244.0.15:80
````

* Se deletarmos o pod-2, o serviço irá permanecer em execução

````shell
kubectl delete -f .\pod-2.yaml
````

* O serviço irá continuar ouvindo na porta 80, se eu fizer um curl/requisição novamente, ele irá ouvir, porém, não irá despachar para nenhum pod, porque não tem nenhum pod _"em pé"_.

````shell
kubectl get svc
````

<p>Por conta do serviço possuir um DNS e IP fixo, além das labels, mesmo que o IP do pod mude, após recria-lo, isso não irá interferir nas requisições
para os pods devidamente configurados.</p>

<p>Se fizermos a requisição via DNS ao invés do IP, também irá funcionar a requisição para o <b>pod-2</b>.</p>

* Se quisermos que o nosso serviço escute em uma porta, mas encaminhe/despache para outra porta que está configurado o pod, usamos a configuração **targetPort**:

```yaml
apiVersion: v1
kind: Service
metadata:
    name: svc-pod-2
spec:
    type: ClusterIP
    selector:
      app: segundo-pod
    ports:
        - port: 9000
          targetPort: 80
```

<p>Após aplicar as novas configurações do pod-2 e do service, devemos usar a porta <b>900</b> para fazer um curl para o serviço.</p>

````shell
root@pod-1:/var/www/html# curl 10.108.136.109:9000
````

10.244.0.15:80 -> Comunicação através do pod, é instável.
10.108.136.109:9000 -> Comunicação através do serviço, é estável.

<p>O serviço irá fazer o bound para o pod no 10.244.0.15:80</p>

### Criando um serviço NodePort

<p>Esse tipo de serviço permite a comunicação externa, para fora do cluster.</p>

![Screenshot 2023-08-20 at 10.19.17 AM.png](img%2FScreenshot%202023-08-20%20at%2010.19.17%20AM.png)

<p>Então, por exemplo, conseguimos acessar um pod que está dentro do nosso cluster, pelo navegador.</p>

<p>O serviço <b>NodePort</b> também é um <b>ClusterIP</b>, então conseguimos se comunicar com o pod internamente pelo serviço e também conseguimos se comunicar externamente pelo serviço.</p>

![Screenshot 2023-08-20 at 10.21.32 AM.png](img%2FScreenshot%202023-08-20%20at%2010.21.32%20AM.png)

* Crie um novo serviço para pod-1 do tipo NodePort

````yaml
apiVersion: v1
kind: Service
metadata:
    name: svc-pod-1
spec:
    type: NodePort
    ports:
        - port: 80
          #targetPort: 80
    selector:
      app: primeiro-pod
````

![Screenshot 2023-08-20 at 10.26.10 AM.png](img%2FScreenshot%202023-08-20%20at%2010.26.10%20AM.png)


* Aplique as mudanças do arquivo de configuração para criar um novo serviço do tipo **NodePort**


````shell
kubectl apply -f .\svc-pod-1.yaml
````

````yaml
apiVersion: v1
kind: Pod
metadata:
    name: pod-1
    labels:
        app: primeiro-pod
spec:
    containers:
        - name: container-pod-1
          image: nginx:latest
          ports:
            - containerPort: 80
````

* Depois aplique as mudanças do pod-1


````shell
kubectl apply -f .\pod-1.yaml
````

````shell

~ % kubectl get pods -o wide
NAME          READY   STATUS    RESTARTS      AGE   IP            NODE       NOMINATED NODE   READINESS GATES
news-portal   1/1     Running   1 (17h ago)   27h   10.244.0.19   minikube   <none>           <none>
nginx-pod     1/1     Running   4 (17h ago)   25d   10.244.0.17   minikube   <none>           <none>
pod-1         1/1     Running   1 (17h ago)   23h   10.244.0.18   minikube   <none>           <none>
pod-2         1/1     Running   1 (17h ago)   23h   10.244.0.20   minikube   <none>           <none>
````

#### Fazer acesso ao pod dentro do Cluster pelo ClusterIP

* Consulte os serviços 

````shell
kubectl get svc
````

````shell
~ % kubectl get svc
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP        26d
svc-pod-1    NodePort    10.97.146.102    <none>        80:30363/TCP   6s
svc-pod-2    ClusterIP   10.108.136.109   <none>        9000/TCP       17h
````

<p>É possível ver que foi feito um bound da porta 80 para porta 30363 do serviço <b>svc-pod-1</b></p>

* Execute o terminal do **news-portal** e tente acessar o pod pelo IP e pela porta do serviço **svc-pod-1**

````shell
kubectl exec -it news-portal -- bash
````

* Faça um **curl** pelo terminal do **news-portal**

````shell
root@news-portal:/var/www/html# curl 10.97.146.102:80
````

<p>O Serviço possui dois IPs, um para comunicação interna pelo <b>clusterIP</b> e outro para comunicação external pelo <b>externalIP</b>.</p>

<p>O IP externo tem que ser a partir do nó, porque é um node cluster ou node port.</p>

* Use o comando a seguir para ver os nodes, de modo wide para ver os IPs

````shell
kubectl get nodes -o wide
````

````shell
~ % kubectl get nodes -o wide
NAME       STATUS   ROLES           AGE   VERSION   INTERNAL-IP    EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION   CONTAINER-RUNTIME
minikube   Ready    control-plane   26d   v1.27.3   192.168.49.2   <none>        Ubuntu 22.04.2 LTS   6.1.32-0-virt    docker://24.0.4
````

<p>O Docker Desktop no Windows ele faz um bound automaticamente do Docker Desktop para o nosso LocalHost, então o IP desse nó no Windows 
vai ser LocalHost.</p>

<p>Se acessarmos, iremos ver que o windows está rodando alguma coisa na porta 80, mas não é nosso pod: </p> 

`localhost:80`

<p>O que nós queremos acessar é a página do Nginx.</p>

<p>Como vimos, a API fez um bound do serviço para a porta <b>30363</b>, então se acessarmos o LocalHost com está porta, teremos acesso ao Html do Nginx</p>

`localhost:30363`

<p>Porém, essa porta é gerada de forma arbitrária, ela vai variar de 30000 até 32767.</p>

#### Como definir a porta externa do NodePort

<p>Onde nós podemos definir qualquer valor de porta no intervalo de 30000 até 32767</p>

````yaml
apiVersion: v1
kind: Service
metadata:
    name: svc-pod-1
spec:
    type: NodePort
    ports:
        - port: 80
          #targetPort: 80
          nodePort: 30000
    selector:
        app: primeiro-pod
````

* Após definir a porta externa e aplicar as mudanças

````shell
kubectl apply -f .\svc-pod-1.yaml
````

* Ao consultar os serviços, iremos ver que a porta mudou para **30000**

````shell
kubectl get svc
````

````shell
~ % kubectl get svc
NAME         TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kubernetes   ClusterIP   10.96.0.1        <none>        443/TCP        26d
svc-pod-1    NodePort    10.97.146.102    <none>        80:30000/TCP   7m39s
svc-pod-2    ClusterIP   10.108.136.109   <none>        9000/TCP       18h
````

<p>Agora é possível acessar o pod-2 pela porta 30000</p>

`localhost:30000`

#### Linux

<p>No Linux ele não faz o bound automaticamente para LocalHost, então após consultar os nodes com wide, no linux, 
pegamos o IP internal do node e utilizamos ele pra acessar de forma externa.</p>

````shell
kubectl get nodes -o wide
````

````shell
~ % kubectl get nodes -o wide
NAME       STATUS   ROLES           AGE   VERSION   INTERNAL-IP    EXTERNAL-IP   OS-IMAGE             KERNEL-VERSION   CONTAINER-RUNTIME
minikube   Ready    control-plane   26d   v1.27.3   192.168.49.2   <none>        Ubuntu 22.04.2 LTS   6.1.32-0-virt    docker://24.0.4
````

`http://192.168.49.2:30000/`

<p>Então LocalHost não vai funcionar no Linux, nós temos que usar o internal IP no Linux. Enquanto no Windows, todo o acesso vai ser via LocalHost porque ele vai bind direto. 
A única diferença vai ser essa, o comportamento do resto todo é o mesmo.</p>

#### MacOs

<p>No caso do Windows, o Docker Desktop faz um bind automaticamente do Docker para o localhost, então você pode acessar o serviço utilizando o localhost na 
porta especificada pelo NodePort. Já no macOS, você precisa descobrir o IP interno do seu nó e utilizar esse IP para acessar o serviço na porta especificada pelo NodePort.</p>

<p>No exemplo da aula, foi utilizado o comando <b>kubectl get nodes -o wide</b> para obter o IP interno do nó. No caso do macOS, você pode tentar utilizar o 
comando <b>docker-machine ip default</b> para obter o IP do seu nó.</p>

<p>Por exemplo, se o IP do seu nó for 192.168.99.106 e o NodePort definido para o serviço for 30000, você pode acessar a aplicação no navegador 
utilizando o IP do nó e a porta 30000, da seguinte forma: <b>192.168.99.106:30000</b>.</p>

* Duas formas de descobrir o IP do nó minikube

````shell
docker inspect minikube
kubectl describe node minikube
kubectl get nodes -o wide
````

````shell
Addresses:
  InternalIP:  192.168.49.2
````

### Criando um serviço Load Balancer

<p>O LoadBalancer nada mais é do que um ClusterIP que permite a comunicação entre uma mna do mundo externo e os nosso pods. 
Só que ele automaticamente se integra ao LoadBalancerdo nosso cloud provider.</p>

<p>Então quando nós criamos um LoadBalancer ele vai utilizar automaticamente, sem nenhum esforço manual, o cloud provider da 
AWS ou do Google Cloud Platform, ou da Azure, e assim por diante.</p>

![Screenshot 2023-08-20 at 1.22.42 PM.png](img%2FScreenshot%202023-08-20%20at%201.22.42%20PM.png)

* Então no Google Cloud Platform, após criarmos o nosso Cluster-1

![Screenshot 2023-08-20 at 1.26.43 PM.png](img%2FScreenshot%202023-08-20%20at%201.26.43%20PM.png)

* No terminal do provider o **cloudshell** iremos digitar o seguindo comando pra criar o **pod-1**

````shell
cat > pod-1.yaml

apiVersion: v1
kind: Pod
metadata:
  name: pod-1
  labels:
    app: primeiro-pod
spec:
    containers:
        - name: container-pod-1
          image: nginx:latest
    ports:
        - containerPort: 80
````

* E depois aplique as modificações pelo mesmo terminal do **cloudshell**

````shell
kubectl apply -f pod-1.yaml
````

* Agora, crie um serviço do tipo Load Balancer chamado svc-pod-1-loadbalancer

````yaml
apiVersion: v1
kind: Service
metadata:
  name: svc-pod-1-loadbalancer
spec:
    type: LoadBalancer
    ports:
        - port: 80
          nodePort: 30000
    selector:
        app: primeiro-pod
````

* No terminal do **Google Cloud Platform**, no **cloudshell**, digite o comando a seguir para aplicar as modificações

````shell
cat > lb.yaml

apiVersion: v1
kind: Service
metadata:
name: svc-pod-1-loadbalancer
spec:
type: LoadBalancer
ports:
- port: 80
nodePort: 30000
selector:
app: primeiro-pod
````

* No mesmo terminal choudshell


````shell
kubectl apply -f lb.yaml
````

* Na aba **Serviços e Entradas** da plataforma **Google Cloud Platform**, podemos ver o svc-pod-1-loadbalancer em execução, criando os endpoints para acesso

![Screenshot 2023-08-20 at 1.40.24 PM.png](img%2FScreenshot%202023-08-20%20at%201.40.24%20PM.png)

* E depois, basta clicarmos no link que foi gerado o do IP, para acessarmos o pod-1 pelo serviço svc-pod-1-loadbalancer

http://35.247.212.255

- Sobre os Load Balancer: 

    - Utilizam automaticamente os balanceadores de carga de cloud providers.

    - Por serem um Load Balancer, também são um NodePort e ClusterIP ao mesmo tempo.

### Deletar todos services/pods

````sh
kubectl delete pods --all
kubectl delete svc --all
````

### Continuando o projeto

#### Aplicando service ao projeto

* Criar um arquivo para o service do tipo NodePort

````yaml
apiVersion: v1
kind: Service
metadata:
  name: svc-news-portal
spec:
  type: NodePort
  ports:
    - port: 80
      nodePort: 30000
  selector:
    app: news-portal
````

* Colocar a label e a porta no pod da aplicação 

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: news-portal
  labels:
    app: news-portal
spec:
  containers:
    - name: news-portal-container
      image: aluracursos/portal-noticias:1
      ports:
      - containerPort: 80
````

* Aplicar as mudanças dos dois yamls

````sh
kubectl apply -f .\news-portal.yaml
````

````sh
kubectl apply -f .\svc-news-portal.yaml
````

#### Subindo o sistema de notícias

<p>Iremos criar um serviço e um pod responsáveis no caso pelo sistema de notícias onde 
será cadastrado. Esse sistema também vai prover para o nosso portal essas notícias para que nós possamos exibir.</p>

<p>Então, como nós queremos acesso do mundo externo ao nosso pod do sistema de notícias e também ao mundo interno do 
nosso cluster, para que o nosso portal consiga consumir essas notícias, nós precisamos criar um NodePort e um pod no caso - obviamente com a imagem do nosso sistema.</p>

![Screenshot 2023-08-28 at 7.58.07 AM.png](img%2FScreenshot%202023-08-28%20at%207.58.07%20AM.png)

* Crie o novo pod 

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: news-system
  labels:
    app: news-system
spec:
  containers:
    - name: news-system-container
      image: aluracursos/sistema-noticias:1
      ports:
        - containerPort: 80
````

* Crie o novo serviço 

````yaml
apiVersion: v1
kind: Service
metadata:
  name: svc-news-system
spec:
  type: NodePort
  ports:
    - port: 80
      nodePort: 30001
  selector:
    app: news-system
````

* Aplique as alterações

````sh
kubectl apply -f .\news-system.yaml
````

````sh
kubectl apply -f .\svc-news-system.yaml
````

#### Subindo o banco de dados

<p>Queremos comunicação apenas dentro do cluster. Nós não queremos que o nosso banco seja acessível para o mundo externo, 
nós podemos criar um *ClusterIP” para ele.</p>

![Screenshot 2023-08-28 at 8.17.02 AM.png](img%2FScreenshot%202023-08-28%20at%208.17.02%20AM.png)

* Crie o novo pod

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: news-db
  labels:
    app: news-db
spec:
  containers:
    - name: news-db-container
      image: aluracursos/mysql-db:1
      ports:
        - containerPort: 3306
````

* Crie o novo serviço

````yaml
apiVersion: v1
kind: Service
metadata:
  name: svc-news-db
spec:
  type: ClusterIP
  ports:
    - port: 3306
  selector:
    app: news-db
````

* Aplique as alterações

````sh
kubectl apply -f .\news-db.yaml
````

````sh
kubectl apply -f .\svc-news-db.yaml
````

* Consultado os pods e serviços 

````sh
~ % kubectl get svc                     
NAME              TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kubernetes        ClusterIP   10.96.0.1        <none>        443/TCP        6m20s
svc-news-db       ClusterIP   10.104.13.2      <none>        3306/TCP       117s
svc-news-portal   NodePort    10.101.187.230   <none>        80:30000/TCP   117s
svc-news-system   NodePort    10.103.79.65     <none>        80:30001/TCP   117s
~ % kubectl get pods
NAME          READY   STATUS             RESTARTS      AGE
news-db       0/1     CrashLoopBackOff   4 (12s ago)   2m32s
news-portal   1/1     Running            0             2m32s
news-system   1/1     Running            0             2m32s
````

<p>O pod do news-db está com algum erro, e ao consultar o <b>kubectl describe pods news-db</b></p>
<p>Podemos ver os logs e que ocorreu um erro ao tentar inicializar a aplicação, por conta que não definimos as variáveis 
de ambiente do banco de dados.</p>

### Aplicar para todos os arquivos

* Para aplicar as mudanças para todos os arquivos dentro do diretório **project**

````sh
kubectl apply -f project --recursive
kubectl apply -f project --r
````

### Variáveis de Ambiente

* Iremos primeiro deletar o pod

````sh
kubectl delete pod news-db
````

* Adicionar as envs dentro do yaml do pod

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: news-db
  labels:
    app: news-db
spec:
  containers:
    - name: news-db-container
      image: aluracursos/mysql-db:1
      ports:
        - containerPort: 3306
      env:
        - name: "MYSQL_ROOT_PASSWORD"
          value: "q1w2e3r4"
        - name: "MYSQL_DATABASE"
          value: "empresa"
        - name: "MYSQL_PASSWORD"
          value: "q1w2e3r4"
````

* Iremos recriar o pod, aplicando as alterações

````sh
kubectl apply -f .\news-db.yaml
````

* Execute o pod no modo interativo para sabermos se está funcionando
* E acessar o banco de dados diretamente dentro dele

````sh
kubectl exec -it news-db -- bash
````

* Execute o MySql com a senha **q1w2e3r4**

````sh
root@news-db:/# mysql -u root -p
````

* Para consultar as databases do MySql

````sh
mysql> show databases;

+--------------------+
| Database           |
+--------------------+
| information_schema |
| empresa            |
| mysql              |
| performance_schema |
+--------------------+
4 rows in set (0.00 sec)
````

* Para acessar uma database
````sh
mysql> use empresa;
Reading table information for completion of table and column names
You can turn off this feature to get a quicker startup with -A

Database changed
````

* Para consultar as tabelas da database empresa

````sh
mysql> show tables;
+-------------------+
| Tables_in_empresa |
+-------------------+
| noticias          |
| usuario           |
+-------------------+
2 rows in set (0.00 sec)
````

* Fazer uma consulta da tabela **usuario**

````sh
select * from usuario;
+-----------+-------+-------+
| idusuario | login | senha |
+-----------+-------+-------+
|         1 | admin | admin |
+-----------+-------+-------+
1 row in set (0.00 sec)
````

<p>O sistema de notícias ainda não sabe qual é o pod do banco de dados, eles ainda não estão vinculados.</p>

* Se acessarmos o sistema 

````sh
kubectl exec -it news-system -- bash
````

*  E dar um **ls**, iremos ver que ele possui um arquivo _**bancodedados.php**_

````sh
root@news-system:/var/www/html# ls
Dockerfile    bancodedados.php    excluir.php  index.php             noticias.php    php.ini              php.ini-production  theme       uploadClass.php
arquivos.php  docker-compose.yml  funcoes.php  inserir_noticias.php  notificacao.sh  php.ini-development  sair.php            upload.php  uploads
````

* Olhando dentro do arquivo _**bancodedados.php**_

````sh
root@news-system:/var/www/html# cat bancodedados.php
<?php
$host = getenv("HOST_DB");
$usuario = getenv("USER_DB");
$senha = getenv("PASS_DB");
$banco = getenv("DATABASE_DB");
?>
````

<p>Dando uma olhada dentro desses arquivos nós percebemos que precisamos também definir outras variáveis de ambiente 
para esse pod.</p>

<p>Estamos misturando variáveis de configuração, trechos de configuração com o nosso conteúdo de imagem no pod <b>news-bd</b>.
Nós estamos deixando tudo muito acoplado. Seria interessante se nós separássemos isso para mantermos as responsabilidades.</p>

### Config Map

<p>O Kubernetes vai muito além de ser um simples orquestrador de containers e ele já nos provê diversas soluções nativas para diversos problemas.</p>

<p>Nós temos a solução chamada ConfigMap, onde ele vai ser responsável por armazenar essas configurações que foram 
utilizadas dentro de determinados pods.</p>

<p>Nós podemos guardar dentro deles para não acoplarmos o nosso recurso com informações de configuração, por isso um ConfigMap.</p>

<p>Conseguimos reutilizar configurações definidas dentro de ConfigMaps em diferentes pods. Nós podemos ter pods utilizando 
diferentes ConfigMaps.</p>

<p>Então isso nos dá um poder de desacoplamento muito grande e de reutilização também.</p>

![Screenshot 2023-08-30 at 7.50.18 AM.png](img%2FScreenshot%202023-08-30%20at%207.50.18%20AM.png)

![Screenshot 2023-08-30 at 7.47.26 AM.png](img%2FScreenshot%202023-08-30%20at%207.47.26%20AM.png)

![Screenshot 2023-08-30 at 7.49.04 AM.png](img%2FScreenshot%202023-08-30%20at%207.49.04%20AM.png)

#### Criando um ConfigMap

* Cria um arquivo de configuração chamado **db-configmap.yaml**

````yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: db-configmap
data:
  MYSQL_ROOT_PASSWORD: q1w2e3r4
  MYSQL_DATABASE: empresa
  MYSQL_PASSWORD: q1w2e3r4
````

* Remova as **_envs_** do arquivo pod **news-db**

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: news-db
  labels:
    app: news-db
spec:
  containers:
    - name: news-db-container
      image: aluracursos/mysql-db:1
      ports:
        - containerPort: 3306
````

* Aplique as configurações do **configmap**

````sh
kubectl apply -f .\db-configmap.yaml
````

#### Como consultar os ConfigMap

* Para consultar o configmap

````sh
kubectl get configmap
````

* Para descrever o configmap

````sh
kubectl describe configmap db-configmap
````

### Aplicando ConfigMap no projeto

* Para aplicar as chaves uma por uma

````yaml
env:
  - name: MYSQL_ROOT_PASSWORD
    valueFrom:
      configMapKeyRef:
        name: db-configmap
        key: MYSQL_ROOT_PASSWORD
````

* Para aplicar todas as chaves de uma vez

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: news-db
  labels:
    app: news-db
spec:
  containers:
    - name: news-db-container
      image: aluracursos/mysql-db:1
      ports:
        - containerPort: 3306
      envFrom:
        - configMapRef:
            name: db-configmap
````

* Delete o pod **news-db.yaml**

````shell
kubectl delete pod news-db
````

* Aplique as novas declarações no pod

````shell
kubectl apply -f .\news-db.yaml
````

* Consulte os pods

````shell
kubectl get pods

project % kubectl get pods
NAME          READY   STATUS    RESTARTS      AGE
news-db       1/1     Running   0             41s
news-portal   1/1     Running   1 (25h ago)   47h
news-system   1/1     Running   1 (25h ago)   47h
````

* Acesse o terminal do pod **news-db**, e consulte os databases

````shell
kubectl exec -it news-db -- bash
root@news-db:/# mysql -u root -p

mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| empresa            |
| mysql              |
| performance_schema |
+--------------------+
4 rows in set (0.00 sec)
````

* Digite **_exit_** para sair

### Vinculando o banco de dados ao news-system

* Entre no modo interativo do pod **news-system**, ao usar o comando cat, 
* Iremos visualizar o que tem dentro do arquivo **_bancodedados.php_**

````shell
project % kubectl exec -it news-system -- bash

root@news-system:/var/www/html# ls
Dockerfile    bancodedados.php    excluir.php  index.php             noticias.php    php.ini              php.ini-production  theme       uploadClass.php
arquivos.php  docker-compose.yml  funcoes.php  inserir_noticias.php  notificacao.sh  php.ini-development  sair.php            upload.php  uploads

root@news-system:/var/www/html# cat bancodedados.php
<?php
$host = getenv("HOST_DB");
$usuario = getenv("USER_DB");
$senha = getenv("PASS_DB");
$banco = getenv("DATABASE_DB");
?>
````

* Precisamos declarar as variáveis **HOST_DB**, **USER_DB**, **PASS_DB** e **DATABASE_DB**

* Para isso, crie um **ConfigMap** para o pod **news-system**

````yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: system-configmap
data:
  HOST_DB: svc-news-db:3306 #usando DNS para se referênciar ao pod db
  USER_DB: root
  PASS_DB: q1w2e3r4
  DATABASE_DB: empresa
````

* Aplique as configurações do **_system-configmap_**

````sh
kubectl apply -f .\system-configmap.yaml
````

* Coloca a referência ao **configmap** no pod do **news-system**

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: news-system
  labels:
    app: news-system
spec:
  containers:
    - name: news-system-container
      image: aluracursos/sistema-noticias:1
      ports:
        - containerPort: 80
      envFrom:
        - configMapRef:
            name: system-configmap
````

* Delete o pod **news-system.yaml**

````shell
kubectl delete pod news-system
````

* Aplique as novas declarações no pod

````shell
kubectl apply -f .\news-system.yaml
````

* O **news-portal** precisa saber qual é o IP do **news-system**, ao consultarmos o arquivo **_configuracao.php_**

* Notamos que precisamos definir a variável **_IP_SISTEMA_**

```shell
project % kubectl exec -it news-portal -- bash

root@news-portal:/var/www/html# ls
configuracao.php  content.html  docker-compose.yml  index.php  theme

root@news-portal:/var/www/html# cat configuracao.php
<?php
$urlnoticias = getenv("IP_SISTEMA");
?>
```

* Crie um **ConfigMap** para o **news-portal**

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: portal-configmap
data:
  IP_SISTEMA: http://192.168.49.2:30001 #se for windows colocar o localhost ao invés do InternalIP
```

* Aplique as configurações do **portal-configmap**

```shell
kubectl apply -f .\portal-configmap.yaml
```

* Adicione a env no pod news-portal 

````yaml
apiVersion: v1
kind: Pod
metadata:
  name: news-portal
  labels:
    app: news-portal
spec:
  containers:
    - name: news-portal-container
      image: aluracursos/portal-noticias:1
      ports:
        - containerPort: 80
      envFrom:
        - configMapRef:
            name: portal-configmap
````

* Delete o pod **news-portal.yaml**

````shell
kubectl delete pod news-portal
````

* Aplique as novas declarações no pod

````shell
kubectl apply -f .\news-portal.yaml
````

### Como ficou o Cluster do projeto

![Screenshot 2023-08-30 at 9.00.43 AM.png](img%2FScreenshot%202023-08-30%20at%209.00.43%20AM.png)

<p>Caso tivéssemos múltiplos nodes em nosso cluster, tudo funcionaria da mesma maneira, pois as portas mapeadas pelo NodePort 
são compartilhadas entre os IP's de todos os nodes.</p>

<p>Mais informações podem ser adquiridas em:</p> 

https://kubernetes.io/docs/concepts/services-networking/service/#nodeport