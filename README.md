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

___

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
        $ kubectl edit deployment.v1.apps/nginx-deployment

        # See rollout status
        kubectl rollout status deployment.v1.apps/nginx-deployment

        # Describe Deployment
        $ kubectl describe deployment

        # Rolling back to a previous revision
        kubectl rollout undo deployment.v1.apps/nginx-deployment

- Know various ways to configure applications.

    - [Concepts: Cluster Administration: Managing Resources](https://v1-12.docs.kubernetes.io/docs/concepts/cluster-administration/manage-deployment/)

- Know how to scale applications.

    - [Concepts: Cluster Administration: Managing Resources: #Scaling Your Application](https://v1-12.docs.kubernetes.io/docs/concepts/cluster-administration/manage-deployment/#scaling-your-application).

        ```bash
        # Increase replicas number for nginx-deployment
        $ kubectl scale deployment/nginx-deployment --replicas=5

        # Using autoscaling
        $ kubectl autoscale deployment/ginx-deployment --min=2 --max=5
        ```

- Understand the primitives necessary to create a self-healing application.

    - [Concepts: Workloads: Pods: Pod Lifecycle](https://v1-12.docs.kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/)

    - [Tasks: Configure Pods and Containers: Liveness and Readiness Probes](https://v1-12.docs.kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-probes/)

## Installation, Configuration & Validation 12%

- Design a Kubernetes cluster.
- Install Kubernetes masters and nodes.
- Configure secure cluster communications.
- Configure a Highly-Available Kubernetes cluster.
- Know where to get the Kubernetes release binaries.
- Provision underlying infrastructure to deploy a Kubernetes cluster.
- Choose a network solution.
- Choose your Kubernetes infrastructure configuration.
- Run end-to-end tests on your cluster.
- Analyse end-to-end tests results.
- Run Node end-to-end tests.

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
- Facilitate operating system upgrades.
- Implement backup and restore methodologies.

## Logging / Monitoring 5%

- Understand how to monitor all cluster components.
- Understand how to monitor applications.
- Manage cluster component logs.
- Manage application logs.


## Storage 7%

- Understand persistent volumes and know how to create them.
- Understand access modes for volumes.
- Understand persistent volume claims primitive.
- Understand Kubernetes storage objects.
- Know how to configure applications with persistent storage.


## Troubleshooting 10%

- Troubleshoot application failure.
- Troubleshoot control plane failure.
- Troubleshoot worker node failure.
- Troubleshoot networking.

___

# CKA Preparation Courses

- [Certified Kubernetes Administrator (CKA) - Linux Academy](https://linuxacademy.com/cp/modules/view/id/155)

- [Kubernetes Fundamentals (LFS258) - Linux Foundation](https://training.linuxfoundation.org/training/kubernetes-fundamentals/)

- [Kubernetes Deep Dive - A Cloud Guru](https://acloud.guru/learn/kubernetes-deep-dive)

___

# Tips 
