# Sources:
https://artifacthub.io/packages/helm/bitnami/thanos
https://docs.bitnami.com/kubernetes/infrastructure/thanos/administration/enable-metrics/

# Install
<pre>
$ oc project saberkan-thanos-poc
$ helm install thanos thanos

$ oc project saberkan-application-poc
$ oc create -f secret-sidecar.yaml
$ oc create -f prometheus.yaml
</pre>
