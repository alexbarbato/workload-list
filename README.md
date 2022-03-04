# Tanzu App Workload Importer

## Application Workload Repo Reconciler

## Problem Description
Realistically development teams will likely not be allowed to imperatively add workloads to build or run clusters. They will probably need to make some PR to a repo and have it approved to be "automatically" applied.

Beyond that there is the day 2 problems of a workload definition - what if a new service claim is added? A different supply chain targeted? A change in some git repo? etc.

Workloads do not by default have a reconciliation loop today to stay current.

## Solution
Deploy a kapp that instructs the kapp-controller to ensure all workloads defined in a given git-repo will be deployed automatically to the TAP cluster and then continuously reconciled.

Now when new workloads are to be added to the cluster or changed, the only requirement is that their definitions files are checked into this repo.


## Usage
Fork this repo and update your workload-list.yaml to refer to your fork.

Use kapp to continuously deploy reconciling this workload repo.

Place any desired application workload definitions in the _workloads_ subfolder

``` 
# For now you need to go through the two yaml files below and change the namespaces to your configured working namespace
kubectl apply -f ./gitops-service-account.yaml
kapp deploy -a workload-list -f ./workload-list.yaml
```

## Bonus
In theory you could use the _clusters_ folder to do store your TAP installation manifests and use this as a place to store your entire TAP installation, to include workloads.