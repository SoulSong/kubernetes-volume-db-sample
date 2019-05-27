# Before you begin
Make sure the namespace named `volumn-ns` has been created.

# How to deploy
- create sc
```bash
$ kubectl apply -f ./kubernetes/redis/cluster/local/local-storageclass.yaml
```
 
- create pv
```bash
$ kubectl apply -f ./kubernetes/redis/cluster/local/redis-pv.yaml
```

- create configMap
```bash
$ kubectl apply -f ./kubernetes/redis/cluster/local/redis-cluster-configmap.yaml
```

- create headless-service
```bash
$ kubectl apply -f ./kubernetes/redis/cluster/local/redis-headless-service.yaml
```

- create statefulSet
```bash
$ kubectl apply -f ./kubernetes/redis/cluster/local/redis-statefulset.yaml
```

- create redis cluster
```bash
$ kubectl exec -it redis-cluster-0 -n volumn-ns -- redis-cli --cluster create --cluster-replicas 1 $(kubectl get pods -l app=redis-cluster -n volumn-ns -o jsonpath='{range.items[*]}{.status.podIP}:6379 ')
```

# How to test
- access the redis-cluster by the pod named `redis-cluster-0`:
```bash
$ kubectl exec -it redis-cluster-0 -n volumn-ns  -- redis-cli -c
```

# Expose Redis-server
If you need access the redis-cluster server which is deployed in k8s, just create normal service as follows:
- create access-service
```bash
$ kubectl apply -f ./kubernetes/redis/cluster/local/redis-access-service.yaml
```
If your apps also deployed in k8s, just access the redis cluster with the pod dns like `<pod-name>.<headless-service-name>.<namespace-name>.svc.cluster.local`, 
example `redis-cluster-0.redis-cluster-headless.volumn-ns.svc.cluster.local`.

# Cleaning up
```bash
$ kubectl delete -f ./kubernetes/redis/cluster/local/redis-statefulset.yaml
$ kubectl delete -f ./kubernetes/redis/cluster/local/redis-headless-service.yaml
$ kubectl delete -f ./kubernetes/redis/cluster/local/redis-cluster-configmap.yaml
$ kubectl delete pvc --all -n volumn-ns
$ kubectl delete -f ./kubernetes/redis/cluster/local/redis-pv.yaml
$ kubectl delete -f ./kubernetes/redis/cluster/local/local-storageclass.yaml
```

