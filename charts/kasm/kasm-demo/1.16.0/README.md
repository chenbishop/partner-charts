## Deploy

The following will deploy Kasm in your Kubernetes cluster.

## Prerequisite
StorageClass for Persistent Volume Claims (PVC): A StorageClass must be configured in the cluster to create Persistent Volume Claims (PVC) for the postgres-db. For detailed instructions, refer to the [Rancher Docs](https://ranchermanager.docs.rancher.com/how-to-guides/new-user-guides/manage-clusters/create-kubernetes-persistent-storage).

## Deploy Helm Chart
Refer to the [values.yaml](https://github.com/chenbishop/kasm-helm/blob/main/charts/kasm-demo/values.yaml) for available Helm values and their default configurations.

To begin, it's recommended to start by adding the global.hostname value in the values.yaml file. This will set the hostname for TLS certificates and the ingress URL.

## Next Steps
Once the Helm chart is fully deployed, add the ingress IP address to your DNS zone. After that, you should be able to access your Kasm instance at https://{hostname}, for example: https://kasm.example.com.

### Login Kasm Admin Console
The default admin username is `admin@kasm.local`. To retrieve the password, run the following kubectl command:
```
kubectl get secret --namespace {namespace} kasm-secrets -o jsonpath="{.data.admin-password}" | base64 -d
```

### Install Agent
Kasm agents are responsible for issuing compute resources, and they need to be deployed separately on a dedicated VM (Kasm does not currently support deploying the agent in Kubernetes). For a detailed installation guide, refer to the Kasm Agent Documentation.

To retrieve the manager token, use the following kubectl command:
``
kubectl get secret --namespace {namespace} kasm-secrets -o jsonpath="{.data.manager-token}" | base64 -d
``

