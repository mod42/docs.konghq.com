---
title: Kong Ingress on Google Kubernetes Engine (GKE)
---

## Requirements

1. A fully functional GKE cluster.
   The easiest way to do this is to do it via the web UI:
   Go to Google Cloud's console > Kubernetes Engine > Cluster >
   Create a new cluster.
   This documentation has been tested on a zonal cluster in
   europe-west-4a using 1.10.5-gke.4 as Master version.
   The default pool has been assigned 2 nodes of kind 1VCPU
   with 3.75GB memory (default setting).
   The OS used is COS (Container Optimized OS) and the auto-scaling
   has been enabled. Default settings are being used except for
   `HTTP load balancing` which has been disabled (you probably want to use
   Kong features for this). For more information on GKE clusters,
   refer to
   [the GKE documentation](https://cloud.google.com/kubernetes-engine/docs/).
1. If you wish to use a static IP for Kong, you have to reserve a static IP
   address (in Google Cloud's console > VPC network >
   External IP addresses). For information,
   you must create a regional IP
   global is not supported as `loadBalancerIP` yet)
1. Basic understanding of Kubernetes
1. A working `kubectl`  linked to the GKE Kubernetes
   cluster we will work on. For information, you can associate a new `kubectl`
   context by using:

   ```bash
   gcloud container clusters get-credentials <my-cluster-name> --zone <my-zone> --project <my-project-id>
    ```

## Update User Permissions

> Because of [the way Kubernetes Engine checks permissions
when you create a Role or ClusterRole](https://cloud.google.com/kubernetes-engine/docs/how-to/role-based-access-control), you must
first create a RoleBinding that grants you all of
the permissions included in the role you want to create.
An example workaround is to create a RoleBinding that
gives your Google identity a cluster-admin role
before attempting to create additional Role or
ClusterRole permissions.
This is a known issue in RBAC in Kubernetes and
Kubernetes Engine versions 1.6 and
later.

A fast workaround:

```yaml

echo -n "
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
  name: cluster-admin-user
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: User
  name: <the current user using kubectl> # usually the Google account
                                         # e.g.: example@testorg.com
  namespace: kube-system" | kubectl apply -f -

```

{% include_cached /md/kic/deploy-kic.md version=page.version %}

## Setup environment variables

Next, we will setup an environment variable with the IP address at which
Kong is accessible. This will be used to actually send requests into the
Kubernetes cluster.

Execute the following command to get the IP address at which Kong is accessible:

```bash
$ kubectl get services -n kong
NAME         TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)                      AGE
kong-proxy   LoadBalancer   10.63.250.199   203.0.113.42   80:31929/TCP,443:31408/TCP   57d
```

Let's setup an environment variable to hold the IP address:

```bash
$ export PROXY_IP=$(kubectl get -o jsonpath="{.status.loadBalancer.ingress[0].ip}" service -n kong kong-proxy)
```

> Note: It may take a while for Google to actually associate the
IP address to the `kong-proxy` Service.

Once you've installed the {{site.kic_product_name}}, please follow our
[getting started](/kubernetes-ingress-controller/{{page.kong_version}}/guides/getting-started) tutorial to learn
about how to use the Ingress Controller.
