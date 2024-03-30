# k8s-kyverno-argocd

# Enforce Automated k8s cluster security using kyverno policy generator and argocd
In this project we will learn how to enforce policies, governence and compliance on your kubernetes cluster. Whether your kubernetes cluster is on AWS, Azure, GCP or on-premises, this project will work without any additional changes.
To explain the project with examples, using this configuration you can

* Generate -> For example, Create a default network policy whenever a namespace is created.
* Validate -> For example, Block users from using latest tag in the deployment or pod resources.
* Mutate -> For example, Attach pod security policy for a pod that is created without any pod security policy configuration.
* Verify Images -> For example, Verify if the Images used in the pod resources are properly signed and verified images.

   # High Level Design
On a very high level, A DevOps Engineer will write the required Kyverno Policy custom resource and commits it to a Git repository. Argo CD which is pre configured with auto-sync to watch for resources in the git repo, deploys the Kyverno Policies on to the Kubernetes cluster.
* ![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/f1f49f2b-b8c5-481c-bdd5-e39593f05a96)

  
# Installation
* To setup this project you need to install Argo CD controller and Kyverno controller, Assuming you have Kubernetes installed.

* Installation of both Kyverno and Argo CD are pretty straight forward as both of them support Helm charts and also provide a consolidated installation yaml files.
 # Kyverno
 There are two easy ways to install kyverno:

* Using Helm
* Using the kubernetes manifest files

  # Using Helm
  * Add helm repo for kyverno
  * ![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/1f0b491e-241c-475c-a440-05e47f815632)
  * Install kyverno in HA mode
  *  helm install kyverno kyverno/kyverno -n kyverno --create-namespace --set replicaCount=3
  *  ![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/bbd84430-5c49-4a0a-b0ff-84df1d443183)
  *  ![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/12d404fa-6d84-4e6d-92cb-ade12f166965)
  *  ![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/16949947-89e4-4d2c-9bbf-5775eaac7227)

# Argo CD
There are three ways to install Argo CD

* kubectl apply -f https://raw.githubusercontent.com/argoproj/argo-cd/master/manifests/install.yaml
* Helm Charts, Follow the link
* Using the Argo CD Operator, Follow the link

# Demystifying Kyverno & Kyverno Policies
Kyverno is a policy engine designed for Kubernetes

A Kyverno policy is a collection of rules. Each rule consists of a match declaration, an optional exclude declaration, and one of a validate, mutate, generate, or verifyImages declaration. Each rule can contain only a single validate, mutate, generate, or verifyImages child declaration.
![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/77e6333a-17db-48ec-be66-cc226e7aac77)

Policies can be defined as cluster-wide resources (using the kind ClusterPolicy) or namespaced resources (using the kind Policy.) As expected, namespaced policies will only apply to resources within the namespace in which they are defined while cluster-wide policies are applied to matching resources across all namespaces. Otherwise, there is no difference between the two types.

Additional policy types include PolicyException and (Cluster)CleanupPolicy which are separate resources and described further in the documentation.
 # Architecture
 ![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/6353216e-ab5f-42cb-ad5e-97875869f143)



