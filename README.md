# Pull Image from Private Docker Registry in Kubernetes cluster

##Create kubernetes secrets using command line


      kubectl create secret docker-registry your-registry-key \
    --docker-server=https://index.docker.io/v1/ \
    --docker-username=<your-registry-username> \
    --docker-password=<your-password> \
    --docker-email=<your-email@gmail.com>
    
    
## Create file my-app-deployment.yml
    
```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
  labels:
    app: my-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-app
  template:
    metadata:
      labels:
        app: my-app
    spec:
      imagePullSecrets:
      - name: your-registry-key
      containers:
      - name: my-app
        image: akkaoui/fastapi-app:v2
        imagePullPolicy: Always
        ports:
          - containerPort: 8100
```

## Deployment application on k8s

```
kubectl apply -f my-app-deployment.yml
```

## Create file my-app-service.yml
    
```
apiVersion: v1
kind: Service
metadata:
  name: my-app-service
spec:
  selector:
    app: my-app
  ports:
    - protocol: TCP
      port: 8100
      targetPort: 8100
  type: LoadBalancer
```

## Deployment serivce on k8s

```
kubectl apply -f my-app-serivce.yml
```


## Display serivces 

```
kubectl get svc
```

```
NAME             TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)          AGE
fastapi-app      LoadBalancer   xx.xxx.xx.xxx   xx.xxx.xx.xxx    8000:30965/TCP   5d5h
kubernetes       ClusterIP      xx.xxx.x.x      <none>           443/TCP          5d5h
my-app-service   LoadBalancer   xx.xxx.x.xxx    xx.xxx.xxx.xxx   8100:31694/TCP   42s
```
