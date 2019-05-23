# Before you begin
Make sure the namespace named `volumn-ns` has been created.

# How to deploy
- create storage-class
```bash
$ kubectl apply -f ./kubernetes/mysql/standalone/local/local-storageclass.yaml
```
- create pv
```bash
$ kubectl apply -f ./kubernetes/mysql/standalone/local/mysql-pv.yaml
```
- create statefulSet&service
```bash
$ kubectl apply -f ./kubernetes/mysql/standalone/local/mysql-statefulset.yaml
```

# How to test
- access mysql-server
```bash
kubectl run -it --rm --image=mysql:8.0 --restart=Never -n volumn-ns  mysql-client -- mysql -h mysql -P 3306 -ppassword
```

# Cleaning up
```bash
$ kubectl delete -f ./kubernetes/mysql/standalone/local/mysql-statefulset.yaml
$ kubectl delete pvc mysql-persistent-storage-mysql-0  -n volumn-ns
$ kubectl delete pv mysql-pv-volume
$ kubectl delete sc local-storage 
```