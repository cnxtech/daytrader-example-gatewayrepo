
## Run on Kubernetes

### Build the Gateway

1.  `$ cd daytrader-gatewayapp`

2.  `$ mvn -Pcd clean install`

    This command builds the Docker Image and pushes it to the DockerHub registry

### Start the Gateway

1.  `$ kubectl apply -f daytrader-gateway/env/external/k8s/deployment.yaml`

    This command pulls the image from DockerHub and deploys it to the Kubernetes Cluster
    
2.  `$ kubectl get pods --watch`
    
    NAME | READY | STATUS | RESTARTS | AGE
    ---- | ----- | ------ | -------- | ---
    daytrader-gateway-xxxxxxxxx-xxxxx | 1/1 | Running | 0 | 6m
    
    Watch until you see READY `1/1` and STATUS `Running` then Ctrl-c to stop watching
    
3.  `$ kubectl apply -f daytrader-gateway/env/external/k8s/service.yaml`

**TODO** Add a `deploy_server` shell script to run these commands. (See Run on Spring Boot)

### Test the Gateway
                    
1.  Start the Accounts, Portfolios, and Quotes

2.  `$ cd daytrader-gateway`

3.  `$ mvn -Pci-k8s clean verify`

    This command starts the application, runs the integration tests, and stops the aplication

    **TODO** Add the `ci-k8s` Maven profile to run these integration tests. (See Run on Spring Boot)

4.  Stop the Accounts, Portfolios, and Quotes
    
### Stop the Gateway

1.  `$ kubectl delete deployments daytrader-gateway`

2.  `$ kubectl delete services daytrader-gateway`

    **TODO** Add an `undeploy_server` shell script to run these commands. (See Run on Spring Boot)

### Review the Swagger Documentation

1.  Start the Gateway

2.  `kubectl port-forward daytrader-gateway-xxxxxxxxx-xxxxx`

    You should see `Forwarding from 127.0.0.1:8888 -> 2443`
    
    This command forwards local port 8888 to port 2443 of your Pod

3.  Point you browser to `https://localhost:2443/swagger-ui.html`

4.  Stop the Gateway after reviewing the APIs



