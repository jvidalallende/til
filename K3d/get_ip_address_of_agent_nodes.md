# Get IP address of agent nodes in K3d

While playing with [k3d][02], I found out that to access [NodePort][01] services I need to use the IP
address of agent nodes (which are containers). This can be achieved by inspecting the metadata of the
cluster nodes.

This is just a long [jq][00] incantation, but it took me a while to get right, and I also understood
a bit better how to select items with it, so here it is as a reference.

It retrieves the list of nodes, filters them by those that contain the value `agent` within the annotation
`k3s.io/node-args`, and then it filters again the `addresses` field to only output the ones with `type="InternalIP".

```
kubectl get nodes -ojson | jq -r '.items[] | select(.metadata.annotations."k3s.io/node-args" | contains ("agent")) | .status.addresses[] | select(.type == "InternalIP") | .address'

172.19.0.5
172.19.0.6
```

[//]: # ( ------------------- references below this line ------------------- )

[00]: https://jqlang.org/
[01]: https://kubernetes.io/docs/concepts/services-networking/service/#type-nodeport
[02]: https://k3d.io
