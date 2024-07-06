
# Pakage
## Make packet
Go to chart folder 
```bash
helm package . # /// -> return my-chart-0.1.0.tgz
```
## Move the tgz file to github repo

```bash
cd ../my-chart-repo
mv ../my-chart-0.1.0.tgz .
```

## Add index for repo 
```bash 
# helm repo index . --url https://your-username.github.io/your-repository, below is mine !
helm repo index . --url https://tpneik.github.io/helm-test
```

## Do as normal
```bash
git add .
git commit -m "Add Helm chart my-chart-0.1.0"
git push origin main
```

## Enable GitHub Pages
Go to your GitHub repository on the GitHub website and enable GitHub Pages:

- Navigate to the repository settings.
- Scroll down to the "GitHub Pages" section.
- Select the branch you want to use for GitHub Pages (e.g., main).
- Choose the root directory (/).


# Deploy 

##
Defaul yml

```yaml
namespace: nodetest-ns

appName: nodetest

outterPort: 31313
replicas: 5

image:
  name: tpneik/apptest
  tag: v1

service:
  nodeport:
    port: 80
    targetport: 3000
    nodeport: 31313
  loadbalancer:
    port: 80
    targetport: 3000
  clusterip:
    port: 80
    targetport: 3000

env: clusterip
```

## Add repo
```bash
helm repo add helm-test https://tpneik.github.io/helm-test
helm repo update
```
## Runnnnnn
```bash
# you can overside as the value I add above !
# you alse can choose the service type by define env

helm install example helm-test/nodetest --set env=clusterip --set namespace=example
```