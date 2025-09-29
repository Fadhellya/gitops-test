kasih cluster-admin untuk sa openshift-gitops-argocd-application-controller
argoPass=$(oc get secret openshift-gitops-cluster -n openshift-gitops -o jsonpath='{.data.admin\.password}' | base64 -d)
