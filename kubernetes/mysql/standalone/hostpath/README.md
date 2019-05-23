# Before you begin
Make sure the namespace named `volumn-ns` has been created.

# How to deploy
- create pv&pvc
```bash
$ kubectl apply -f ./kubernetes/mysql/standalone/hostpath/mysql-pv.yaml
```
- create deployment&service
```bash
$ kubectl apply -f ./kubernetes/mysql/standalone/hostpath/mysql-deployment.yaml
```

# How to test
- access mysql-server
```bash
kubectl run -it --rm --image=mysql:8.0 --restart=Never -n volumn-ns  mysql-client -- mysql -h mysql -P 3306 -ppassword
```

# Cleaning up
```bash
$ kubectl delete deployment,svc mysql -n volumn-ns
$ kubectl delete pvc mysql-pv-claim  -n volumn-ns
$ kubectl delete pv mysql-pv-volume
```