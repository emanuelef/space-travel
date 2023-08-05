# space-travel

Port forward service
kubectl port-forward service/podinfo 9898:9898

Generate traffic
kubectl run -i --tty load-generator --rm --image=busybox:1.28 --restart=Never -- /bin/sh -c "while sleep 0.01; do wget -q -O- http://podinfo:9898/swagger.json; done" >/dev/null