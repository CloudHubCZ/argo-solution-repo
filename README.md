# Test solution repository for ArgoCD

## Commands
k exec -it frontend-deployment-d5c7bc455-jh75j -n accounting -- curl http://backend-service:8080/actuator/health
k exec -it frontend-deployment-d5c7bc455-jh75j -n accounting -- curl http://persistence-service:8080/actuator/health