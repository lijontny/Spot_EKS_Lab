# EC2 Spot with Multiple Instances
### Autoscaling with Attribute Based Instance Type
1. Clone the github repo - Follow the instructions [here](https://ec2spotworkshops.com/ec2-auto-scaling-with-multiple-instance-types-and-purchase-options/clone_github.html){:target="_blank" rel="noopener"}
2. Create a EC2 launch template - Follow the instructions [here](https://ec2spotworkshops.com/ec2-auto-scaling-with-multiple-instance-types-and-purchase-options/create_lt.html){:target="_blank" rel="noopener"}
3. Deploy the aws elastic load balancer - Follow the instructions [here](https://ec2spotworkshops.com/ec2-auto-scaling-with-multiple-instance-types-and-purchase-options/deploy_lb.html){:target="_blank" rel="noopener"}
4. Create an ec2 auto scaling group (ASG) - Follow the instructions [here](https://ec2spotworkshops.com/ec2-auto-scaling-with-multiple-instance-types-and-purchase-options/create_asg.html){:target="_blank" rel="noopener"}
   - We will be using **Attribute based Instance Type** Selection in the autoscaling group. This feature will let you define the instance type in form of vCPU, memory and more instead of directly calling instance type
5. Verify the instances type - Browse the webapp [here](https://ec2spotworkshops.com/ec2-auto-scaling-with-multiple-instance-types-and-purchase-options/browse_app.html){:target="_blank" rel="noopener"}

### Scale-Out with Spot

1. Setup dynamic scaling in ASG - Follow instructions [here](https://ec2spotworkshops.com/ec2-auto-scaling-with-multiple-instance-types-and-purchase-options/scale_dynamic.html){:target="_blank" rel="noopener"}
2. Stress Test with AWS Systems Manager - Follow instructions [here](https://ec2spotworkshops.com/ec2-auto-scaling-with-multiple-instance-types-and-purchase-options/stress_ssm.html){:target="_blank" rel="noopener"}