1) Я мав помилку 

>Warning  FailedScheduling  5m59s  default-scheduler  0/1 nodes are available: 1 node(s) had untolerated taint {node.cloudprovider.kubernetes.io/uninitialized: true}. preemption: 0/1 nodes are available: 1 Preemption is not helpful for scheduling.

Я зробив 

`sudo kubebuilder/bin/kubectl get nodes`

`sudo kubebuilder/bin/kubectl taint nodes <node-name> node.cloudprovider.kubernetes.io/uninitialized-`

І далі контейнер nginx запустився, і я зміг зробити `sudo kubebuilder/bin/kubectl port-forward deployment/demo 8080:80` і відкрити <b>welcome</b> сторінку в браузері.
<b>Це правильний шлях чи ні?</b>



2)  Також я хотів запитати чи тут правлиьно стоїть cluster-name
в цій команді ?

```sudo PATH=$PATH:/opt/cni/bin:/usr/sbin kubebuilder/bin/kube-controller-manager \
    --kubeconfig=/var/lib/kubelet/kubeconfig \
    --leader-elect=false \
    --cloud-provider=external \
    --service-cluster-ip-range=10.0.0.0/24 \
    --cluster-name=kubernetes \
    --root-ca-file=/var/lib/kubelet/ca.crt \
    --service-account-private-key-file=/tmp/sa.key \
    --use-service-account-credentials=true \
    --v=2 &
```


Я дивився назву його в поді і в інструкції вище </br>
`sudo kubebuilder/bin/kubectl config set-cluster test-env --server=https://127.0.0.1:6443 --insecure-skip-tls-verify`
і `sudo kubebuilder/bin/kubectl config view --minify -o jsonpath='{.contexts[0].context.cluster}{"\n"}`' і там пише `env-test`. 



Питання:
1) Ци виконання команди `sudo kubebuilder/bin/kubectl taint nodes <node-name> node.cloudprovider.kubernetes.io/uninitialized-` вважається правильним шляхом ?
2) Чи правильно тут встановлено назву кластеру  `--cluster-name=kubernetes` ?
3) Чи треба щось робити із setup.sh ?
