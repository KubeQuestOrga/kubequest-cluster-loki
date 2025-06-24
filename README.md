# KubeQuest - Loki / Grafana - Cluster K3s

## Pourquoi Loki + Grafana ❓

Le tableau de bord Kubernetes permet de gérer les objets du cluster,  
mais il est **limité pour l'observation en profondeur** des logs et des performances.

Pour une **observabilité complète**, on utilise :
- **Loki** : une solution de centralisation de logs, développée par Grafana Labs, pensée comme "Prometheus pour les logs".
- **Promtail** : un agent déployé sur chaque nœud qui collecte les logs des pods.
- **Grafana** : une plateforme de visualisation des métriques **et des logs**.

<br /><br /><br /><br />


## ⚙ Setup Environment
1. Connect to the NODE MASTER in Cluster K3S.
2. Install HELM : https://helm.sh/docs/intro/install/
3. Use repo grafana/loki stack HELM : https://artifacthub.io/packages/helm/grafana/loki-stack
4. Run command :
```bash
sudo chmod 644 /etc/rancher/k3s/k3s.yaml
sudo helm repo add grafana https://grafana.github.io/helm-charts
sudo helm repo update
sudo KUBECONFIG=/etc/rancher/k3s/k3s.yaml helm install loki-stack grafana/loki-stack --version 2.10.2 --namespace loki-grafana-stack --create-namespace --set grafana.enabled=true --set promtail.enabled=true
```
5. Récupérer le mot de passe lors du setup du site :
```bash
kubectl get secret --namespace loki-grafana-stack loki-stack-grafana -o jsonpath="{.data.admin-password}" | base64 -d && echo
```
