# Introduction
Define some db-servers in kubernetes, all servers will use different volume-types, 
like host,local and so on.

# Require
Create a namespace named volumn-ns for the definition of all resources.
- create namespace
```bash
$ kubectl apply -f ./kubernetes/namespace.yaml
```

# DB Servers
- mysql 
    - standalone
        - hostPath
        - local
- redis
    - standalone
        - configMap        