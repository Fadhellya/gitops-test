# GitOps ArgoCD Sample Setup

Dokumentasi singkat untuk membuat **ArgoCD Application** di OpenShift dan memberikan akses cluster-admin untuk service account `openshift-gitops-argocd-application-controller`.

---

## 1. Berikan Cluster-Admin ke Service Account

Service Account berikut perlu diberikan role `cluster-admin`:

```bash
oc adm policy add-cluster-role-to-user cluster-admin \
  -z openshift-gitops-argocd-application-controller -n openshift-gitops

2. Ambil Password Admin ArgoCD

Untuk login ke ArgoCD, ambil password admin dari secret:

argoPass=$(oc get secret openshift-gitops-cluster -n openshift-gitops -o jsonpath='{.data.admin\.password}' | base64 -d)
echo $argoPass


3. Contoh ArgoCD Application

Berikut contoh manifest ArgoCD Application untuk repository GitOps:
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: test-gitops
  namespace: openshift-gitops
spec:
  destination:
    namespace: demo
    server: https://kubernetes.default.svc
  source:
    path: argo
    repoURL: https://github.com/Fadhellya/gitops-test.git
    targetRevision: main
  sources: []
  project: default
  syncPolicy:
    automated:
      prune: true
      selfHeal: false
    syncOptions:
      - CreateNamespace=true

