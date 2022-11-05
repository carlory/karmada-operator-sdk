[![License](http://img.shields.io/:license-apache-blue.svg)](http://www.apache.org/licenses/LICENSE-2.0.html)

# Karmada Operator SDK

Karmada Operator SDK is a framework for building [Karmada](karmada) APIs using custom resource definitions (CRDs).

Similar to kubernetes development frameworks such as [Kubebuilder](kubebuilder) and [Operator SDK](operator-sdk), This project increases velocity and reduces the complexity managed by developers for rapidly building and publishing Karmada APIs in Go. It builds on top of the canonical techniques used to build the core Karmada APIs to provide simple abstractions that reduce boilerplate and toil.

This project does not exist as an example to copy-paste, but instead provides powerful libraries and tools to simplify building and publishing Karmada APIs from scratch.

## Quick Start

// TBD

## Motivation

Operators are a [design pattern](operator-pattern) make public in a 2016 CoreOS [blog](coreos-blog) post. The goal of an Operator is to put operational knowledge only resided in the minds of administrators, various combinations of shell scripts or automation software like Ansible. I was outside of your Kuberentes cluster and hard to integrate. With Operators, CoreOS changed that.

Operators implement and automate common Day-1 (installation, configuration, etc) and Day-2 (re-configuration, update, backup, failover, restore, etc.) activities in a piece of software running inside your Kubernetes cluster, by integrating natively with Kubernetes concepts and APIs. We call this a Kubernetes-native application. As a commpany's Kuberentes use matures, the next step is a mulit-cluster implementation. Instead of running an application on a single cluster, it expaneds and unifies its distributed architecture across multiple clusters. This is where Karmada comes in. 

Leveraging [Kubebuilder](kubebuilder) or [OLM Operator SDK](operator-sdk), it is relatively easy to build an operator to manage and scale a Kuberentes-native application right out of the box. However, the multi-cluster application architecture comes with complexitites that are not addressed by the existing frameworks. Developers need to know a things or two about the details of Karmada and Kubernetes to create a stateful application across multiple clusters. It's not easy to build a Karmada-native application from scratch.

In order to facilitate easily building Karmada APIs and tools using the canonical approach, this framework provides a collection of Karmada development tools to minimize toil.

This project attempts to facilitate the following developer workflow for building APIs

1. Create a new project directory
2. Create one or more resource APIs as CRDs and then add fields to the resources
3. Implement reconcile loops in controllers and watch additional resources
4. Test by running against a cluster (self-installs CRDs and starts controllers automatically)
5. Update bootstrapped integration tests to test new fields and business logic
6. Build and publish a container from the provided Dockerfile

## Architecture

// TBD

## Concepts

[Kubernetes Operators](operator-pattern) build upon two central Kubernetes cencepts: Resources and Controllers. Resources are the objects that the operator manages. Controllers are the commponents that operators watch the resources and make changes to them. 

Karmada Operators, by their nature, are application-specific, so the hard work is going to be encoding all the application operational domain knowledge into a reasonable configuration resource and control loop. There are some common patterns that we have found while building operators. It is important to understand these concepts before building a Karmada-native application, especially when you are building a stateful application, such as a middleware or database.

Different from the single cluster architecture of traditional application , the controllers of multi-cluster application architecture upon the Karmada platform is splited into two components to reconcile the resources in the member clusters and the resources in the karmada control plane. The controllers in the member clusters are called `Member Controller Manager` and the controllers in the control plane are called `Controlplane Controller Manager`.

### Custom Resource Definition

// TBD

### Controlplane Controller Manager

// TBD

### Member Controller Manager (aka Agent)

// TBD

## Scope

Building APIs using CRDs, Controllers and Admission Webhooks.

## What's Next

See [RoadMap](ROADMAP.md) for details.

More will be coming soon. Welcome to [open an issue](open-an-issue) and [propose a PR](propose-a-pr). 🎉🎉🎉

## Contributors

<a href="https://github.com/firefly-io/karmada-operator-sdk/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=firefly-io/karmada-operator-sdk" />
</a>

Made with [contrib.rocks](https://contrib.rocks).

## License

Operator SDK is under Apache 2.0 license. See the [LICENSE](LICENSE) file for details.

[karmada]: https://github.com/karamda-io/karmada.git
[operator-sdk]: https://github.com/operator-framework/operator-sdk.git
[kubebuilder]: https://github.com/kubernetes-sigs/kubebuilder.git
[open-an-issue]: https://github.com/firefly-io/karmada-operator-sdk/issues
[propose-a-pr]: https://github.com/firefly-io/karmada-operator-sdk/pulls
[coreos-blog]: https://web.archive.org/web/20170129131616/https://coreos.com/blog/introducing-operators.html
[operator-pattern]: https://kubernetes.io/docs/concepts/extend-kubernetes/operator/