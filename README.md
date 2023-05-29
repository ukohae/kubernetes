# kubernetes
[Kubernetes Note](https://github.com/devops-terraform-aws/kubernetes)

[Kubernetes Documentation Reference](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.27/#deployment-v1-apps)

### Kubernetes commands
```
kubectl apply -f fileName.yaml
kubectl get all
kubectl delete po --all   # delete all pod
kubectl rollout status deploy webapp   # check status of deployment
kubectl rollout undo deploy webapp --to-revision=2   # rollback to specific version
kubectl rollout history deploy webapp   # check version history
kubectl get all -n kube-system      # list all in kube-system
kubectl get po -n nameSpace  # get pods in specific nameSpace
kubectl describe svc kube-dns -n kube-system  #  decribe the service kube-dns in nameSpace `kube-system`
kubectl exec -it podName -- sh   # enter a pod
kubectl logs podName  # only on pods
kubectl logs -f podName # this will follow the logs
```

## Troubleshooting
### ImagePullBackOff Error
1.  `Image not found`: The specified image name or tag does not exist in the registry or repository. It could be due to a typo in the image name, incorrect image version, or the image being removed from the registry.

2.  `Authentication issues`: If the container image requires authentication or the registry requires credentials to access the image, incorrect or missing authentication credentials can cause a pullback error. This can be resolved by providing the correct credentials or configuring the Kubernetes cluster with the necessary authentication details.

3.  `Network connectivity`: The cluster may face network connectivity issues that prevent it from reaching the image registry. This can occur due to firewall rules, network misconfiguration, or restricted internet access within the cluster. Checking the network connectivity and resolving any network-related problems can help resolve the pullback error.

4.  `Registry unreachable`: The image registry might be down or experiencing issues, making it temporarily unreachable. In such cases, the pullback error will persist until the registry is available again.

5.  `Resource limitations`: If the Kubernetes cluster does not have sufficient resources (CPU, memory, disk space) to pull and run the container image, it can result in a pullback error. Ensuring that the cluster has enough resources available can help resolve this issue.

6.  `Image pull policy`: The image pull policy specified in the pod configuration can also cause pullback errors. If the pull policy is set to "IfNotPresent" or "Never," and the image is not already present in the cluster, it will result in a pullback error. Setting the pull policy to "Always" can resolve this problem, but it may increase the time required for pod creation.

7.  `Image registry configuration`: In some cases, misconfiguration of the image registry can lead to pullback errors. This can include incorrect URL configurations, insecure registry settings, or issues with SSL certificates. Verifying the registry configuration and addressing any misconfigurations can help resolve the error.