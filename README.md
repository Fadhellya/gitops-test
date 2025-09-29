# GitOps ArgoCD Sample Setup

Dokumentasi singkat untuk membuat **ArgoCD Application** di OpenShift dan memberikan akses cluster-admin untuk service account `openshift-gitops-argocd-application-controller`.

---

## 1. Berikan Cluster-Admin ke Service Account

Service Account berikut perlu diberikan role `cluster-admin`:

```bash
oc adm policy add-cluster-role-to-user cluster-admin \
  -z openshift-gitops-argocd-application-controller -n openshift-gitops
