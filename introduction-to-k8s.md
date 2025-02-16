# Kubernetes

## 1. What is Kubernetes?

### 1.1 Introduction to Kubernetes

<div align="center">
  <img width="1000" src="./images/k8s.png" alt="Kubernetes">
</div>

<div align="center">
  <i><a href="https://kubernetes.io/vi/docs/concepts/overview/what-is-kubernetes">
         Introduction to Kubernetes
    </a></i>
</div>

Kubernetes is an open-source, portable, and scalable platform for managing containerized applications and services. It simplifies application deployment and configuration automation. Kubernetes has a vast and rapidly growing ecosystem, with many available tools, services, and community supports.

The name “Kubernetes” originates from Greek and means "helmsman" or "pilot." Google open-sourced Kubernetes in 2014, building on over a decade and a half of experience running large-scale workloads in production and incorporating the best ideas and practices from the community.

**Looking Back in Time**

Let’s explore why Kubernetes is so valuable by taking a look back at previous deployment eras.

<div align="center">
  <img width="1000" src="./images/k8s-2.png" alt="Kubernetes">
</div>

**_The Era of Traditional Deployment:_**  
Originally, applications were run on physical servers. There was no clear method for delineating resource boundaries among applications on the same physical server, which often led to resource allocation issues. For instance, if multiple applications ran on a single physical server, one might consume the majority of the resources while others suffered from reduced performance. One solution was to run each application on a separate physical server; however, this approach was inefficient because resources were underutilized and maintaining numerous physical servers was costly.

**_The Era of Virtualization:_**  
Virtualization was introduced as an alternative solution. It allows multiple virtual machines (VMs) to run on the same physical server CPU. Virtualization provides isolation between applications running in different VMs and enhances security by ensuring that one application's data cannot be freely accessed by another.

Virtualization improves resource utilization on physical servers, eases scalability by enabling quick addition or updates to applications, reduces hardware costs, and more. With virtualization, a pool of physical resources acts as a cluster of readily available virtual machines. Each VM is a fully functional computer running its own operating system atop virtualized hardware.

**_The Era of Containers:_**  
Containers are similar to VMs but offer an additional level of isolation by sharing the host’s operating system. This makes containers lightweight. Like VMs, a container has its own filesystem, CPU, memory, and process space. Because they are decoupled from the underlying infrastructure, containers are highly portable across different clouds or OS distributions.

Containers have become popular because they offer many benefits, including:

- **Agile Application Development & Deployment:** It is faster and more efficient to create container images compared to VM images.
- **Continuous Integration & Continuous Deployment:** Frequent and reliable builds and deployments are possible with easy rollbacks.
- **Dev and Ops Separation:** Applications are built into container images during build/release rather than at deployment—decoupling them from the infrastructure.
- **Enhanced Observability:** Beyond operating system metrics, you can monitor application health and other signals.
- **Consistent Environments:** The same container can run on a developer's laptop, in testing, and in production.
- **Portability:** Containers can run on various operating systems like Ubuntu, RHEL, CoreOS, on-premises, or in cloud environments.
- **Centralized Application Management:** It abstracts running an operating system on virtual hardware to running an application on logical resources.
- **Elastic Micro-Services:** Applications are split into smaller, independent services that can scale and be managed separately rather than as a monolithic application.
- **Resource Isolation and Efficient Utilization:** Leading to predictable performance and optimal use of resources.

### 1.2 When Should You Use Kubernetes?

- When you need rapid system scaling and are already using containers (such as Docker).
- For services that require deploying a large number of containers.
- When your project demands future scalability.

### 1.3 What Problems Does Kubernetes Solve?

Running applications in containers solves many issues, but imagine managing over a thousand containers—how do you know which container belongs to which application or project? And if you need to scale an application by running multiple containers, how do you route user requests to the correct containers? What if a physical server fails and can no longer operate? Kubernetes addresses these challenges by:

- Managing a large number of Docker hosts.
- Scheduling containers.
- Performing rolling updates.
- Scaling and auto-scaling.
- Monitoring the lifecycle and health status of containers.
- Self-healing by detecting and correcting failures automatically.
- Providing service discovery.
- Balancing load.
- Handling data management, worker nodes, and logs.
- Treating infrastructure as code.
- Facilitating integration and scalability with other systems.

## 2. Kubernetes Architecture

<div align="center">
  <img width="1000" src="./images/k8s-3.png" alt="Kubernetes">
</div>

A Kubernetes system consists of two main components: the **Control Plane** (or Master Node) and the **Data Plane** (or Worker Node). The Master Node handles system management and control tasks, while the Worker Nodes run the workloads. Pods are created and executed on the Worker Nodes.

On the Master Nodes, there are four main components:

- **etcd:** A highly available and consistent key-value database that stores all the configuration data of the system.
- **Controllers:** Background processes running on the Master Node that continuously monitor the state of the Kubernetes cluster via APIs and make necessary adjustments to reach the desired state.
- **kube-apiserver:** The core component of the Kubernetes Master, which exposes HTTP APIs. It enables communication between end users and various components in the Kubernetes cluster and allows users to retrieve information (e.g., Pods, Namespaces, Services) via kubectl or direct REST API calls.
- **kube-scheduler:** The default service that assigns Pods to run on specific nodes. It examines Pods that have been created but not yet scheduled, determines which nodes meet the specified requirements, and assigns the Pods to the most suitable nodes. If no node can satisfy the requirements, the Pod remains unscheduled until an appropriate node becomes available.

On the Worker Nodes, the primary components include:

- **kubelet:** Acts as the node agent by registering the node with the Kubernetes cluster, receiving Pod deployment instructions from the API server, and ensuring the containers run properly. Note that kubelet only manages containers that Kubernetes creates.
- **kube-proxy:** A network proxy that runs on every node, managing network rules to allow communication to the Pods from within or outside the cluster.
- **Container Runtime:** The component responsible for running containers. Common container runtimes supported by Kubernetes include Docker and Containerd.

### 2.1 Pod Lifecycle

**Creating a Pod**

When a new Pod is created, the following sequence of events and components is involved:

<div align="center">
  <img width="1000" src="./images/k8s-4.png" alt="Kubernetes">
</div>

Detailed flow for creating a Pod:

1. When you create a new Pod (typically by applying a YAML file with kubectl), the command sends a request to the API server to create the Pod based on the detailed description in the YAML.
2. The API server validates the YAML file. If there are no errors, it writes the Pod’s details into etcd, the key-value database described earlier. At this moment, the system has recorded that a new Pod should be created. After the data is stored, the API server responds to the client, confirming the creation of the Pod.
3. Next, the scheduler monitors the API server for newly created Pods that have not yet been assigned to any node. Upon detecting such a Pod, the scheduler retrieves its information and finds a node (e.g., node1) that meets the Pod’s requirements, then updates the Pod’s specification to indicate that it should run on node1. This update is sent back to the API server.
4. The API server receives the assignment information for the new Pod, updates etcd accordingly, and marks the Pod as "Bound" to a node.
5. The kubelet on node1, which continuously monitors for Pods in the "Bound" state scheduled to run on it, detects the new Pod. It then retrieves the necessary information for the Pod and launches it as one or more containers on node1, subsequently updating the Pod’s status back to the API server.
6. Finally, when the API server receives the status update from kubelet on node1, it stores the updated information in etcd and sends an acknowledgement back to the kubelet indicating that the update has been accepted.

**Deleting a Pod**

The process for deleting a Pod occurs as follows:

<div align="center">
  <img width="1000" src="./images/k8s-5.png" alt="Kubernetes">
</div>

Detailed flow for deleting a Pod:

1. The user issues a command to delete a Pod.
2. The corresponding Pod object in Kubernetes is updated to a “dead” state after a period known as the grace period.
3. Several actions occur concurrently:
   - The Pod appears in a "Terminating" state when viewed from the client.
   - The kubelet detects that the Pod is marked as Terminating and begins shutting down the Pod’s processes.
   - The endpoint controller monitors the deletion status of the Pod to remove it from any endpoints it serves.
4. If the Pod defines a preStop hook, that hook is executed inside the Pod. If the preStop hook is still running when the grace period expires, step (2) is restarted with an additional grace period of 2 seconds. (Learn more about [Container Hooks here](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/).)
5. The processes inside the Pod first receive a terminate (TERM) signal. Once the grace period ends, all remaining processes within the Pod are forcibly killed with a SIGKILL signal. Finally, the kubelet finishes deleting the Pod by informing the API server and setting the grace period to 0, meaning the Pod is removed immediately and will no longer be visible to clients.
