# Certified Kubernetes Administrator (CKA) - V1.12.0

The objective of this repository is help you for taking the Kubernetes Certified Administrator Certification exam using online resources, especially using resources from the [Kubernetes Oficial Documentation](https://kubernetes.io).

The references were selected for the Exam Curriculum 1.12.0, which uses the Kubernetes 1.12 version, and there are exclusive information for API objects and annotations. For more information, please see [CKA Curriculum 1.12.0](https://github.com/cncf/curriculum/blob/master/CKA_Curriculum_V1.12.0.pdf).

Please, feel free to place a pull request whether something is not up-to-date, should be added or contains wrong information/reference.

# Exam

The exam is kind of "put your hands on", where you have 24 problems to fix within 180 minutes. Based on that, you have ~7.5 minutes per problem, where usually you will spend more time in some problems than others.

My tip: Spend your time wisely. Use the Notebook feature (provided in exam's UI) to keep track of your progress, where you might take notes of each question, put some anottations in order to help you. Additionally, don't get stuck, move to the next problem, and take it back when you finish all the other problems.

Exam Cost: $300 and includes one free retake.

It's important to mention that you have access to [Kubernetes Oficial Documentation](https://kubernetes.io) during the exam. So get yourself familiar with Kubernetes online documentation, and know where to find all specific topics listed below. It might be helpful for you during the exam.

For information about the exam, please refer [Certified Kubernetes Administrator (CKA) Program](https://www.cncf.io/certification/cka/).

# CKA Curriculum

Exam objectives that outline of the knowledge, skills and abilities that a Certified Kubernetes Administrator (CKA) can be expected to demonstrate.

## Application Lifecycle Management 8%

- Understand Deployments and how to perform rolling updates and rollbacks.

    - [Concepts: Workloads: Controllers: Deployment](https://v1-12.docs.kubernetes.io/docs/concepts/workloads/controllers/deployment/)

    - Example Deployment File (dep-nginx.yaml) using NGINX 

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
                    image: nginx:1.15.4
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

- Know various ways to configure applications.

    - [Concepts: Cluster Administration: Managing Resources](https://v1-12.docs.kubernetes.io/docs/concepts/cluster-administration/manage-deployment/)

- Know how to scale applications.

    - [Concepts: Cluster Administration: Managing Resources: #Scaling Your Application](https://v1-12.docs.kubernetes.io/docs/concepts/cluster-administration/manage-deployment/#scaling-your-application).

        ```bash
        # Increase replicas number for nginx-deployment
        kubectl scale deployment/nginx-deployment --replicas=5

        # Using autoscaling
        kubectl autoscale deployment/nginx-deployment --min=2 --max=5
        ```

- Understand the primitives necessary to create a self-healing application.

    - [Concepts: Workloads: Pods: Pod Lifecycle](https://v1-12.docs.kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

    - [Tasks: Configure Pods and Containers: Liveness and Readiness Probes](https://v1-12.docs.kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)

## Installation, Configuration & Validation 12%

- Design a Kubernetes cluster.

    - [Concepts: Cluster Administration: Overview: Planning a Cluster](https://v1-12.docs.kubernetes.io/docs/concepts/cluster-administration/cluster-administration-overview/#planning-a-cluster)

- Install Kubernetes masters and nodes.

    - [Setup: Creating a Custom Cluster from Scratch](https://v1-12.docs.kubernetes.io/docs/setup/scratch/)

- Configure secure cluster communications.

    - [Tasks: TLS: Manage TLS Certificates in a Cluster](https://v1-12.docs.kubernetes.io/docs/tasks/tls/managing-tls-in-a-cluster/)

- Configure a Highly-Available Kubernetes cluster.

    - [Setup: Bootstrapping Clusters with kubeadm: Creating Highly Available Clusters with kubeadm](https://v1-12.docs.kubernetes.io/docs/setup/independent/high-availability/)

- Know where to get the Kubernetes release binaries.

    - [Setup: Downloading Kubernetes: Bulding from Source](https://v1-12.docs.kubernetes.io/docs/setup/release/building-from-source/)

- Provision underlying infrastructure to deploy a Kubernetes cluster.

    - [Setup: Picking the Right Solution](https://v1-12.docs.kubernetes.io/docs/setup/pick-right-solution/)

- Choose a network solution.

    - [Setup: Creating a Custom Cluster from Scratch: #Network](https://v1-12.docs.kubernetes.io/docs/setup/scratch/#network)

- Choose your Kubernetes infrastructure configuration.

    - [Setup: Creating a Custom Cluster from Scratch: #Nodes](https://v1-12.docs.kubernetes.io/docs/setup/scratch/#nodes)
    - [Setup: Building Large Clusters](https://v1-12.docs.kubernetes.io/docs/setup/cluster-large/)

- Run end-to-end tests on your cluster.

    - [Reference: Kubectl Commands: Cluster Management](https://v1-12.docs.kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#-strong-cluster-management-strong-)

    - [Extra: End-to-End Testing in Kubernetes](https://github.com/kubernetes/community/blob/master/contributors/devel/e2e-tests.md)

- Analyse end-to-end tests results.

    - [Extra: Kubetest](https://github.com/kubernetes/test-infra/tree/master/kubetest)

- Run Node end-to-end tests.

    - [Node End-To-End tests](https://github.com/kubernetes/community/blob/master/contributors/devel/e2e-node-tests.md)

```bash
# Kucebtl Cheatsheet commands to end-to-end tests

# Display addresses of the master and services
kubectl cluster-info

# Dump current cluster state to stdout
kubectl cluster-info dump

# Check health of cluster components
kubectl get componentstatuses

# List the nodes
kubectl get nodes

# Show metrics for a given node
kubectl top node my-node

# List all pods in all namespaces, with more details
kubectl get pods -o wide --all-namespaces

# List all services in all namespaces, with more details
kubectl get svc  -o wide --all-namespaces
```

## Core Concepts 19%

- Understand the Kubernetes API primitives

    - [Concepts: Kubernetes API Overview](https://v1-12.docs.kubernetes.io/docs/concepts/overview/kubernetes-api/)
    - [Concepts: Understanding Kubernetes Objects](https://v1-12.docs.kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/).
    - [Reference: API Reference - V1.12](https://v1-12.docs.kubernetes.io/docs/reference/kubernetes-api/)
    - [Optional: Kubernetes Architecture 101 (Video Youtube)](https://www.youtube.com/watch?v=zeS6OyDoy78)

- Understand the Kubernetes cluster architecture.

    - [Concepts: Kubernetes Components](https://v1-12.docs.kubernetes.io/docs/concepts/overview/components/)
    - [Concepts: Concepts Underlying the Cloud Controller Manager](https://v1-12.docs.kubernetes.io/docs/concepts/architecture/cloud-controller/)

- Understand Services and other network primitives.

    - [Concepts: Services, Load Balancing and Networking](https://v1-12.docs.kubernetes.io/docs/concepts/services-networking/service/)

## Networking 11%

- Understand the networking configuration on the cluster nodes.
- Understand Pod networking concepts.
- Understand service networking.
- Deploy and configure network load balancer.
- Know how to use Ingress rules.
- Know how to configure and use the cluster DNS.
- Understand CNI.

## Scheduling 5%

- Use label selectors to schedule Pods.
- Understand the role of DaemonSets.
- Understand how resource limits can affect Podscheduling.
- Understand how to run multiple schedulers and how to configure Pods to use them.
- Manually schedule a pod without a scheduler.
- Dispaly scheduler events.
- Know how to configure the Kubernetes scheduler.

## Security 12%

- Know how to configure authentication and authorization.
- Understand Kubernetes security primitives.
- Know to configure network policies.
- Create and manage TLS certificates for cluster components.
- Work with images securely.
- Define security contexts.
- Secure persistent key value store.

## Cluster (Maintenance) 11%

- Understand Kubernetes cluster upgrade process.

    - [Tasks: Administration with kubeadm: Upgrading kubeadm clusters from v1.11 to v1.12](https://v1-12.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade-1-12/)
    - [Tasks: Administration with kubeadm: Upgrading kubeadm HA clusters from v1.11 to v1.12](https://v1-12.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade-ha-1-12/)

- Facilitate operating system upgrades.
- Implement backup and restore methodologies.

    - [Tasks: Administer a Cluster: Operating etcd clusters for Kubernetes](https://v1-12.docs.kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)

## Logging / Monitoring 5%

- Understand how to monitor all cluster components.

    - [Tasks: Monitor, Log, and Debug: Tools for Monitoring Resources](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/)

- Understand how to monitor applications.

    - [Tasks: Monitor, Log, and Debug: Application Introspection and Debugging](https://v1-12.docs.kubernetes.io/docs/tasks/debug-application-cluster/debug-application-introspection/)

- Manage cluster component logs.

    - [Tasks: Monitor, Log, and Debug: Troubleshoot Clusters](https://v1-12.docs.kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/)

        - Master Log Files
        ```
        /var/log/kube-apiserver.log - API Server, responsible for serving the API
        /var/log/kube-scheduler.log - Scheduler, responsible for making scheduling decisions
        /var/log/kube-controller-manager.log - Controller that manages replication controllers
        ```

         - Worker Nodes Log Files
        ```
        /var/log/kubelet.log - Kubelet, responsible for running containers on the node
        /var/log/kube-proxy.log - Kube Proxy, responsible for service load balancing
        ```

- Manage application logs.

    - [Tasks: Monitor, Log, and Debug: Troubleshoot Applications](https://v1-12.docs.kubernetes.io/docs/tasks/debug-application-cluster/debug-application/)


## Storage 7%

- Understand persistent volumes and know how to create them.

    - [Concepts: Storage: Persistent Volumes](https://v1-12.docs.kubernetes.io/docs/concepts/storage/persistent-volumes/)

- Understand access modes for volumes.

    - [Concepts: Storage: Persistent Volumes: #Access Modes](https://v1-12.docs.kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes)

- Understand persistent volume claims primitive.

    - [Concepts: Storage: Persistent Volumes: #PersistentVolumeClaims](https://v1-12.docs.kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)

- Understand Kubernetes storage objects.

    - [Concepts: Storage: Volumes](https://v1-12.docs.kubernetes.io/docs/concepts/storage/volumes)

- Know how to configure applications with persistent storage.

    - [Concepts: Storage: Volumes: #local](https://v1-12.docs.kubernetes.io/docs/concepts/storage/volumes/#local)
    - [Concepts: Storage: Volumes: #hostPath](https://v1-12.docs.kubernetes.io/docs/concepts/storage/volumes/#hostpath)

## Troubleshooting 10%

- Troubleshoot application failure.


    - [Tasks: Monitor, Log, and Debug: Troubleshoot Applications](https://v1-12.docs.kubernetes.io/docs/tasks/debug-application-cluster/debug-application/)
    - [Tasks: Monitor, Log, and Debug: Determine the Reason for Pod Failure](https://v1-12.docs.kubernetes.io/docs/tasks/debug-application-cluster/determine-reason-pod-failure/)

- Troubleshoot control plane failure.

    - [Tasks: Monitor, Log, and Debug: Troubleshoot Clusters](https://v1-12.docs.kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/)

- Troubleshoot worker node failure.

    - [Tasks: Monitor, Log, and Debug: Troubleshoot Clusters: #Worker Nodes](https://v1-12.docs.kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/#worker-nodes)

- Troubleshoot networking.

# CKA Preparation Courses

- [Certified Kubernetes Administrator (CKA) - Linux Academy](https://linuxacademy.com/cp/modules/view/id/155)

- [Kubernetes Fundamentals (LFS258) - Linux Foundation](https://training.linuxfoundation.org/training/kubernetes-fundamentals/)

- [Kubernetes Deep Dive - A Cloud Guru](https://acloud.guru/learn/kubernetes-deep-dive)

# kubectl Ninja

Tip: Use [kubectl Cheatsheet](https://v1-12.docs.kubernetes.io/docs/reference/kubectl/cheatsheet/) during the exam. You don't need to decorate everything.

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

Generate a manifest template from imperative spec using the output option "-o yaml" and the parameter "--dry-run":

```shell
kubectl create service clusterip my-service --tcp=8080 --dry-run -o yaml
```

Create resources using kubectl + stdin instead of creating them from manifest files. It helps a lot and saves time. You can use the output of the command above and modify as required:

```shell
cat <<EOF | kubectl create -f -
...
EOF  
```
It saves lots of time, believe me.

# CKA Tips

Some helpful links that contain tips that might help you from different pespectives of the CKA exam. 

- [Graham Moore - 7.5 tips to help you ace the Certified Kubernetes Administrator (CKA) exam](https://kubedex.com/7-5-tips-to-help-you-ace-the-certified-kubernetes-administrator-cka-exam/)

