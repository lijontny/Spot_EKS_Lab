# Karpenter
1. Change to working directory
   ```commandline
   cd ~/environment/terraform-aws-eks-blueprints/examples/karpenter/
    ```
2. Deploy Karpenter Cluster
   - Initialize working directory
    ```commandline
   terraform init
    ```
   - plan deployment
    ```commandline
   terraform plan
    ```
   - apply
    ```commandline
    terraform apply
    ```
3. Add Kubernetes context in config
```commandline
aws eks --region us-west-2 update-kubeconfig --name karpenter
```
4. Validate deployment
```commandline
kubectl get nodes
```
5. Check Karpenter Logs
```commandline
kubectl logs -f deployment/karpenter -n karpenter controller
```
6. Scale out with sample script
```commandline
kubectl apply -f provisioners/sample_deployment_lt.yaml
```