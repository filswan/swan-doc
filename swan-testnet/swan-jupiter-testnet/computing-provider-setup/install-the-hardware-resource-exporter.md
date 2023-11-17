# Install the Hardware resource-exporter

The `resource-exporter` plugin is developed to collect the node resource constantly, computing provider will report the resource to the Lagrange Auction Engine to match the space requirement. To get the computing task, every node in the cluster must install the plugin. You just need to run the following command:

```bash
cat <<EOF | kubectl apply -f -
apiVersion: apps/v1
kind: DaemonSet
metadata:
  namespace: kube-system
  name: resource-exporter-ds
  labels:
    app: resource-exporter
spec:
  selector:
    matchLabels:
      app: resource-exporter
  template:
    metadata:
      labels:
        app: resource-exporter
    spec:
      containers:
      - name: resource-exporter
        image: filswan/resource-exporter:v11.2.5
        imagePullPolicy: IfNotPresent
EOF
```

If you have installed it correctly, you can see the result shown in the figure by the command: `kubectl get po -n kube-system`

![7](https://github.com/lagrangedao/go-computing-provider/assets/102578774/38b0e15f-5ff9-4edc-a313-d0f6f4a0bda8)
