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