

## Run on Kubernetes


### Build the Gateway

1.  `$ cd daytrader-gatewayapp`

2.  `$ mvn -Pcd clean install`

    This command builds the Docker Image and pushes it to the DockerHub registry

### Start the Gateway

1.  `$ cd daytrader-gateway/env/external/k8s`

2.  `$ kubectl apply -f deployment.yaml`

    This command pulls the image from DockerHub and deploys it to the Kubernetes Cluster
    
3.  `$ kubectl get pods --watch`
    
    NAME | READY | STATUS | RESTARTS | AGE
    ---- | ----- | ------ | -------- | ---
    daytrader-gateway-xxxxxxxxx-xxxxx | 1/1 | Running | 0 | 6m
    
    Watch until you see READY `1/1` and STATUS `Running` then Ctrl-c to stop watching
    
4.  `$ kubectl apply -f service.yaml`

Currently, these commands are run manually, but they can easily be added to Maven

### Test the Gateway

1.  Start the Accounts, Portfolios, and Quotes

2.  Access the Swagger UI for testing the APIs

3.  Stop the Accounts, Portfolios, and Quotes
    
### Stop the Gateway

1.  `$ cd daytrader-web\env\external\k8s`

1.  `$ kubectl delete deployments daytrader-gateway`

2.  `$ kubectl delete services daytrader-gateway`

Currently, these commands are run manually, but they can easily be added to Maven

### Access the Swagger UI

1.  Start the Gateway

2.  `kubectl port-forward daytrader-gateway-xxxxxxxxx-xxxxx`

    You should see `Forwarding from 127.0.0.1:8888 -> 2443`
    
    This command forwards local port 8888 to port 2443 of your Pod

3.  Point you browser to https://localhost:2443/swagger-ui.html

4.  Stop the Gateway after reviewing (or testing) the APIs

