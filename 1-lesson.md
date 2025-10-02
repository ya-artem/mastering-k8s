Я мав помилку 

>Warning  FailedScheduling  5m59s  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node.cloudprovider.kubernetes.io/uninitialized: true}. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.

Я зробив 

sudo kubebuilder/bin/kubectl get nodes

sudo kubebuilder/bin/kubectl taint nodes <node-name> node.cloudprovider.kubernetes.io/uninitialized-

І далі контейнер nginx запустився, і я зміг зробити port-forward sudo kubebuilder/bin/kubectl port-forward deployment/demo 8080:80 і відкрити welcome сторінку в браузері.
<b>Це правильний шлях чи ні?</b>



# Також я хотів запитати чи тут правлиьно стоїть cluster-name я дивився його по 
sudo kubebuilder/bin/kubectl config set-cluster test-env --server=https://127.0.0.1:6443 --insecure-skip-tls-verify
і sudo kubebuilder/bin/kubectl config view --minify -o jsonpath='{.contexts[0].context.cluster}{"\n"}' і там пише env-test ?

sudo PATH=$PATH:/opt/cni/bin:/usr/sbin kubebuilder/bin/kube-controller-manager \
    --kubeconfig=/var/lib/kubelet/kubeconfig \
        --leader-elect=false \
            --cloud-provider=external \
                --service-cluster-ip-range=10.0.0.0/24 \
                    --cluster-name=kubernetes \
                        --root-ca-file=/var/lib/kubelet/ca.crt \
                            --service-account-private-key-file=/tmp/sa.key \
                                --use-service-account-credentials=true \
                                    --v=2 &