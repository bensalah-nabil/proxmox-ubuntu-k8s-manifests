### podinfo ###
# Generate GitRepository Resource YAML
flux create source git podinfo --url=https://github.com/Selvamraju007/podinfo-app --branch=master --interval=30s --export > ./clusters/tur/podinfo-source.yaml

# Generate Kustomization Resource YAML
flux create kustomization podinfo --target-namespace=default --source=podinfo-app --path="./kustomize" --prune=true --interval=5m --export > ./clusters/tur/podinfo-kustomization.yaml

### 5-DEMO ###
flux create source git 5-demo-source-git-bb-app --url https://github.com/bensalah-nabil/bb-app-source --branch 5-demo --timeout 10s --export > 5-demo-source-git-bb-app.yaml

flux create helmrelease 5-demo-helm-release-git-helm-bb-app --chart helm-chart --interval 10s --target-namespace 5-demo --source GitRepository/5-demo-source-git-bb-app --values 5-demo-values.yaml --export > 5-demo-helm-release-git-helm-bb-app.yaml

### 3-DEMO ###
flux create kustomization  3-demo-kustomize-git-bb-app --source GitRepository/3-demo-source-git-bb-app --prune true --interval 10s --target-namespace 3-demo --path kustomize --export > 3-demo-kustomize-git-bb-app.yaml 

### 6-DEMO ###

flux create helmrelease 6-demo-helm-release-git-helm-bb-app --chart helm-chart --interval 10s --target-namespace 6-demo --source GitRepository/6-demo-source-helm-bb-app --values ../../../6-demo-values.yaml --export > 6-demo-helm-release-git-helm-bb-app.yaml

### OPENWEBUI ###
flux create source helm webssh --url https://helm.openwebui.com --timeout 10s --export > webssh.yaml

flux create helmrelease helm-release-helm-webssh --chart open-webui --interval 10s --target-namespace webssh-system --source HelmRepository/webssh --values ../../../webssh-values.yaml --export > helm-release-webssh.yaml

#### INGRESS ####
flux create source helm ingress-nginx --url  https://kubernetes.github.io/ingress-nginx --timeout 10s --export > source-helm-ingress-nginx.yaml

flux create helmrelease helm-release-ingress-nginx --chart ingress-nginx  --interval 10s --target-namespace ingress-nginx --source HelmRepository/ingress-nginx --values ../../../proxmox-ubuntu-k8s/helm/ingress-nginx/values.yaml --export > helm-release-ingress-nginx.yaml

### PROMETHEUS ####
flux create source helm promethus-grafana --url  https://prometheus-community.github.io/helm-charts --timeout 10s --export > source-helm-prometheus-grafana.yaml

flux create helmrelease helm-release-promethus-grafana --chart kube-prometheus-stack  --interval 10s --target-namespace monitoring --source HelmRepository/promethus-grafana --values ../../../proxmox-ubuntu-k8s/helm/prometheus-grafana/values.yaml --export > helm-release-promethus-grafana.yaml

### OPENCOST ####
flux create source helm opencost --url https://opencost.github.io/opencost-helm-chart --timeout 10s --export > source-helm-opencost.yaml

flux create helmrelease helm-release-opencost --chart opencost  --interval 10s --target-namespace opencost --source HelmRepository/opencost --values ../../../proxmox-ubuntu-k8s/helm/opencost/values.yaml --export > helm-release-opencost.yaml

### LONGHORN ####
flux create source helm longhorn --url https://charts.longhorn.io --timeout 10s --export > source-helm-longhorn.yaml

flux create helmrelease helm-release-longhorn --chart longhorn --interval 10s --target-namespace longhorn-system  --source HelmRepository/longhorn  --values ../../../proxmox-ubuntu-k8s/helm/longhorn/values.yaml --export > helm-release-longhorn.yaml

### METALB ###
flux create source helm metalb-helm --url https://metallb.github.io/metallb  --timeout 10s --export > source-helm-metalb.yaml

flux create helmrelease helm-release-metalb --chart metallb --interval 10s --target-namespace metalb-system  --source HelmRepository/metalb-helm  --values ../../../proxmox-ubuntu-k8s/helm/metalb/values.yaml --export > helm-release-metalb.yaml

flux create source git metalb-git --url https://github.com/bensalah-nabil/proxmox-ubuntu-k8s --branch main --timeout 10s --export > source-git-metalb.yaml

flux create kustomization  kustomize-git-metalb --source GitRepository/metalb-git --prune true --interval 10s --target-namespace metalb-system --path manifests/meta-lb --export > kustomize-git-metalb.yaml

### K8S-DASHBOARD ###

flux create source helm kubernetes-dashboard --url https://kubernetes.github.io/dashboard/ --timeout 10s --export > source-helm-kubernetes-dashboard.yaml

flux create helmrelease helm-release-kubernetes-dashboard --chart kubernetes-dashboard --interval 10s --target-namespace k8s-ui-system  --source HelmRepository/kubernetes-dashboard --values ../../../proxmox-ubuntu-k8s/helm/k8s-ui/values.yaml --export > helm-release-kubernetes-dashboard.yaml

### HARBOR ####

flux create source helm harbor --url https://helm.goharbor.io --timeout 10s --export > source-helm-harbor.yaml

flux create helmrelease helm-release-harbor --chart harbor --interval 10s --target-namespace harbor-system  --source HelmRepository/harbor --values ../../../proxmox-ubuntu-k8s/helm/harbor/values.yaml --export > helm-release-harbor.yaml

### Jenkins ###

flux create source helm jenkins --url https://charts.jenkins.io --timeout 10s --export > source-helm-jenkins.yaml

flux create helmrelease helm-release-jenkins --chart jenkins --interval 10s --target-namespace jenkins-system  --source HelmRepository/jenkins --values ../../../proxmox-ubuntu-k8s/helm/jenkins/values.yaml --export > helm-release-jenkins.yaml

### Chaos ###

flux create source helm chaos-mesh --url https://charts.chaos-mesh.org --timeout 10s --export > source-helm-chaos-mesh.yaml

flux create helmrelease helm-release-chaos --chart chaos-mesh --interval 10s --target-namespace chaos-mesh --source HelmRepository/chaos-mesh --values ../../../proxmox-ubuntu-k8s/helm/chaos-mesh/values.yaml --export > helm-release-chaos-mesh.yaml

### Oauth Proxy ###

flux create source helm oauth-proxy --url https://oauth2-proxy.github.io/manifests  --timeout 10s --export > source-helm-oauth-proxy.yaml

flux create helmrelease helm-release-oauth-proxy --chart oauth2-proxy --interval 10s --target-namespace oauth2-proxy --source HelmRepository/oauth-proxy --values ../../../proxmox-ubuntu-k8s/helm/oauth2-proxy/values.yaml --export > helm-release-oauth-proxy.yaml

### Atlantis ###

flux create source helm atlantis --url https://kubernetes-charts.storage.googleapis.com  --timeout 10s --export > source-helm-atlantis.yaml

flux create helmrelease helm-release-atlantis --chart atlantis --interval 10s --target-namespace atlantis --source HelmRepository/atlantis --values ../../../proxmox-ubuntu-k8s/helm/atlantis/values.yaml --export > helm-release-atlantis.yaml

### Vault ###

flux create source helm vault --url https://helm.releases.hashicorp.com  --timeout 10s --export > source-helm-vault.yaml

flux create helmrelease helm-release-vault --chart vault --interval 10s --target-namespace vault-system --source HelmRepository/vault --values ../../../proxmox-ubuntu-k8s/helm/vault/values.yaml --export > helm-release-vault.yaml
### Positiz ###

flux create source helm bitnami-postiz --url=oci://ghcr.io/gitroomhq/postiz-helmchart/charts --interval=10m --namespace=flux-system --export > source-helm-postiz.yaml

flux create helmrelease postiz --source=HelmRepository/bitnami-postiz --chart=postiz-app --interval 10s --target-namespace postiz-system --values  ../../../proxmox-ubuntu-k8s/helm/postiz/values.yaml  --export > helm-release-postiz.yaml

### Rancher ###

flux create source helm rancher --url https://releases.rancher.com/server-charts/stable  --timeout 10s --export > source-helm-rancher.yaml

flux create helmrelease helm-release-rancher --chart rancher --chart-version 2.11.2 --interval 10s --target-namespace rancher-system --source HelmRepository/rancher --values ../../../proxmox-ubuntu-k8s/helm/rancher/values.yaml --export > helm-release-rancher.yaml

### cert-manager ###

flux create source helm cert-manager --url https://charts.jetstack.io  --timeout 10s --export > source-helm-cert-manager.yaml

flux create helmrelease helm-release-cert-manager --chart cert-manager  --chart-version 1.17.2 --interval 10s --target-namespace cert-manager --source HelmRepository/cert-manager --values ../../../proxmox-ubuntu-k8s/helm/cert-manager/values.yaml --export > helm-release-cert-manager.yaml

### Minecraft ###

flux create source helm minecraft --url https://itzg.github.io/minecraft-server-charts/  --timeout 10s --export > source-helm-minecraft.yaml

flux create helmrelease helm-release-minecraft --chart Minecraft --chart-version 4.26.3 --interval 10s --target-namespace minecraft --source HelmRepository/minecraft --values ../../../proxmox-ubuntu-k8s/helm/minecraft/values.yaml --export > helm-release-minecraft.yaml

### Mestrics-server ####

flux create source helm metrics-server --url https://kubernetes-sigs.github.io/metrics-server/ --timeout 10s --export > source-helm-metrics-server.yaml

flux create helmrelease helm-release-metrics-server --chart metrics-server --chart-version 3.12.2 --interval 10s --target-namespace metrics-server --source HelmRepository/metrics-server --values ../../../proxmox-ubuntu-k8s/helm/metrics-server/values.yaml --export > helm-release-metrics-server.yaml

### Odoo ###
flux create source helm bitnami --url=oci://registry-1.docker.io/bitnamicharts --interval=10m --namespace=flux-system --export > source-helm-odoo.yaml

flux create helmrelease odoo --source=HelmRepository/bitnami --chart=odoo --interval 10s --target-namespace odoo-system --chart-version=28.2.4 --values  ../../../proxmox-ubuntu-k8s/helm/odoo/values7.yaml  --export > helm-release-odoo.yaml

flux create kustomization  kustomize-odoo --source GitRepository/metalb-git --prune true --interval 10s --target-namespace odoo-system --path manifests/apps/odoo --export > kustomize-git-odoo.yaml

### Positiz ###
flux create source helm bitnami-postiz --url=oci://ghcr.io/gitroomhq/postiz-helmchart/charts --interval=10m --namespace=flux-system --export > source-helm-postiz.yaml

flux create helmrelease postiz --source=HelmRepository/bitnami-postiz --chart=postiz-app --interval 10s --target-namespace postiz-system --values  ../../../proxmox-ubuntu-k8s/helm/postiz/values.yaml  --export > helm-release-postiz.yaml

### Rancher ###
flux create source helm rancher --url https://releases.rancher.com/server-charts/stable  --timeout 10s --export > source-helm-rancher.yaml

flux create helmrelease helm-release-rancher --chart rancher --chart-version 2.11.2 --interval 10s --target-namespace rancher-system --source HelmRepository/rancher --values ../../../proxmox-ubuntu-k8s/helm/rancher/values.yaml --export > helm-release-rancher.yaml

### cert-manager ###

flux create source helm cert-manager --url https://charts.jetstack.io  --timeout 10s --export > source-helm-cert-manager.yaml

flux create helmrelease helm-release-cert-manager --chart cert-manager  --chart-version 1.17.2 --interval 10s --target-namespace cert-manager --source HelmRepository/cert-manager --values ../../../proxmox-ubuntu-k8s/helm/cert-manager/values.yaml --export > helm-release-cert-manager.yaml

### Minecraft ###

flux create source helm minecraft --url https://itzg.github.io/minecraft-server-charts/  --timeout 10s --export > source-helm-minecraft.yaml

flux create helmrelease helm-release-minecraft --chart Minecraft --chart-version 4.26.3 --interval 10s --target-namespace minecraft --source HelmRepository/minecraft --values ../../../proxmox-ubuntu-k8s/helm/minecraft/values.yaml --export > helm-release-minecraft.yaml

### Mestrics-server ####

flux create source helm metrics-server --url https://kubernetes-sigs.github.io/metrics-server/ --timeout 10s --export > source-helm-metrics-server.yaml

flux create helmrelease helm-release-metrics-server --chart metrics-server --chart-version 3.12.2 --interval 10s --target-namespace metrics-server --source HelmRepository/metrics-server --values ../../../proxmox-ubuntu-k8s/helm/metrics-server/values.yaml --export > helm-release-metrics-server.yaml

### glasskube ###

flux create source helm glasskube-operator --url  https://charts.glasskube.eu/ --timeout 10s --export > source-helm-glasskube-operator.yaml

flux create helmrelease helm-release-glasskube --chart glasskube-operator --chart-version 0.12.2 --interval 10s --target-namespace glasskube-operator --source HelmRepository/glasskube-operator --values ../../../proxmox-ubuntu-k8s/helm/glasskube/values.yaml --export > helm-release-glasskube-operator.yaml

### ERPNext ###

flux create source helm erpnext --url  https://helm.erpnext.com/ --timeout 10s --export > source-helm-erpnext.yaml

flux create helmrelease helm-release-erpnext --chart erpnext --chart-version 7.0.209 --interval 10s --target-namespace erpnext-system --source HelmRepository/erpnext --values ../../../proxmox-ubuntu-k8s/helm/erpnext/values.yaml --export > helm-release-erpnext.yaml

### CTFD ###

flux create source git ctfd-git --url https://github.com/bensalah-nabil/CTFd --branch main --timeout 10s --export > source-git-ctfd.yaml

flux create kustomization  kustomize-ctf --source GitRepository/ctfd-git --prune true --interval 10s --target-namespace ctfd-system --path manifests/ --export > kustomize-git-ctd.yaml

### Blog ###

flux create source git blog-git --url https://github.com/bensalah-nabil/blog --branch main --timeout 10s --export > source-git-blog.yaml

flux create kustomization  kustomize-blog --source GitRepository/blog-git --prune true --interval 10s --target-namespace blog-system --path manifests/ --export > kustomize-git-blog.yaml

### ImagePolicy ###

flux create image repository blog --image=ghcr.io/tur-pve/rblog --interval=5m --export > blog-registry.yaml

flux create image policy blog --image-ref=blog --select-semver=main --export > blog-policy.yaml
