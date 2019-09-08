# Test Cluster Flux/Configs

Config files for kubernetes and flux.

Flux is deployed by fluxctl when the masters initialise, and will poll this Github repository for
changes. When a change is detected, all the configs in `kubernetes/` will be applied to the cluster.
