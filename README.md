# space-travel

Port forward service
kubectl port-forward service/podinfo 9898:9898

Generate traffic
kubectl run -i --tty load-generator --rm --image=busybox:1.28 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://podinfo:9898/swagger.json; done" >/dev/null


https://fluxcd.io/flux/guides/sealed-secrets/#encrypt-secrets

flux create source helm sealed-secrets \
--interval=1h \
--url=https://bitnami-labs.github.io/sealed-secrets \
--export > ./clusters/my-cluster/sealed-source.yaml


flux create helmrelease sealed-secrets \
--interval=1h \
--release-name=sealed-secrets-controller \
--target-namespace=flux-system \
--source=HelmRepository/sealed-secrets \
--chart=sealed-secrets \
--chart-version=">=1.15.0-0" \
--crds=CreateReplace \
--export > ./clusters/my-cluster/sealed-release.yaml