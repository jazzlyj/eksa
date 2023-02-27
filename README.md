
# Install EKS Anywhere

* Install the latest release of eksctl. The EKS Anywhere plugin requires eksctl version 0.66.0 or newer.
```bash
curl "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" \
    --silent --location \
    | tar xz -C /tmp
sudo mv /tmp/eksctl /usr/local/bin/

```


* Install the eksctl-anywhere plugin.
```bash
export EKSA_RELEASE="0.14.2" OS="$(uname -s | tr A-Z a-z)" RELEASE_NUMBER=29
curl "https://anywhere-assets.eks.amazonaws.com/releases/eks-a/${RELEASE_NUMBER}/artifacts/eks-a/v${EKSA_RELEASE}/${OS}/amd64/eksctl-anywhere-v${EKSA_RELEASE}-${OS}-amd64.tar.gz" \
    --silent --location \
    | tar xz ./eksctl-anywhere
sudo mv ./eksctl-anywhere /usr/local/bin/


```

* Install the kubectl Kubernetes command line tool. This can be done by following the instructions here .

Or you can install the latest kubectl directly with the following.
```bash
export OS="$(uname -s | tr A-Z a-z)" ARCH=$(test "$(uname -m)" = 'x86_64' && echo 'amd64' || echo 'arm64')
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/${OS}/${ARCH}/kubectl"
sudo mv ./kubectl /usr/local/bin
sudo chmod +x /usr/local/bin/kubectl
```




# EKS Anywhere standalone cluster 
```bash
CLUSTER_NAME=mgmt
eksctl anywhere generate clusterconfig $CLUSTER_NAME --provider docker > $CLUSTER_NAME.yaml
eksctl anywhere create cluster -f $CLUSTER_NAME.yaml
```
    Performing setup and validations
    Warning: The docker infrastructure provider is meant for local development and testing only
    ✅ Docker Provider setup is valid
    ✅ Validate certificate for registry mirror
    ✅ Validate authentication for git provider
    ✅ Create preflight validations pass
    Creating new bootstrap cluster
    Provider specific pre-capi-install-setup on bootstrap cluster
    Installing cluster-api providers on bootstrap cluster
    Provider specific post-setup
    Creating new workload cluster
    Installing networking on workload cluster
    Creating EKS-A namespace
    Installing cluster-api providers on workload cluster
    Installing EKS-A secrets on workload cluster
    Installing resources on management cluster
    Moving cluster management from bootstrap to workload cluster
    Installing EKS-A custom components (CRD and controller) on workload cluster
    Installing EKS-D components on workload cluster
    Creating EKS-A CRDs instances on workload cluster
    Installing GitOps Toolkit on workload cluster
    GitOps field not specified, bootstrap flux skipped
    Writing cluster config file
    Deleting bootstrap cluster
    🎉 Cluster created!
    --------------------------------------------------------------------------------------
    The Amazon EKS Anywhere Curated Packages are only available to customers with the 
    Amazon EKS Anywhere Enterprise Subscription
    --------------------------------------------------------------------------------------
    Enabling curated packages on the cluster
    Installing helm chart on cluster	{"chart": "eks-anywhere-packages", "version": "0.2.30-eks-a-28"}

```bash
export KUBECONFIG=${PWD}/${CLUSTER_NAME}/${CLUSTER_NAME}-eks-a-cluster.kubeconfig
kubectl get ns
```

Use the cluster

Once the cluster is created you can use it with the generated KUBECONFIG file in your local directory
```bash
```



```bash
```