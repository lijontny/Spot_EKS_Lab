# Kubecost
### Steps:
1. Create an Ingress Class
```commandline
cat <<EOF | kubectl create -f -
apiVersion: networking.k8s.io/v1
kind: IngressClass 
metadata:
  name: aws-alb
spec:
  controller: ingress.k8s.aws/alb  
EOF

```

2. Expose Kubecost with an ALB (Create a K8s service)
```commandline
cat <<EOF | kubectl apply -f -
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  namespace: kubecost
  name: kubecost-ingress
  annotations:
    alb.ingress.kubernetes.io/scheme: internet-facing 
    alb.ingress.kubernetes.io/target-type: ip 
spec:
  ingressClassName: aws-alb 
  rules:
  - http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: kubecost-cost-analyzer 
            port:
               number: 9090
EOF
```
3. Find endpoint to access Kubecost ALB
```commandline
$ kubectl get ingress -n kubecost
NAME               CLASS     HOSTS   ADDRESS                                                                  PORTS   AGE
kubecost-ingress   aws-alb   *       k8s-kubecost-kubecost-xxxxxxxxx.us-west-2.elb.amazonaws.com   80      34s
```