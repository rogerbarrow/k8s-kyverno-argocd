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

# Step 1 start a mini Kube Clouster
![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/f490dfd9-2b24-45a6-8cc8-32cc5d52aad0)

# Download Kyverno
![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/2ff7a68f-e1f2-4267-8e19-d93a11af4abe)

# download ArgoCD
![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/9c17b4ff-9a30-44d3-b7fc-adfa40dab9d6)

# Download Policy
![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/fb924f24-4799-4599-8d7f-7e7ef0f29cf7)

* ![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/d0b9c96a-24f3-4aa7-8a15-378cd60e7740)

* ![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/a5b32c05-c4db-4d79-ba0c-31405fd64528)

# Attempt to Create pod- Request should Fail because of Kyverno
![image](https://github.com/rogerbarrow/k8s-kyverno-argocd/assets/46138186/17834782-38ea-4204-8a40-31d6958ab4a0)
