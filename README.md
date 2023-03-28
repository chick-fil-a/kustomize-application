# kustomize-application

Example `kustomize` feeder repository for applications.

## Resources

* Chick-fil-A Tech Blog: <>

## Introduction

When we started migrating DXE services from Elastic Beanstalk to our new EKS-based platform in 2018, there were only a limited number of folks in the organization that had experience developing and maintaining Kubernetes manifests. It was clear from the beginning that we didn't want each team writing the entirety of their own manifests. This would have immediately created a barrier of entry to the new platform, in addition to a confusing mess of requirements, tooling, and team silos.

We decided to build a set of base manifests for each of our common application types. Teams could pull in these manifests and "patch-in" any changes for their particular application using kustomize. This made the learning curve we were asking teams to climb less daunting: folks didn't need to write a (potentially gigantic) pile of yaml to deploy their applications to Kubernetes. Rather, they just needed to learn how patch the base manifests.

So, what does this feeder repository look like? Well, it looks like this repo!

## Usage

You can use the base manifests for a given application by referencing this application repository in their own `kustomization.yaml` file. For example, to pull the base manifests for a Python API:

```yaml
resources:
- https://github.com/chick-fil-a/kustomize-application/python-api?ref=main

patches:
- target:
    kind: Deployment
  path: patches/deploy.yaml

...
```

The key is the resources list: the first item (and only item in our example) references the base manifests from `kustomize-application`. There are additional examples in the `examples`  directory.
