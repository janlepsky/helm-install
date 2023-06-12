kubectl create namespace mogenius
helm repo add mogenius https://helm.mogenius.com/public
helm repo update
helm install mogenius mogenius/mogenius-platform -n mogenius \
--set namespace="mogenius" \
--set global.cluster_name="mogenius-tst-1" \
--set global.api_key="mo_181497e6-3c1d-419a-abe4-942d0cf5a07c_jsl5dy79ru772r23wk4a" \
--set global.namespace="mogenius" \
--set k8smanager.enabled=true \
--set metrics.enabled=false \
--set traffic-collector.enabled=true \
--set pod-stats-collector.enabled=true \
--set ingress-nginx.enabled=true \
--set ingress-nginx.defaultBackend.image.registry=ghcr.io/mogenius \
--set ingress-nginx.defaultBackend.image.image=mo-default-backend \
--set ingress-nginx.defaultBackend.image.tag=latest \
--set ingress-nginx.defaultBackend.enabled=true \
--set certmanager.enabled=true \
--set cert-manager.startupapicheck.enabled=false \
--set certmanager.namespace="mogenius" \
--set cert-manager.namespace="mogenius" \
--set cert-manager.installCRDs=true
echo "Wait 120 sec ... until all services have been started ..." ; sleep 120
helm install mogenius-issuer mogenius/mogenius-cluster-issuer --set global.clusterissuermail="jan@mogenius.com"
