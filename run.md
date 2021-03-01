1. Install minikube (https://minikube.sigs.k8s.io/docs/start/)
2. Install kube-state-metrics (download https://github.com/kubernetes/kube-state-metrics/tree/master/examples/standard and execute `kubectl apply -f .` inside the manifests' folder)
3. Install istio (follow https://istio.io/v1.7/docs/setup/getting-started/, until `Verify external access` step)
4. Create a free tier elastic account (https://cloud.elastic.co/registration?elektra=en-cloud-page) and create the following stack:
```
Create an Elastic Observability Deployment:
provider: Google Cloud
region: europe-west1
stack version: 7.11.1
Download and save the credentials
```
5. Create a testing Slack account
Create and store a Slack webhook: https://www.elastic.co/guide/en/kibana/7.11/slack-action-type.html#configuring-slack


## LOCAL STACK (deprecated)
#kubectl apply -f snapshot.yml
#minikube -n kube-system service kibana --url
#kubectl -n kube-system port-forward svc/kibana 5601

kubectl apply -f nginx.yml

1. verify cloud.id, cloud.auth

2. explain and `kubectl apply -f filebeat-kubernetes.7.11.yaml`

3. explain and `kubectl apply -f metricbeat-kubernetes.7.11.yaml` (if timeout then remove dashboard.setup)

4. Talk about istio and show live the changes

5. kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -s productpage:9080/productpage | grep -o "<title>.*</title>"
while sleep 3; do kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -s productpage:9080/productpage | grep -o "<title>.*</title>"; done

6. create an alert on Metrics Explorer based on `prometheus.istio_requests_total.rate`

7. `term to highlight: "Generated config:"` and kubectl apply -f nats.yaml

8. Show nats dashboards

#QUERY: kubernetes.labels.k8s-app: "metricbeat"


9. 
```
cat << EOF | kubectl apply -f -
apiVersion: v1
kind: Secret
metadata:
  name: somesecret
type: Opaque
data:
  value: $(echo -n "passpass" | base64)
EOF
```

kubectl apply -f redis.yml