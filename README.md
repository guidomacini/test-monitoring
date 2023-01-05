# test-monitoring Project

With this project I've reproduced the problem (there is an "/hello" endpoint) -> test-monitoring/src/main/java/org/acme/GreetingResource.java. 
Enabling the ELASTIC_APM_ENABLE_EXPERIMENTAL_INSTRUMENTATIONS all endpoint is monitored under a GET or POST generic paths.

## My environment

We use minikube to have a Kubernetes environment, and we followed the [ECK guide](https://www.elastic.co/guide/en/cloud-on-k8s/current/k8s-quickstart.html) to deploy all resources on a Kubernetes cluster. 

## Running on Minikube

You can build a docker image running: 
```shell script
./gradlew build -Dquarkus.container-image.build=true
```

You can load the image on Minikube running:
```shell script
minikube image load {pc-username}/test-monitoring:1.0.0-SNAPSHOT
```

I created a kubernetes.yml file to deploy the application in Minikube (in a namespace 'test' as in the example) in /src/resources/. 
Modify ELASTIC_APM_SECRET_TOKEN and ELASTIC_APM_SERVER_URL accordingly to your environment:
```shell script
kubectl apply -f build/kubernetes/kubernetes.yml -n test
```
