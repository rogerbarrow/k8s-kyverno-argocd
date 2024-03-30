# k8s-kyverno-argocd

# Enforce Automated k8s cluster security using kyverno policy generator and argocd
In this project we will learn how to enforce policies, governence and compliance on your kubernetes cluster. Whether your kubernetes cluster is on AWS, Azure, GCP or on-premises, this project will work without any additional changes.
To explain the project with examples, using this configuration you can

* Generate -> For example, Create a default network policy whenever a namespace is created.
* Validate -> For example, Block users from using latest tag in the deployment or pod resources.
* Mutate -> For example, Attach pod security policy for a pod that is created without any pod security policy configuration.
* Verify Images -> For example, Verify if the Images used in the pod resources are properly signed and verified images.

   # High Level Design
