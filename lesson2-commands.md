export PATH=$PATH:/opt/cni/bin:kubebuilder/bin
sudo PATH=$PATH:/opt/cni/bin:/usr/sbin /opt/cni/bin/containerd -c /etc/containerd/config.toml &

HOST_IP=$(hostname -I | awk '{print $1}')


sudo PATH=$PATH:/opt/cni/bin:/usr/sbin kubebuilder/bin/kubelet \
            --kubeconfig=/var/lib/kubelet/kubeconfig \
            --config=/var/lib/kubelet/config.yaml \
            --root-dir=/var/lib/kubelet \
            --cert-dir=/var/lib/kubelet/pki \
            --hostname-override=$(hostname) \
            --node-ip=$HOST_IP \
            --v=1

sudo cp manifests/etcd.yaml /etc/kubernetes/manifests/

sudo cp manifests/kube-apiserver.yaml /etc/kubernetes/manifests/

sudo cp manifests/kube-scheduler.yaml /etc/kubernetes/manifests/

sudo cp manifests/kube-controller-manager.yaml /etc/kubernetes/manifests/

Then run 
sudo kubebuilder/bin/kubectl get pods -n kube-system to see pods 

example 
`
NAME                                      READY   STATUS    RESTARTS   AGE
etcd-codespaces-276783                    1/1     Running   0          3m17s
kube-apiserver-codespaces-276783          1/1     Running   0          3m19s
kube-controll-manager-codespaces-276783   1/1     Running   0          33s
kube-scheduler-codespaces-276783          1/1     Running   0          97s
`


Deployments for replcias sudo kubebuilder/bin/kubectl create deployment nginx --image=nginx --replicas=3



sudo kubebuilder/bin/kubectl get pods 

`
NAME                    READY   STATUS    RESTARTS   AGE
nginx-bf5d5cf98-f22dz   0/1     Pending   0          59s
nginx-bf5d5cf98-w2d9g   0/1     Pending   0          59s
nginx-bf5d5cf98-w6z48   0/1     Pending   0          59s
`

Error
`  Warning  FailedScheduling  77s   default-scheduler  0/1 nodes are available: 1 Too many pods. preemption: 0/1 nodes are available: 1 No preemption victims found for incoming pod.`


To fix need to increase pod numbers, in base config there is 4 pods we can update config, or run win option max-pods=20


After run win --max-pods=20

`
NAME                    READY   STATUS    RESTARTS   AGE
nginx-bf5d5cf98-f22dz   1/1     Running   0          6m38s
nginx-bf5d5cf98-w2d9g   1/1     Running   0          6m38s
nginx-bf5d5cf98-w6z48   1/1     Running   0          6m38s
`


# Command for debug
sudo ctr --namespace k8s.io container ls

sudo kubebuilder/bin/kubectl get pods -n kube-system


sudo kubebuilder/bin/kubectl logs -n kube-system kube-scheduler-codespaces-64f81d