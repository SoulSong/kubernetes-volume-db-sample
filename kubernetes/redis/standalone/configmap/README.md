# Before you begin
Make sure the namespace named `volumn-ns` has been created.

# How to deploy
- create configMap
```bash
$ kubectl apply -f ./kubernetes/redis/standalone/configmap/redis-configmap.yaml
```

- create deployment&service
```bash
$ kubectl apply -f ./kubernetes/redis/standalone/configmap/redis-deployment.yaml
```

# How to test
- access redis-server
```bash
$ kubectl run -it --rm --image=redis:5.0.4 --restart=Never -n volumn-ns  redis-cli -- redis-cli -h redis -p 6379
If you don't see a command prompt, try pressing enter.
redis:6379> info memory
# Memory
used_memory:852952
used_memory_human:832.96K
used_memory_rss:5570560
used_memory_rss_human:5.31M
used_memory_peak:873784
used_memory_peak_human:853.30K
used_memory_peak_perc:97.62%
used_memory_overhead:840726
used_memory_startup:791032
used_memory_dataset:12226
used_memory_dataset_perc:19.74%
allocator_allocated:1157176
allocator_active:1372160
allocator_resident:8183808
total_system_memory:10971176960
total_system_memory_human:10.22G
used_memory_lua:37888
used_memory_lua_human:37.00K
used_memory_scripts:0
used_memory_scripts_human:0B
number_of_cached_scripts:0
maxmemory:2097152
maxmemory_human:2.00M
maxmemory_policy:allkeys-lru
allocator_frag_ratio:1.19
allocator_frag_bytes:214984
allocator_rss_ratio:5.96
allocator_rss_bytes:6811648
rss_overhead_ratio:0.68
rss_overhead_bytes:-2613248
mem_fragmentation_ratio:6.86
mem_fragmentation_bytes:4758632
mem_not_counted_for_evict:0
mem_replication_backlog:0
mem_clients_slaves:0
mem_clients_normal:49694
mem_aof_buffer:0
mem_allocator:jemalloc-5.1.0
active_defrag_running:0
lazyfree_pending_objects:0
redis:6379> set foo bar
OK
redis:6379> get foo
"bar"
redis:6379> exit
```

# Cleaning up
```bash
$ kubectl delete -f ./kubernetes/redis/standalone/configmap/redis-deployment.yaml
$ kubectl delete -f ./kubernetes/redis/standalone/configmap/redis-configmap.yaml
```