Ref: https://github.com/StephenGrider/multi-k8s/tree/master/k8s

1. make sure to have no special character in the docker hub account's password - 
easier to save it in an env on travis

Helm (on google cloud terminal)
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 > get_helm.sh
chmod 700 get_helm.sh
./get_helm.sh

helm repo add stable https://kubernetes-charts.storage.googleapis.com/
helm install ocular-nginx-ingress stable/nginx-ingress --set rbac.create=true


tracil cli logn and creating encrypted service-acount.json.enc from gcloud 
https://docs.travis-ci.com/user/encrypting-files/

make sure to add --com to bith this commands from cli:
travis login --com
travis encrypt-file service-account.json -r ocular-hub/ocular --com
rm service-account.json 

================
didars-air:~ didar.alam$ travis login --com



 >travis env list

 How to create cert-manager:
 ==========================
 https://cert-manager.io/docs/installation/kubernetes/

 1. make sure GKE cluster kubernest versuon is 1.15 or above
 2. $ kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v0.15.1/cert-manager.yaml
 3. kubectl create clusterrolebinding cluster-admin-binding \
    --clusterrole=cluster-admin \
    --user=$(gcloud config get-value core/account) 
 4. kubectl create namespace cert-manager
 5. helm repo add jetstack https://charts.jetstack.io
 6. helm repo update
 7. kubectl apply --validate=false -f https://raw.githubusercontent.com/jetstack/cert-manager/v0.13.0/deploy/manifests/00-crds.yaml

  -Note that this menifest url above is found at: https://github.com/jetstack/cert-manager/issues/2540
 8. (for help 2.x):
 helm install \
  --name cert-manager \
  --namespace cert-manager \
  --version v0.15.1 \
  jetstack/cert-manager

  Verify:  helm ls --all cert-manager;
  $ kubectl get pods --namespace cert-manager
  If it shows a failed statues : you need to delete and re-create/troubl shoot

  there is an example test issuer/certificate config for test in that link https://cert-manager.io/docs/installation/kubernetes/
  So test if certificate generation works! 

  https://cert-manager.io/docs/tutorials/acme/http-validation/


  kubectl describe certificate okular-us





