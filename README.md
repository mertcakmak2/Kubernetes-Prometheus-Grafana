
## Helm Kurulumu

```bash
  curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
```

```bash
  sudo apt-get install apt-transport-https --yes
```

```bash
  echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
```
```bash
  sudo apt-get update
```
```bash
  sudo apt-get install helm
```
![image](https://user-images.githubusercontent.com/21373505/146519688-abec4199-9ab4-446b-bae4-a3949ed06153.png)

## Prometheus Kurulumu

```bash
  kubectl create namespace monitoring
```
```bash
  kubectl get ns
```
```bash
  helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
```
```bash
  helm repo update
```
```bash
  helm install k8spromethuesstack --namespace monitoring prometheus-community/kube-prometheus-stack
```

![image](https://user-images.githubusercontent.com/21373505/146519705-08a81569-954c-45ea-8187-e53bef83dc92.png)
![image](https://user-images.githubusercontent.com/21373505/146519921-d9bec0fb-8c61-43b1-97a4-80a89848730d.png)

## Grafana Ui İçin NodePort Verme İşlemi

- kubectl patch svc k8spromethuesstack-grafana -p '{"spec": {"type": "NodePort"}}' -n monitoring

http://167.172.105.147:31513 ⇒ Grafana UI

## Prometheus Ui İçin NodePort Verme İşlemi

- kubectl patch svc k8spromethuesstack-kube-pr-prometheus -p '{"spec": {"type": "NodePort"}}' -n monitoring

http://167.172.105.147:30385 ⇒ Prometheus UI
