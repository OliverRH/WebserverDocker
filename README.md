
# Installere webserver fra docker image

Jeg har uploaded et docker image som består af websiden med HTML, CSS og JavaScript, og så selve webserver delen som benytter Apache HTTP Server Project (httpd). Derudover har jeg to YAML filer, **webserver-deployment.yaml** og **webserver-service.yaml**, der skal bruges for at køre webserveren.





## Installation

**Valgfrit:**
Du kan vælge selv at bygge dit docker image, det gør du ved at køre følgende kode i din terminal. Husk at være inde i mappen **WebserverDocker**

```
docker build -t webserver .
```

Jeg har også uploade dette image på hub.docker.com, det kan hentes ved at bruge:
```
oliverrhen/webserver
```

##
Start med at starte minikube:

```
minikube start
```

Opret deployment og service for webseveren:
```
kubectl apply -f ./webserver-deployment.yaml
kubectl apply -f ./webserver-service.yaml
```
Du kan nu skrive:
```
kubectl get pods
```
Du skulle gerne få noget ligende dette:
```
NAME                                       READY   STATUS    RESTARTS   AGE
webserver-deployment-6cc4975b6c-49m9f      1/1     Running   0          152m
webserver-deployment-6cc4975b6c-bhltc      1/1     Running   0          152m
webserver-deployment-6cc4975b6c-dxt2b      1/1     Running   0          152m
webserver-deployment-6cc4975b6c-rbmz6      1/1     Running   0          152m
webserver-deployment-6cc4975b6c-x25gm      1/1     Running   0          152m
```
Du kan også teste ved at skrive:
```
kubectl get deployment
```
Så skulle du få dette:
```
NAME                       READY   UP-TO-DATE   AVAILABLE   AGE
webserver-deployment       5/5     5            5           153m
```
Du kan også teste ved at skrive:
```
kubectl get service    
```
Så skulle du få dette:
```
NAME                TYPE        CLUSTER-IP    EXTERNAL-IP   PORT(S)        AGE
kubernetes          ClusterIP   10.96.0.1     <none>        443/TCP        162m
webserver-service   NodePort    10.99.51.85   <none>        80:30428/TCP   151m
```

For at få url til hjemmesiden:

```
minikube service webserver-service --url 
```
Så vil du få en IP adresse du kan indtaste i din browser
```
http://127.0.0.1:57386
❗  Because you are using a Docker driver on darwin, the terminal needs to be open to run it.
```
