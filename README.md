# KubeAI on Huawei Cloud Managed Kubernetes Service (CCE)


### To deploy

1. Create a namespace, in this example "kubeai"
   ```kubectl create namepace -n kubeai```
2. Create pv and pvc for open-webui
   ```kubectl create -f pv-pvc.yaml -n kubeai```
3. Deploy kubeai with custom-values.yaml
   ```helm upgrade --install kubeai kubeai/kubeai -f custom-values.yaml  -n kubeai --wait --timeout 15m```
4. Deploy models with kubeai-models.yaml
   ```helm upgrade kubeai-models kubeai/models -f ./kubeai-models.yaml -n kubeai --wait --timeout 15m```
5. Create a Load Balancer service to access open-webui
