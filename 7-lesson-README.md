  Warning  FailedScheduling  9m39s  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node.cloudprovider.kubernetes.io/uninitialized: true}. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.
  Warning  FailedScheduling  4m26s  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node.cloudprovider.kubernetes.io/uninitialized: true}. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.



  sudo kubebuilder/bin/kubectl taint nodes codespaces-c72d34 node.cloudprovider.kubernetes.io/uninitialized:NoSchedule-



sudo kubebuilder/bin/kubectl describe pod flux-operator-bc65f64f8-xrzs2 -n flux-system


sudo kubebuilder/bin/kubectl logs flux-operator-bc65f64f8-xrzs2 -n flux-system

"Probe failed" probeType="Readiness" pod="flux-system/flux-operator-bc65f64f8-xrzs2" podUID="7253d6a1-53e9-4b4d-9975-ab93c23a91d6" containerName="manager" probeResult="failure" output="Get \"http://10.22.0.2:8081/readyz\": dial tcp 10.22.0.2:8081: connect: connection refused"

{"level":"error","ts":"2025-10-14T15:06:31.458Z","logger":"setup","msg":"unable to start manager","error":"failed to determine if *v1.FluxInstance is namespaced: failed to get restmapping: failed to get server groups: Get \"https://10.0.0.1:443/api\": dial tcp 10.0.0.1:443: i/o timeout"}




sudo kubebuilder/bin/kubectl get svc -A | grep kubernetes

sudo kubebuilder/bin/kubectl get endpoints kubernetes -n default


sudo kubebuilder/bin/kubectl get svc kubernetes -n default


sudo kubebuilder/bin/kubectl -n default edit endpoints kubernetes

sudo kubebuilder/bin/kubectl apply -f manifests/endpoints.yaml