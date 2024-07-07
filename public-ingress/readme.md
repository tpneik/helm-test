# Instruction

```bash
# create namespcae
kubectl create namespace public-ingress

# helm install
helm install ingress ingress-nginx/ingress-nginx   \
--namespace public-ingress   \
--set controller.config.http2=true   \
--set controller.config.http2-push="on"   \
--set controller.config.http2-push-preload="on"   \
--set controller.ingressClassByName=true   \
--set controller.ingressClassResource.controllerValue=k8s.io/ingress-nginx   \
--set controller.ingressClassResource.enabled=true   \
--set controller.ingressClassResource.name=nginx   \
--set controller.service.externalTrafficPolicy=Local \   
--set controller.setAsDefaultIngress=true
```

## Make sure that "something" have not been created before

```bash
kubectl get ingressclass 
# If exist class "nginx" or something as mentioned above -> 
kubectl delete ingressclass nginx # or something that exist

# If something relate to admission -> Go check 
kubectl get validatingadmissionpolicies 
kubectl get validatingadmissionpolicybindings 
kubectl get validatingwebhookconfigurations