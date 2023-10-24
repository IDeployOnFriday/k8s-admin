Count the number of nodes that are ready to run normal workloads

```
   k get nodes --no-headers | grep -v -c control-plane > count.txt
```