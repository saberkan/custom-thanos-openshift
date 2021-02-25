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


# Adding prom-label-proxy in front of thanos (for rbac)
Source: https://github.com/prometheus-community/prom-label-proxy 

<pre>
$ oc new-project saberkan-thanos-proxy
$ oc create -f thanos-kube-rbac-proxy.yaml
$ TOKEN=$(oc whoami -t)
$ curl -H 'Accept: application/json' -H "Authorization: Bearer ${TOKEN}" http://thanos-rbac-proxy-insecure-saberkan-thanos-proxy.apps.ocp.prod.redlabclub.eu/api/v1/query?query=up\&namespace=saberkan-application-poc
</pre>

# TODO
- Add nginx in front of prom-label-proxy to add namespace in uri
- Add oauth-proxy in front of nginx to check access into route
