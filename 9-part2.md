# Create a Pod Which Uses a Sidecar to Expose the Main Container's Log File to Stdout

link to sidecar yaml - https://kubernetes.io/docs/concepts/workloads/pods/sidecar-containers/


```
apiVersion: v1
kind: Pod
metadata:
  name: logging-sidecar
  namespace: baz
spec:
  containers:
  - name: busybox1
    image: busybox
    command: ['sh', '-c', 'while true; do echo Logging data > /output/output.log; sleep 5; done']
    volumeMounts:
    - name: sharedvol
      mountPath: /output
  - name: sidecar
    image: busybox
    command: ['sh', '-c', 'tail -f /input/output.log']
    volumeMounts:
    - name: sharedvol
      mountPath: /input
  volumes:
  - name: sharedvol
    emptyDir: {}
```