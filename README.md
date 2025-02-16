# CDE-VDT-2024-Phase-2

This repository is a comprehensive guide on building a Cloud Development Environment (CDE) using Kubernetes. It covers everything from the basics of Kubernetes to advanced topics like custom controllers, custom resources, operators, Eclipse Che integration, and deploying the complete solution on a public Kubernetes cluster.

## Topics Covered

- **Introduction to Kubernetes:**  
  Understand Kubernetes architecture, pod lifecycle, and core concepts.  
  See: [introduction-to-k8s.md](./introduction-to-k8s.md)

- **Kubernetes Controllers:**  
  Learn about the fundamentals of Kubernetes controllers, including how they are designed to reconcile the desired state with the actual state of the cluster.  
  See: [controller-k8s.md](./controller-k8s.md)

- **Kubebuilder & Custom Controllers:**  
  Explore how to extend Kubernetes with custom controllers using Kubebuilder. This section covers scaffolding, logging in the Reconcile function, and adding custom logic.  
  See: [kubebuilder-controller.md](./kubebuilder-controller.md)

- **Adding Custom Resources:**  
  Discover how to define and use custom resources to simplify complex deployments, such as deploying a PostgreSQL database in Kubernetes as a custom resource.  
  See: [adding-custom-resources-to-k8s.md](./adding-custom-resources-to-k8s.md)

- **Operators and DevWorkspace Operator:**  
  Understand Operators and how they manage the lifecycle of developer workspaces, enabling configurable and reproducible environments.  
  See: [devworkspace-operator.md](./devworkspace-operator.md)

- **Eclipse Che:**  
  Learn about Eclipse Che, a Kubernetes-native integrated developer environment, its features, and how to deploy it for cloud-native development.  
  See: [eclipse-che.md](./eclipse-che.md)

- **Deploying CDE on a Public Kubernetes Cluster:**  
  Follow a step-by-step guide to deploy your Cloud Development Environment on a public Kubernetes cluster while configuring networking, TLS certificates, and OIDC authentication.  
  See: [deloy-cde-on-k8s-cluster-public.md](./deloy-cde-on-k8s-cluster-public.md)

## Repository Structure

- **README.md:** This file explaining the overall project and providing links to the detailed guides.
- **introduction-to-k8s.md:** An introduction and detailed explanation of Kubernetes concepts.
- **controller-k8s.md:** An overview of Kubernetes controllers, including their design and event-based reconciliation.
- **kubebuilder-controller.md:** A hands-on guide to building custom controllers using Kubebuilder.
- **adding-custom-resources-to-k8s.md:** A guide on defining and deploying custom resources in Kubernetes.
- **devworkspace-operator.md:** Instructions on using the DevWorkspace Operator to manage developer workspaces.
- **eclipse-che.md:** Information on deploying Eclipse Che and exploring its cloud-native IDE features.
- **deloy-cde-on-k8s-cluster-public.md:** Step-by-step deployment guide to run a CDE on a public Kubernetes cluster.
- **assets/**: Directory containing images and other supporting files referenced in the markdown documents.

## How To Get Started

1. **Learn the Basics:**  
   Start with [introduction-to-k8s.md](./introduction-to-k8s.md) to build a strong foundation in Kubernetes.

2. **Understand Controllers:**  
   Read [controller-k8s.md](./controller-k8s.md) to understand how Kubernetes controllers work and their role in reconciling state.

3. **Extend Kubernetes:**  
   Dive into [kubebuilder-controller.md](./kubebuilder-controller.md) and [adding-custom-resources-to-k8s.md](./adding-custom-resources-to-k8s.md) to learn how to build custom controllers and resources.

4. **Set Up Developer Workspaces:**  
   Follow along with [devworkspace-operator.md](./devworkspace-operator.md) and [eclipse-che.md](./eclipse-che.md) to set up and run cloud-native developer environments.

5. **Deploy Your CDE:**  
   Finally, use [deloy-cde-on-k8s-cluster-public.md](./deloy-cde-on-k8s-cluster-public.md) as your guide to deploy the entire cloud development environment on a public Kubernetes cluster.

## Conclusion

This repository gathers a set of practical exercises and guides aimed at helping you build a robust cloud development environment using Kubernetes. Whether you're new to Kubernetes or looking to extend it with custom controllers and operators, these resources provide a solid foundation for modern cloud-native development.
