# [back-stack](https://backstack.dev/intro/)

## Harmonizing Development Practices

The BACK Stack orchestrates a robust suite of open-source tools, each tackling a critical pain point:

- [Backstage](https://github.com/backstage/backstage#getting-started:) This user-friendly developer portal centralizes access to essential tools and services, streamlining workflows and boosting collaboration.
- [Argo CD](https://github.com/argoproj/argo-cd): Embracing the GitOps philosophy, it automates continuous delivery, ensuring seamless deployments and perfect synchronization between applications and their codebase.
- [Crossplane](https://github.com/crossplane/crossplane): Forget juggling disparate cloud providers. Crossplane is the universal control plane, automating infrastructure provisioning with unmatched efficiency and flexibility.
- [Kyverno](https://github.com/kyverno/kyverno/): Security is woven into the fabric of development. Kyverno enforces policies, calculates compliance scores, and automates governance, safeguarding your applications from the ground up.

```sh
kind delete clusters backstage-demo
kind create cluster --config kind-backstage-demo.yaml

kubectl cluster-info --context kind-backstage-demo
    Kubernetes control plane is running at https://127.0.0.1:51988
    CoreDNS is running at https://127.0.0.1:51988/api/v1/namespaces/kube-system/services/kube-dns:dns/proxy

kubectl version
Client Version: v1.30.1
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3
Server Version: v1.33.2
WARNING: version difference between client (1.30) and server (1.33) exceeds the supported minor version skew of +/-1    
```

## Getting Started

### Argo CD

```sh
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
kubectl port-forward svc/argocd-server -n argocd 8080:443

kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo

[System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String((kubectl get secret -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}")))
```
