# Containerising an Asp.Net Core 3.0 Web Api

Containerising an Asp.Net Core 3.0 Web Api and running it in Kubernetes.

## Prerequisites

* .Net Core 3.0
* Docker Desktop
* Visual Studio Code
* Postman

## New webapi

This is a helloworld api and not for production!

```sh
dotnet new webapi -o HelloAspNetCore --no-https
cd HelloAspNetCore/
code .
```

## Dockerfile

Use the docker extension in Visual Studio Code to generate the dockefile, select View > Command Palette > Docker: Add Docker Files to Workspace...

Then:

```sh
docker build -t hello-aspnetcore:v1 .
docker images # to verify image is built
docker run -it --rm -p 8080:80 hello-aspnetcore:v1
```

Test using postman when running:
<http://localhost:8080/weatherforecast>

Ctrl-c to exit.

## Kubernetes

Enable a local kubernetes cluster using Docker Desktop. Use the Kubernetes extension in Visual Studio Code to help author the deployment and service yaml.

```sh
kubectl config get-contexts # check that the docker desktop is the current context
kubectl apply -f deployment.yaml
kubectl get deployments
kubectl get pods
kubectl logs hello-aspnetcore-deployment-c59bdf7-qhvpw # use pod name from previous command
kubectl apply -f service.yaml
kubectl get services
```

Test using postman when running:
<http://localhost:8080/weatherforecast>
