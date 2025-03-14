#### [Back](./README.md)

# K8 Networking

Kubernetes provides a networking model that allows pods to communicate with each other and with external services. The networking model is based on the following principles:

1. **Each pod has its own IP address:** Pods are assigned an IP address from a pod network.

2. **Pods can communicate with each other:** Pods can communicate with each other using their IP addresses.

3. **Services provide a network identity:** Services provide a network identity and load balancing for accessing pods.

## Network Components:

1. **Pod Network:** A pod network is a virtual network that allows pods to communicate with each other.

2. **Service Network:** A service network is a virtual network that provides access to services.

3. **Cluster Network:** A cluster network is a physical network that connects the nodes in a Kubernetes cluster.

4. **Node Network:** A node network is a physical network that connects the pods running on a node.

## Networking Modes:

1. **Host Networking:** In host networking mode, pods use the host's network stack and IP address.

2. **Bridge Networking:** In bridge networking mode, pods use a virtual bridge to communicate with each other.

3. **Overlay Networking:** In overlay networking mode, pods use a virtual network that overlays the physical network.

## Networking Tools:

1. **kubectl:** kubectl is the command-line tool for interacting with Kubernetes clusters.

2. **Calico:** Calico is a networking tool that provides a flexible and scalable networking solution for Kubernetes.

3. **Flannel:** Flannel is a networking tool that provides a simple and scalable networking solution for Kubernetes.

4. **Cilium:** Cilium is a networking tool that provides a high-performance and scalable networking solution for Kubernetes.

