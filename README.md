kasih cluster-admin untuk sa openshift-gitops-argocd-application-controller <br>
argoPass=$(oc get secret openshift-gitops-cluster -n openshift-gitops -o jsonpath='{.data.admin\.password}' | base64 -d)
