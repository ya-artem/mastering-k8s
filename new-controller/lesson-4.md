Для виконання завдання довелось змінити шлях до пакету у всіх файлах
Після виконання інтсрукції при викоанні 
```bash
kubectl get newresource example-resource -o yaml
```

отримав 

```
apiVersion: apps.newresource.com/v1alpha1
kind: NewResource
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"apps.newresource.com/v1alpha1","kind":"NewResource","metadata":{"annotations":{},"name":"example-resource","namespace":"default"},"spec":{"foo":"hello world"}}
  creationTimestamp: "2025-10-09T16:48:15Z"
  generation: 1
  name: example-resource
  namespace: default
  resourceVersion: "640"
  uid: 8ed367c7-ff7c-4b59-802f-f3e77a8676dc
spec:
  foo: hello world
status:
  ready: true
```
