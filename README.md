# CI/CD Sockshop 

## Overall Plan
- Helm-based ArgoCD install with metrics ON
- 2 ArgoCD projects with scoped permissions (1x for platform, 1x for workload)
- app-of-apps to discover applications (including itself)
- 6-10 applications (one each deployment in sock shop sync waves so infra (ns/CRDs))
- secrets handled via AVP+AzureKeyVault
- kube-prometheus-stack + ServiceMonitors + an alert rule (ex: app out of sync) + grafana dashboards
- README with 1 command bootstrap and screenshots (need to be able to install ArgoCD for the first time manually)



TO DO LIST:

- X BootStrap cmds
- X AppProjects
- X ApplicationSet (for SockShop microservices/applications)
- ? ArgoCD (fully customized in Repo) -- 
    app.yaml(complete) / values.yaml(In-Progress)
- O AVP + KeyVault
- O Monitoring
- O README with bootstrap + screenshots



# BOOTSTRAP CMDS
### Create Namespace
`kubectl apply ns argocd`

### Create Minimal ArgoCD just to get CRDs/controller running - https://argo-cd.readthedocs.io/en/stable/
`kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml`

### Create AppProject for ArgoCD Application and App-of-Apps ApplicationSet
`kubectl apply -n argocd -f https://github.com/rocklobster1618/cicd-sockshop/platform/projects/platform.yaml`

### Create AppProject for all SockShop Microservices
`kubectl apply -n argocd -f https://github.com/rocklobster1618/cicd-sockshop/platform/projects/workload.yaml`

### Create Self-Managing ArgoCD Application - https://artifacthub.io/packages/helm/argo/argo-cd
`kubectl apply -n argocd -f https://github.com/rocklobster1618/cicd-sockshop/platform/argocd/app.yaml`

### Create App-of-Apps ApplicationSet for SockShop Microservices
`kubectl apply -n argocd -f https://github.com/rocklobster1618/cicd-sockshop/platform/app-of-apps/app.yaml`
