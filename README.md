![Check Kubernetes documentation links](https://github.com/leandrocostam/cka-preparation-guide/workflows/Check%20Kubernetes%20documentation%20links/badge.svg)

# Certified Kubernetes Administrator (CKA) - V1.35

The objective of this repository is help you for taking the Certified Kubernetes Administrator (CKA) exam using online resources, especially using resources from [Kubernetes Official Documentation](https://kubernetes.io).

The references were selected for the [Exam Curriculum 1.35](https://github.com/cncf/curriculum/blob/008b73c0ac99d04abf0d95bf7803fc5d147da54a/CKA_Curriculum_v1.35.pdf), and there are exclusive information for API objects and annotations. For more information, please see [CNCF Curriculum](https://github.com/cncf/curriculum/).

Please, feel free to place a pull request whether something is not up-to-date, should be added or contains wrong information/reference.

There are other Kubernetes certification exam preparation guides available:

- [Certified Kubernetes Security Specialist (CKS) - Preparation Guide](https://github.com/leandrocostam/cks-preparation-guide)

# Exam

The exam is kind of "put your hands on", where you have some problems to fix within 120 minutes.

My tip: Spend your time wisely. Use the Notebook feature (provided in exam's UI) to keep track of your progress, where you might take notes of each question, put some annotations in order to help you. Additionally, don't get stuck, move to the next problem, and take it back when you finish all the other problems.

Exam Cost: $445 and includes one free retake.

It's important to mention that you have access to [Kubernetes Official Documentation](https://kubernetes.io) during the exam. So get yourself familiar with Kubernetes online documentation, and know where to find all specific topics listed below. It might be helpful for you during the exam.

For information about the exam, please refer [Certified Kubernetes Administrator (CKA) Program](https://www.cncf.io/certification/cka/).

# CKA Curriculum

Exam objectives that outline of the knowledge, skills and abilities that a Certified Kubernetes Administrator (CKA) can be expected to demonstrate.

## Storage (10%)

- Implement storage classes and dynamic volume provisioning.

    - [Kubernetes Documentation > Concepts > Storage > Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/)
    - [Kubernetes Documentation > Concepts > Storage > Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

- Configure volume types, access modes, and reclaim policies.

    - [Kubernetes Documentation > Concepts > Storage > Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volumes)

- Manage persistent volumes and persistent volume claims.

    - [Kubernetes Documentation > Concepts > Storage > Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)

    - [Kubernetes Documentation > Tasks > Configure Pods and Containers > Configure a Pod to Use a PersistentVolume for Storage](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#create-a-persistentvolume)

## Workloads & Scheduling (15%)

- Understand deployments and how to perform rolling update and rollbacks.

    - [Kubernetes Documentation > Concepts > Workloads > Controllers > Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

    - Example Deployment File (`dep-nginx.yaml`) using NGINX

        ```yaml
        apiVersion: apps/v1
        kind: Deployment
        metadata:
            name: nginx-deployment
            labels:
                app: nginx
        spec:
          replicas: 3
          selector:
            matchLabels:
              app: nginx
          template:
            metadata:
              labels:
                app: nginx
            spec:
              containers:
              - name: nginx
                image: nginx:1.21.6
                ports:
                - containerPort: 80
        ```

        ```bash
        # Create Deployment
        kubectl create -f dep-nginx.yaml

        # Get Deployments
        kubectl get deployments

        # Update Deployment
        kubectl edit deployment.v1.apps/nginx-deployment

        # See rollout status
        kubectl rollout status deployment.v1.apps/nginx-deployment

        # Describe Deployment
        kubectl describe deployment

        # Rolling back to a previous revision
        kubectl rollout undo deployment.v1.apps/nginx-deployment
        ```

- Use ConfigMaps and Secrets to configure applications.

    - [Kubernetes Documentation > Concepts > Configuration > ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)

    - [Kubernetes Documentation > Concepts > Configuration > Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)

- Configure workload autoscaling.

    - [Kubernetes Documentation > Concepts > Cluster Administration > Managing Resources > Scaling Your Application](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/#scaling-your-application)

    - [Kubernetes Documentation > Concepts > Workloads > Autoscaling Workloads](https://kubernetes.io/docs/concepts/workloads/autoscaling/)

        ```bash
        # Increase replicas number for nginx-deployment
        kubectl scale deployment/nginx-deployment --replicas=5

        # Using autoscaling
        kubectl autoscale deployment/nginx-deployment --min=2 --max=5
        ```

- Understand the primitives used to create robust, self-healing, application deployments.

    - [Kubernetes Documentation > Concepts > Workloads > Pods > Pod Lifecycle](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

    - [Kubernetes Documentation > Tasks > Configure Pods and Containers > Configure Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

- configure Pod admission and scheduling (limits, node affinity, etc.).

    - [Kubernetes Documentation > Concepts > Configuration > Managing Resources for Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

    - [Kubernetes Documentation > Concepts > Policy](https://kubernetes.io/docs/concepts/policy/)

    - [Kubernetes Documentation > Concepts > Scheduling > Assign Pods to Nodes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/)

## Services & Networking (20%)

- Understand connectivity between Pods.

    - [Kubernetes Documentation > Concepts > Workloads > Pods > Networking](https://kubernetes.io/docs/concepts/workloads/pods/#pod-networking)

    - [GitHub > Kubernetes Community Documentation > Design Proposals > Networking](https://raw.githubusercontent.com/kubernetes/design-proposals-archive/main/network/networking.md)

- Use ClusterIP, NodePort, LoadBalancer service types and endpoints.

    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Service](https://kubernetes.io/docs/concepts/services-networking/service/)

- Use the Gateway API to manage ingress traffic.

    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Gateway API](https://kubernetes.io/docs/concepts/services-networking/gateway/)

- Know how to use Ingress controllers and Ingress resources.

    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)

    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Ingress Controllers](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/)

- Understand and use CoreDNS.

    - [Kubernetes Documentation > Tasks > Administer a Cluster > Using CoreDNS for Service Discovery](https://kubernetes.io/docs/tasks/administer-cluster/coredns/)

## Troubleshooting (30%)

- Troubleshoot clusters and nodes.

    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Troubleshoot Clusters](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/)

- Troubleshoot cluster components.

    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Troubleshoot Clusters > Cluster failure modes](https://kubernetes.io/docs/tasks/debug/debug-cluster/#cluster-failure-modes)

- Monitor cluster and application resource usage.

    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Tools for Monitoring Resources](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/)

- Manage and evaluate container output streams.

    - [Kubernetes Documentation > Concepts > Cluster Administration > Logging Architecture](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

- Troubleshoot services and networking.

    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Troubleshooting Applications > Debug Services](https://kubernetes.io/docs/tasks/debug/debug-application/debug-service/)
    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Application Introspection and Debugging](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-application-introspection/)

## Cluster Architecture, Installation & Configuration (25%)

- Manage role based access control (RBAC).

    - [Kubernetes Documentation > Reference > Accessing the API > Using RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

- Prepare underlying infrastructure for installing a Kubernetes cluster.

    - [Kubernetes Documentation > Getting started](https://kubernetes.io/docs/setup/)

    - [Kubernetes Documentation > Getting started > Production environment > Installing Kubernetes with deployment tools > Bootstrapping clusters with kubeadm > Installing kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/)

- Create and manage Kubernetes clusters using kubeadm.

    - [Kubernetes Documentation > Getting started > Production environment > Installing Kubernetes with deployment tools > Bootstrapping clusters with kubeadm > Creating a cluster with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)


- Manage the lifecycle of Kubernetes clusters.

    - [Kubernetes Documentation > Tasks > Administer a Cluster > Administration with kubeadm > Upgrading kubeadm clusters](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

- Implement and configure a highly-available control plane.

    - [Kubernetes Documentation > Getting started > Production environment > Installing Kubernetes with deployment tools > Bootstrapping clusters with kubeadm > Creating Highly Available clusters with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/)

- Use Helm and Kustomize to install cluster components.

    - [Kubernetes Documentation > Concepts > Cluster Administration > Managing Resources](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/)

    - [Kubernetes Documentation > Tasks > Manage Kubernetes Objects](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/)

    - [Helm Cheat Sheet](https://helm.sh/docs/intro/CheatSheet)

- Understand extension interfaces (CNI, CSI CRI, etc.).

    - [Kubernetes Documentation > Concepts > Extending Kubernetes > Compute, Storage, and Networking Extensions](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/)

    - [Kubernetes Documentation > Getting started > Production environment >Container Runtimes](https://kubernetes.io/docs/setup/production-environment/container-runtimes/)

    - [Kubernetes Documentation > Concepts > Cluster Administration > Cluster Networking](https://kubernetes.io/docs/concepts/cluster-administration/networking/)    

- Understand CRDs, install and configure operators.

    - [Kubernetes Documentation > Concepts > Extending Kubernetes > Custom Resources](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/)
    
    - [Kubernetes Documentation > Concepts > Extending Kubernetes > Operators](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/)

Helpful commands:

```bash
# Display addresses of the master and services
kubectl cluster-info

# Dump current cluster state to stdout
kubectl cluster-info dump

# List the nodes
kubectl get nodes

# Show metrics for a given node
kubectl top node my-node

# List all pods in all namespaces, with more details
kubectl get pods -o wide --all-namespaces

# List all services in all namespaces, with more details
kubectl get svc  -o wide --all-namespaces
```

# CKA Preparation Courses

- [Free CKA Self-Study Course - RX-M](https://rx-m.com/cka-online-training/)

- [Certified Kubernetes Administrator (CKA) video course - Pluralsight](https://www.pluralsight.com/paths/certified-kubernetes-administrator)

- [Kubernetes Fundamentals (LFS258) video course - Linux Foundation](https://training.linuxfoundation.org/training/kubernetes-fundamentals/)

- [Certified Kubernetes Administrator (CKA) 5-day live, instructor-led Boot Camp - RX-M](https://rx-m.com/training/certified-kubernetes-administrator-cka-boot-camp/)

- [Certified Kubernetes Administrator (CKA) 1-day live, instructor-led Exam Prep - RX-M](https://rx-m.com/training/certified-kubernetes-administrator-cka-exam-prep/)

- [Certified Kubernetes Administrator (CKA) video course - Udemy](https://www.udemy.com/course/certified-kubernetes-administrator-with-practice-tests/)

# kubectl Ninja

Tip: Use [kubectl Cheatsheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/) during the exam. You don't need to decorate everything.

#### Useful commands or parameters during the exam:

```bash
# Use "kubectl describe" for related events and troubleshooting
kubectl describe pods <podid>

# Use "kubectl explain" to check the structure of a resource object.
kubectl explain deployment --recursive

## Add "-o wide" in order to use wide output, which gives you more details.
kubectl get pods -o wide

## Check always all namespaces by including "--all-namespaces"
kubectl get pods --all-namespaces
```

Generate a manifest template from imperative spec using the output option "-o yaml" and the parameter "--dry-run=client":

```shell
# create a service
kubectl create service clusterip my-service --tcp=8080 --dry-run=client -o yaml

# create a deployment
kubectl create deployment nginx --image=nginx --dry-run=client -o yaml

# create a pod
kubectl run nginx --image=nginx --restart=Never --dry-run=client -o yaml
```

Create resources using kubectl + stdin (heredoc) instead of creating them from manifest files. It helps a lot and saves time. You can use the output of the command above and modify as required:

```shell
cat <<EOF | kubectl create -f -
...
EOF
```

It saves lots of time, believe me.

Kubectl Autocomplete (configured for you in the exam environment, but worth enabling in your local environment as well):

```shell
source <(kubectl completion bash)
```

# Practice

Practice a lot with Kubernetes:

- [Killer.sh - CKA Simulator](https://killer.sh/cka)
- [KillerCoda - CKA Simulator](https://killercoda.com/cka)
- [Kubernetes the Hard Way by Kelsey Hightower](https://github.com/kelseyhightower/kubernetes-the-hard-way)

# CKA Tips

Some links that contain tips that might help you from different perspectives of the CKA exam.

- [How to pass the Certified Kubernetes Administrator (CKA) exam on the first attempt](https://medium.com/devopslinks/how-to-pass-certified-kubernetes-administrator-cka-exam-on-first-attempt-36c0ceb4c9e)
- [Everything you need to know about Kubernetes certification CNCF webinar](https://youtu.be/vFvelHoxeP0)
