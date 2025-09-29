kasih cluster-admin untuk sa openshift-gitops-argocd-application-controller <br>
argoPass=$(oc get secret openshift-gitops-cluster -n openshift-gitops -o jsonpath='{.data.admin\.password}' | base64 -d) <br>
#Sample
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

