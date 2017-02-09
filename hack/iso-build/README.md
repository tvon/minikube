# Build container for minikube-iso

This uses a `golang:1.6`` base image to boostrap an environment capable of
compiling `minikube-iso`.  I picked 1.6 because I didn't put much thought into
it, it should perhaps be something more recent.

## Caveats

* Container user is root which will leave you with a bunch of things owned by root in your project.
* Container does not do anything smart with the buildroot data, a volume container would likely be useful.
* The `Makefile` is a hack.
* Golang conventions were likely missed or ignored.

## Usage

From the root of the `minikube` checkout:

```
make -C hack/iso-build image
make -C hack/iso-build minikube_iso
```

Other targets have been added for convenience of running them through the container.
