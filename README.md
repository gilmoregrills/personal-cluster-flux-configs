# Test Cluster Flux/Configs

Config files for kubernetes and flux.

Flux is deployed according to the configuration in `weave_flux.yml`, and will poll this Github repository for
changes. When a change is detected, all the configs in `kubernetes/` will be applied to the cluster.

# Deploying flux:

#### To install, from the root of the repo run:

`helm install --name flux --namespace robin -f weave_flux.yml weaveworks/flux`

#### And to uninstall:

`helm del --purge flux`

#### If you get an error saying the default service account can't create resources in the given namespace just run:

`kubectl create serviceaccount --namespace kube-system tiller`

`kubectl create clusterrolebinding tiller-cluster-rule --clusterrole=cluster-admin --serviceaccount=kube-system:tiller`

`kubectl patch deploy --namespace kube-system tiller-deploy -p '{"spec":{"template":{"spec":{"serviceAccount":"tiller"}}}}'`

#### The flux deployment's public SSH key must also be added this repository as a deploy key, get the key by running:

`fluxctl --k8s-fwd-ns=robin identity`