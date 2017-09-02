# Initial Deployment

```bash
kubectl apply -f initial-deployment.yml
kubectl apply -f godemo-svc.yml
kubectl get svc godemo -o yaml # to get ELB url
while true; do curl aad83d55d8fe911e7b74d0236380feec-152972459.us-east-2.elb.amazonaws.com && echo "" && sleep 0.5; done # execute in another terminal
```

## Canary Deployment

```bash
kubectl -f apply godemo-canary.yml
```

## Rollout

```bash
kubectl scale deployment godemo --replicas 12 #scale to see rollout
kubectl set image deployment/godemo godemo=andrleite/godemo:v1.1 # change deployment image
kubectl rollout status deployment/godemo #verify rollout
kubectl rollout history deployment/godemo
kubectl rollout history deployment/godemo --revision=3
kubectl rollout undo deployment/godemo #change deployment back to previsious rollout revision
kubectl delete -f godemo-canary.yml
```

## Blue Green Deployment

```bash
kubectl apply -f godemo-green.yml
kubectl patch svc godemo -p '{"spec":{"selector":{"color":"green"}}}' # change traffic to green deployment
kubectl patch svc godemo -p '{"spec":{"selector":{"color":"blue"}}}' # change traffic back to blue deployment
```
