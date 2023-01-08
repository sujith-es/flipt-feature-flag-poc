# POC For Flipt Feature Flag with MySQL Database as Backend
## Flipt

More Information on 

- [Flitp](https://www.flipt.io/)
- [MySQL packaged by Bitnami](https://bitnami.com/stack/mysql/helm)

```
kubectl apply -f flipt-storageclass.yaml
kubectl apply -f flipt-pvc.yaml
```
```
helm repo add flipt https://helm.flipt.io
helm upgrade --install flipt flipt/flipt -n flipt -f flipt-values.yaml
```

```
kubectl get svc
```
### MySQL Credential (Replace your password)

```
admin
MYSQL_PASSWORD
```

### MySQL Installation

```
$ helm repo add my-repo https://charts.bitnami.com/bitnami
$ helm install mysql my-repo/mysql -f 

helm upgrade --install mysql my-repo/mysql -n flipt -f bitnami-mysql-values.yaml

```

### MySQL Authentication

```bash
 mysql://root:MYSQL_PASSWORD@mysql.flipt.svc.cluster.local:3306/flipt
```


### Connect to Pods - Port Forwarding

```
kubectl port-forward \
svc/mysql 3306:3306 \
-n flipt

kubectl port-forward \
svc/flipt 8084:8084 \
-n flipt
```



```
export NODE_PORT=$(kubectl get --namespace flipt -o jsonpath="{.spec.ports[0].nodePort}" services flipt)
export NODE_IP=$(kubectl get nodes --namespace flipt -o jsonpath="{.items[0].status.addresses[0].address}")
echo http://$NODE_IP:$NODE_PORT
```


