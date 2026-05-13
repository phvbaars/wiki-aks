## Kubernetes Setup

Setting up a Kubernetes cluster can be achieved with a lot of different methods. Creating a test "cluster" can be very easy with the right tools:
- Minikube. https://minikube.sigs.k8s.io/docs/
- kind. https://kind.sigs.k8s.io/
- MicroK8s. https://microk8s.io/

If you want to set up a production-grade cluster on your own hardware or virtual machines, you can choose one of the various installers:
- kubeadm. https://kubernetes.io/docs/reference/setup-tools/kubeadm/
- kops. https://github.com/kubernetes/kops
- kubespray. https://github.com/kubernetes-sigs/kubespray

A few vendors started packaging Kubernetes into a distribution and even offer commercial support:
- Rancher. https://rancher.com/
- k3s. https://k3s.io/
- Red Hat OpenShift. https://www.redhat.com/en/technologies/cloud-computing/openshift
- VMWare Tanzu Platform
- Talos?

The distributions often choose an opinionated approach and offer additional tools while using Kubernetes as the central piece of their framework.

If you don’t want to install and manage it yourself, you can consume it from a cloud provider:
- Amazon (EKS)
- Google (GKE)
- Microsoft (AKS)
- DigitalOcean (DOKS)