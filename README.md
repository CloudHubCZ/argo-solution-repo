# Test solution repository for ArgoCD

# Commands
## accounting
k exec -it frontend-deployment-d5c7bc455-bpptt -n accounting -- curl http://backend-service:8080/actuator/health --max-time 3
k exec -it frontend-deployment-d5c7bc455-bpptt -n accounting -- curl http://persistence-service:8080/actuator/health --max-time 3

k exec -it backend-deployment-5454c9c54c-dzp68 -n accounting -- curl http://frontend-service:8080/actuator/health --max-time 3
k exec -it backend-deployment-5454c9c54c-dzp68 -n accounting -- curl http://persistence-service:8080/actuator/health --max-time 3

k exec -it persistence-deployment-c8f669857-rjtfh -n accounting -- curl http://frontend-service:8080/actuator/health --max-time 3
k exec -it persistence-deployment-c8f669857-rjtfh -n accounting -- curl http://backend-service:8080/actuator/health --max-time 3

## Sales
helm upgrade --install sales-chart  sales-chart -f sales-chart/values.yaml -n sales --create-namespace
k exec -it frontend-deployment-d5c7bc455-g25zf -n sales -- curl http://backend-service:8080/actuator/health --max-time 3
k exec -it frontend-deployment-d5c7bc455-g25zf -n sales -- curl http://persistence-service:8080/actuator/health --max-time 3

k exec -it frontend-deployment-d5c7bc455-g25zf -n sales -- curl http://backend-service.accounting:8080/actuator/health --max-time 3
k exec -it frontend-deployment-d5c7bc455-g25zf -n sales -- curl http://frontend-service.accounting:8080/actuator/health --max-time 3



