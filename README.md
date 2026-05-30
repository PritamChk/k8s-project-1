# k8s-project-1

To get started with Hands on kubernetes

# Post Kind Cluster Creation - Install Argo CD

> from official doc of ArgoCD

```sh
 kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
```

```sh
[ ec2-user@ip-172-31-38-42: ~/PRITAM ]
[ Sat May 30 | 23:17:55 ] $ kubectl patch svc argocd-server -n argocd -p '{"spec": {"type": "NodePort"}}'
service/argocd-server patched
[ ec2-user@ip-172-31-38-42: ~/PRITAM ]
[ Sat May 30 | 23:20:00 ] $ k get svc -n argocd
NAME                                      TYPE        CLUSTER-IP      EXTERNAL-IP   PORT(S)                      AGE
argocd-applicationset-controller          ClusterIP   10.96.76.129    <none>        7000/TCP,8080/TCP            5m24s
argocd-dex-server                         ClusterIP   10.96.212.37    <none>        5556/TCP,5557/TCP,5558/TCP   5m24s
argocd-metrics                            ClusterIP   10.96.8.59      <none>        8082/TCP                     5m24s
argocd-notifications-controller-metrics   ClusterIP   10.96.10.252    <none>        9001/TCP                     5m24s
argocd-redis                              ClusterIP   10.96.158.52    <none>        6379/TCP                     5m24s
argocd-repo-server                        ClusterIP   10.96.14.151    <none>        8081/TCP,8084/TCP            5m24s
argocd-server                             NodePort    10.96.100.137   <none>        80:31152/TCP,443:31612/TCP   5m24s
argocd-server-metrics                     ClusterIP   10.96.218.205   <none>        8083/TCP                     5m23s
```

> Need to port forward `443` to `31612`

```sh
 kubectl port-forward svc/argocd-server -n argocd 31612:443 --address=0.0.0.0 &
```

> **O/p** : ` Forwarding from 0.0.0.0:31612 -> 8080`

> To find ArgoCD initial password:

```sh
 kubectl get secrets -n argocd argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d && echo
```
