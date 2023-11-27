1. Launch a Kubernetes cluster over AWS console using either eksctl or console. Please refer the below link for reference

https://docs.aws.amazon.com/eks/latest/userguide/create-cluster.html

2. Create the application pods usng deployment.yaml file by running the command `kubectl apply -f deployment.yaml`
3. Check the pods to be in running state using the command `kubectl get pods -A`
4. Launch the service of Load Balancer type to access the pods launched using the command `kubectl apply -f service.yaml`
5. Check the endpoint for the load balancer created `kubectl get svc -A`
6. Go over the browser to check the launched application and verify for the load balancer on AWs console
