# Manual Application Deployment
Note: This Application will be used to test Karpenter scale out mechanism

### Deploy a sample nginx deployment with 2 replicas
```commandline
cat <<EOF | kubectl apply -f -
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
EOF
```
### Validate
Run `get` command below to find deployment:
```commandline
kubectl get deployment
```
Expected output:
```commandline
NAME               READY   UP-TO-DATE   AVAILABLE   AGE
nginx-deployment   2/2     2            2           23s
```
