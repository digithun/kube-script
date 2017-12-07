
## Example
- app running at PORT 8080
- images will auto start images


## Start image / service
`kubectl run jamplay-web --image=gcr.io/jamplay-deploy-poc/jamplay-web --port 8080`

## Expose service to internet from loadbalancer
`kubectl expose deployment jamplay-web --type=LoadBalancer --port 80 --target-port 8080`

## Edit deployment config
**Change jamplay-web to your deployment name**
- get deployment config file
`kubectl get deployment jamplay-web --output yaml >> kube.yml`
- patch deployment file
`kubectl patch deployment jamplay-web --patch "$(cat kube.yml)"`


## Monitor
`kubectrl get service`
`kubectrl get pods`
`kubectrl get deployment`



## See dns table in kube cluster
- create busybox
`kubectl create -f ./busybox.yaml`

- waiting for pod ready
`kubectl get pods busybox`

- check dns
`kubectl exec -ti busybox -- nslookup ${YOUR_DNS}`
> NOTE: ${YOUR_DNS} is Kube service ns {SERVICE_NAME}.{NAME_SPACE} example "jamplay-web.default"
