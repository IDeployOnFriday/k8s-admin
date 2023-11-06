# Create a NetworkPolicy That Denies All Access to the Maintenance Pod

link - https://raw.githubusercontent.com/kubernetes/website/main/content/en/examples/service/networking/network-policy-default-deny-all.yaml
```
---
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-all-ingress
spec:
  podSelector: 
    matchLabels
    app: maintenance 
  policyTypes:
  - Ingress
  - Egress
```

# Create a NetworkPolicy That Allows All Pods in the myproject Namespace to Communicate with Each Other Only on a Specific Port

link - https://raw.githubusercontent.com/kubernetes/website/main/content/en/examples/service/networking/networkpolicy.yaml

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: network-policy
  namespace: foo
spec:
  podSelector:
    matchLabels:
      role: db
  policyTypes:
    - Ingress
  ingress:
    - from:
        - namespaceSelector:
            matchLabels:
              project: myproject
      ports:
        - protocol: TCP
          port: 80
```