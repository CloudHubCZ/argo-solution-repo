# Test solution repository for ArgoCD

## Prerequisites
### Install Nginx
helm upgrade --install ingress-nginx ingress-nginx \
--repo https://kubernetes.github.io/ingress-nginx \
--namespace ingress-nginx --create-namespace

# Install ArgoCD


## Accounting
k exec -it frontend-deployment-d5c7bc455-bpptt -n accounting -- curl http://backend-service:8080/actuator/health --max-time 3
k exec -it frontend-deployment-d5c7bc455-bpptt -n accounting -- curl http://persistence-service:8080/actuator/health --max-time 3

k exec -it backend-deployment-5454c9c54c-dzp68 -n accounting -- curl http://frontend-service:8080/actuator/health --max-time 3
k exec -it backend-deployment-5454c9c54c-dzp68 -n accounting -- curl http://persistence-service:8080/actuator/health --max-time 3

k exec -it persistence-deployment-c8f669857-rjtfh -n accounting -- curl http://frontend-service:8080/actuator/health --max-time 3
k exec -it persistence-deployment-c8f669857-rjtfh -n accounting -- curl http://backend-service:8080/actuator/health --max-time 3

## Sales
### Install Helm
helm upgrade --install sales-chart  sales-chart -f sales-chart/values.yaml -n sales --create-namespace

### Commands
k exec -it frontend-deployment-d5c7bc455-g25zf -n sales -- curl http://backend-service:8080/actuator/health --max-time 3
k exec -it frontend-deployment-d5c7bc455-g25zf -n sales -- curl http://persistence-service:8080/actuator/health --max-time 3

k exec -it frontend-deployment-d5c7bc455-g25zf -n sales -- curl http://backend-service.accounting:8080/actuator/health --max-time 3
k exec -it frontend-deployment-d5c7bc455-g25zf -n sales -- curl http://frontend-service.accounting:8080/actuator/health --max-time 3


helm template sales-prod sales-chart -f sales-chart/values-prod.yaml -n sales-prod > prod/template.yaml && \
helm template sales-test sales-chart -f sales-chart/values-test.yaml -n sales-test > test/template.yaml

git commit -am "Commit" && git push

curl frontend-test.cloudhub.cz/hello -vvvv
curl frontend-prod.cloudhub.cz/hello -vvvv