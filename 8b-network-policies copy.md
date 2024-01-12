# Create a NetworkPolicy That Allows All Pods in the myproject Namespace to Communicate with Each Other Only on a Specific Port

step1 - label the namespace 

link - https://raw.githubusercontent.com/kubernetes/website/main/content/en/examples/service/networking/networkpolicy.yaml

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: np-users-backend-80
  namespace: users-backend
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          app: users-backend
    ports:
    - protocol: TCP
      port: 80
```