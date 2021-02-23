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

# TODO
- Fix prometheus proxy
Source: https://github.com/prometheus-community/prom-label-proxy 

<pre>
$ ~/go/bin/prom-label-proxy \
    -label prometheus_replica \
    -upstream http://thanos-query-saberkan-thanos-poc.apps.ocp.prod.redlabclub.eu \
    -insecure-listen-address 0.0.0.0:8080
$ curl http://localhost:8080/api/v1/query\?query\=\"up\"\&prometheus_replica\=\"prometheus-example-0\" 
</pre>

- Add nginx in front of prometheus proxy
