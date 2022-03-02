argo 部署流任务
argo submit helloworld.yaml -n argo
argo list -n argo
argo get -n argo @latest
argo logs -n argo @latest

kubectl -n argo port-forward deployment/argo-server 2746:2746