![Check Kubernetes documentation links](https://github.com/leandrocostam/kubernetes-certified-administrator-prep-guide/workflows/Check%20Kubernetes%20documentation%20links/badge.svg)

# Certified Kubernetes Administrator (CKA) - V1.20

The objective of this repository is help you for taking the Certified Kubernetes Administrator (CKA) exam using online resources, especially using resources from [Kubernetes Official Documentation](https://kubernetes.io).

The references were selected for the [Exam Curriculum 1.20](https://github.com/cncf/curriculum/blob/master/CKA_Curriculum_v1.20.pdf), and there are exclusive information for API objects and annotations. For more information, please see [CKA Curriculum](https://github.com/cncf/curriculum/).

Please, feel free to place a pull request whether something is not up-to-date, should be added or contains wrong information/reference.

# Exam

The exam is kind of "put your hands on", where you have some problems to fix within 120 minutes.

My tip: Spend your time wisely. Use the Notebook feature (provided in exam's UI) to keep track of your progress, where you might take notes of each question, put some annotations in order to help you. Additionally, don't get stuck, move to the next problem, and take it back when you finish all the other problems.

Exam Cost: $300 and includes one free retake.

It's important to mention that you have access to [Kubernetes Official Documentation](https://kubernetes.io) during the exam. So get yourself familiar with Kubernetes online documentation, and know where to find all specific topics listed below. It might be helpful for you during the exam.

For information about the exam, please refer [Certified Kubernetes Administrator (CKA) Program](https://www.cncf.io/certification/cka/).

# CKA Curriculum

Exam objectives that outline of the knowledge, skills and abilities that a Certified Kubernetes Administrator (CKA) can be expected to demonstrate.

## Cluster Architecture, Installation & Configuration (25%)

- Manage role based access control (RBAC).

    - [Kubernetes Documentation > Reference > Accessing the API > Using RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)

- Use Kubeadm to install a basic cluster.

    - [Kubernetes Documentation > Getting started > Production environment > Installing Kubernetes with deployment tools > Bootstrapping clusters with kubeadm > Creating a cluster with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/create-cluster-kubeadm/)

- Manage a highly-available Kubernetes cluster.

    - [Kubernetes Documentation > Getting started > Production environment > Installing Kubernetes with deployment tools > Bootstrapping clusters with kubeadm > Creating Highly Available clusters with kubeadm](https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/)

- Provision underlying infrastructure to deploy a Kubernetes cluster.

    - [Kubernetes Documentation > Getting started](https://kubernetes.io/docs/setup/)

- Perform a version upgrade on a Kubernetes cluster using Kubeadm.

    - [Kubernetes Documentation > Tasks > Administer a Cluster > Administration with kubeadm > Upgrading kubeadm clusters](https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/)

- Implement etcd backup and restore.

    - [Kubernetes Documentation > Tasks > Administer a Cluster > Operating etcd clusters for Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)


Helpful commands:

```bash
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

## Workloads & Scheduling (15%)

- Understand deployments and how to perform rolling update and rollbacks.

    - [Kubernetes Documentation > Concepts > Workloads > Controllers > Deployments](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/)

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
        ```

- Use ConfigMaps and Secrets to configure applications.

    - [Kubernetes Documentation > Concepts > Configuration > ConfigMaps](https://kubernetes.io/docs/concepts/configuration/configmap/)

    - [Kubernetes Documentation > Concepts > Configuration > Secrets](https://kubernetes.io/docs/concepts/configuration/secret/)

- Know how to scale applications.

    - [Kubernetes Documentation > Concepts > Cluster Administration > Managing Resources > Scaling Your Application](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/#scaling-your-application).

        ```bash
        # Increase replicas number for nginx-deployment
        kubectl scale deployment/nginx-deployment --replicas=5

        # Using autoscaling
        kubectl autoscale deployment/nginx-deployment --min=2 --max=5
        ```

- Understand the primitives used to create robust, self-healing, application deployments.

    - [Kubernetes Documentation > Concepts > Workloads > Pods > Pod Lifecycle](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

    - [Kubernetes Documentation > Tasks > Configure Pods and Containers > Configure Liveness, Readiness and Startup Probes](https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/)

- Understand how resource limits can affect Pod scheduling.

    - [Kubernetes Documentation > Concepts > Configuration > Managing Resources for Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)

- Awareness of manifest management and common templating tools.

    - [Kubernetes Documentation > Concepts > Cluster Administration > Managing Resources](https://kubernetes.io/docs/concepts/cluster-administration/manage-deployment/)

    - [Kubernetes Documentation > Tasks > Manage Kubernetes Objects](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/)

## Services & Networking (20%)

- Understand host networking configuration on the cluster nodes.

    - [Kubernetes Documentation > Concepts > Cluster Administration > Cluster Networking](https://kubernetes.io/docs/concepts/cluster-administration/networking/)

- Understand connectivity between Pods.

    - [Kubernetes Documentation > Concepts > Workloads > Pods > Networking](https://kubernetes.io/docs/concepts/workloads/pods/#pod-networking)

    - [GitHub > Kubernetes Community Documentation > Design Proposals > Networking](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/network/networking.md)

- Understand ClusterIP, NodePort, LoadBalancer service types and endpoints.

    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Service](https://kubernetes.io/docs/concepts/services-networking/service/)

- Know how to use Ingress controllers and Ingress resources.

    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Ingress](https://kubernetes.io/docs/concepts/services-networking/ingress/)
    - [Kubernetes Documentation > Concepts > Services, Load Balancing, and Networking > Ingress Controllers](https://kubernetes.io/docs/concepts/services-networking/ingress-controllers/)

- Know how to configure and use CoreDNS.

    - [Kubernetes Documentation > Tasks > Administer a Cluster > Using CoreDNS for Service Discovery](https://kubernetes.io/docs/tasks/administer-cluster/coredns/)

- Choose an appropriate container network interface plugin.

    - [Kubernetes Documentation > Concepts > Extending Kubernetes > Compute, Storage, and Networking Extensions > Network Plugins](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/)

## Storage (10%)

- Understand storage classes, persistent volumes.

    - [Kubernetes Documentation > Concepts > Storage > Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/)
    - [Kubernetes Documentation > Concepts > Storage > Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/)

- Understand volume mode, access modes and reclaim policies for volumes.

    - [Kubernetes Documentation > Concepts > Storage > Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistent-volumes)

- Understand persistent volume claims primitive.

    - [Kubernetes Documentation > Concepts > Storage > Persistent Volumes](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#persistentvolumeclaims)

- Know how to configure applications with persistent storage.

    - [Kubernetes Documentation > Tasks > Configure Pods and Containers > Configure a Pod to Use a PersistentVolume for Storage](https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/#create-a-persistentvolume)

## Troubleshooting (30%)

- Evaluate cluster and node logging.

    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Troubleshoot Clusters](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/)

- Understand how to monitor applications.

    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Tools for Monitoring Resources](https://kubernetes.io/docs/tasks/debug-application-cluster/resource-usage-monitoring/)

- Manage container stdout & stderr logs.

    - [Kubernetes Documentation > Concepts > Cluster Administration > Logging Architecture](https://kubernetes.io/docs/concepts/cluster-administration/logging/)

- Troubleshoot application failure.

    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Troubleshoot Applications](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-application/)
    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Application Introspection and Debugging](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-application-introspection/)

- Troubleshoot cluster component failure.

    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Troubleshoot Clusters](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-cluster/)

- Troubleshoot networking.

    - [Kubernetes Documentation > Tasks > Monitoring, Logging, and Debugging > Debug Services](https://kubernetes.io/docs/tasks/debug-application-cluster/debug-service/)

# CKA Preparation Courses

- [Certified Kubernetes Administrator (CKA) - A Cloud Guru (formerly Linux Academy)](https://acloudguru.com/course/cloud-native-certified-kubernetes-administrator-cka/)

- [Kubernetes Fundamentals (LFS258) - Linux Foundation](https://training.linuxfoundation.org/training/kubernetes-fundamentals/)

- [Kubernetes Deep Dive - A Cloud Guru](https://acloud.guru/learn/kubernetes-deep-dive)

# kubectl Ninja

Tip: Use [kubectl Cheatsheet](https://v1-18.docs.kubernetes.io/docs/reference/kubectl/cheatsheet/) during the exam. You don't need to decorate everything.

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
# create a service
kubectl create service clusterip my-service --tcp=8080 --dry-run -o yaml

# create a deployment
kubectl create deployment nginx --image=nginx --dry-run -o yaml

# create a pod
kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml
```

Create resources using kubectl + stdin instead of creating them from manifest files. It helps a lot and saves time. You can use the output of the command above and modify as required:

```shell
cat <<EOF | kubectl create -f -
...
EOF  
```
It saves lots of time, believe me.

Kubectl Autocomplete
```shell 
source <(kubectl completion bash)
```

# Practice

Practice a lot with Kubernetes:

- [Kubernetes the Hard Way by Kelsey Hightower](https://github.com/kelseyhightower/kubernetes-the-hard-way)
- [Katacoda: Learn Kubernetes using Interactive Browser-Based Scenarios](https://www.katacoda.com/courses/kubernetes)

# CKA Tips

Some links that contain tips that might help you from different perspectives of the CKA exam. 

- [Graham Moore - 7.5 tips to help you ace the Certified Kubernetes Administrator (CKA) exam](https://kubedex.com/7-5-tips-to-help-you-ace-the-certified-kubernetes-administrator-cka-exam/)
- [How to pass the Certified Kubernetes Administrator (CKA) exam on the first attempt](https://medium.com/devopslinks/how-to-pass-certified-kubernetes-administrator-cka-exam-on-first-attempt-36c0ceb4c9e)
