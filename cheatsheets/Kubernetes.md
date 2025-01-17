#cheatsheets #kubernetes

## Kubectl Commands

### Annotate

```bash
# Annotate a resource with the key and value.
kubectl annotate <resource-type> <resource-name> <key>=<value>

# Override annotation of a resource.
kubectl annotate --overwrite <resource-type> <resource-name> <key>=<value>

# Annotate annotation of all resources.
kubectl annotate --all <resource-type> <resource-name> <key>=<value>

# Remove an annotation from a resource.
kubectl annotate <resource-type> <resource-name> <key>-
```

### Api Version

```bash
# Show API versions.
kubectl api-versions
```

### Apply

```bash
# Apply the config in <config-file>.
kubectl apply -f <config-file>

# Another way to apply the config in <config-file>.
cat <config-file> | kubectl apply -f -

# Apply the config string.
echo '<config-string>' | kubectl apply -f -
```

### Attach

```bash
# Attach to the first container in a pod.
kubectl attach <pod-name>

# Attach to a container in a pod.
kubectl attach <pod-name> -c <container-name>
```

### Autoscale

```bash
# Auto scale a deployment.
kubectl autoscale deployment <deployment-name> --min=<min-pods-number> --max=<max-pods-number> --cpu-percent=<cpu-percentage>

# Auto scale a replication controller.
kubectl autoscale rc <rc-name> --min=<min-pods-number> --max=<max-pods-number> --cpu-percent=<cpu-percentage>
```

### Cluster Info

```bash
# Display addresses of the master and services.
kubectl cluster-info

# Dump current cluster state to stdout.
kubectl cluster-info dump

# Dump current cluster state to <output-directory>.
kubectl cluster-info dump --output-directory=<output-directory>
```

### Config

#### View Config

```bash
# View kubectl config.
kubectl config view
```

#### Context

```bash
# Display the current-context.
kubectl config current-context

# Get available contexts.
kubectl config get-contexts

# Sets the current-context in a kubeconfig file.
kubectl config use-context <context-name>

# Set cluster field for context.
kubectl config set-context <context-name> --cluster=<cluster-name>

# Set user field for context.
kubectl config set-context <context-name> --user=<username>

# Set namespace field for context.
kubectl config set-context <context-name> --namespace=<namespace>
```

#### Cluster

```bash
# Set only the server field on the cluster entry without touching other values.
kubectl config set-cluster <cluster-name> --server=<server-endpoint>

# Embed certificate authority data for the cluster entry.
kubectl config set-cluster <cluster-name> --certificate-authority=<crt-file-path>

# Enable/disable cert checking for the cluster entry.
kubectl config set-cluster <cluster-name> --insecure-skip-tls-verify=<boolean>
```

#### Credentials

```bash
# Set only the "client-key" field without touching other values.
kubectl config set-credentials <username> --client-key=<client-key-filepath>

# Set the authentication username and password for user.
kubectl config set-credentials <username> --username=<auth-username> --password=<auth-password>

# Embed client certificate data for user.
kubectl config set-credentials <username> --client-certificate=<crt-filepath> --embed-certs=true
```

#### Others

```bash
# Sets an individual value in a kubeconfig file.
kubectl config set <property-name> <property-value>

# Unsets an individual value in a kubeconfig file.
kubectl config unset <property-name>
```

### Cordon & Uncordon

```bash
# Mark node as unschedulable.
kubectl cordon <node-name>

# Mark node as schedulable.
kubectl uncordon <node-name>
```

### Create

```bash
# Create a resource by filename or stdin
kubectl create -f <filename>

# Another way to create the config in <config-file>.
cat pod.yaml | kubectl create -f -

# Create a resource with the config string.
echo '<config-string>' | kubectl create -f -
```

### Delete

```bash
# Delete a resource.
kubectl delete <resource-type> <resource-name>

# Delete a resource matching a label.
kubectl delete <resource-type> -l <label-key>=<label-value>

# Delete all resources of certain type.
kubectl delete <resource-type> --all
```

### Describe

```bash
# Describe a resource.
kubectl describe <resource-type>/<resource-name>

# Describe a resource matching a label.
kubectl describe <resource-type> -l <label-key>=<label-value>
```

### Drain

```bash
# Drain a node for maintenance.
kubectl drain <node-name>

# Drain a node for maintenance forcefully.
kubectl drain <node-name> --force

# Drain a node with a grace period.
kubectl drain <node-name> --grace-period=<grace-period-in-seconds>
```

### Edit

```bash
# Edit a resource.
kubectl edit <resource-type>/<resource-name>
```

### Exec

```bash
# Execute a command in a container.
kubectl exec <pod-name> [-c <container-name>] -- <command>
```

### Explain

```bash
# Explain a resource.
kubectl explain <resource-type>
```

### Expose

```bash
# Create a service for a replica, which maps the container <target-port> to <port>.
kubectl expose rc <rc-name> --port=<port> --target-port=<target-port> [--name=<name>]

# Create a second service based on an existing service, which maps the container <target-port> to <port>.
kubectl expose service <service-name> --port=<port> --target-port=<target-port> [--name=<name>]
```

### Get

```bash
# List all resources of type <resource-type>.
kubectl get <resource-type>

# List all resources of type <resource-type> in json.
kubectl get <resource-type> -o json

# List all resources of type <resource-type> with more details.
kubectl get <resource-type> -o wide

# List the resource with name of <resource-name>.
kubectl get <resource-type> <resource-name>
```

### Label

```bash
# Label a resource with the key and value.
kubectl label <resource-type> <resource-name> <key>=<value>

# Override annotation of a resource.
kubectl label --overwrite <resource-type> <resource-name> <key>=<value>

# Label annotation of all resource.
kubectl label --all <resource-type> <resource-name> <key>=<value>

# Remove an annotation of a resource.
kubectl label <resource-type> <resource-name> <key>-
```

### Logs

```bash
# Show logs for the first container of a pod.
kubectl logs <pod-name>

# Show logs for a container in the pod.
kubectl logs <pod-name> -c <container-name>

# Show of a previous terminated pod.
kubectl logs <pod-name> -p

# Follow the log of a pod.
kubectl logs <pod-name> -f

# Show last few lines of logs in a pod.
kubectl logs <pod-name> --tail=<number-of-lines>

# Show all logs for a pod since <time-duration> (e.g., 5m, 1h).
kubectl logs --since=<time-duration> <pod-name>
```

### Patch

```bash
# Patch a node. An example of json-string is {"spec":{"unschedulable":true}}.
kubectl patch node <node-name> -p '<json-string>'
```

### Port Forward

```bash
# Forward container's <port> to host's <port>.
kubectl port-forward <pod-name> <port>

# Forward container's <container-port> to host's <host-port>.
kubectl port-forward <pod-name> <host-port>:<container-port>

# Forward container's <container-port> to host's random port.
kubectl port-forward <pod-name> :<container-port>

# Forward container's <container-port> to host's random port.
kubectl port-forward <pod-name> 0:<container-port>
```

### Proxy

```bash
# Run a proxy on port <proxy-port>.
kubectl proxy --port=<proxy-port>

# Run a proxy on an arbitrary port.
kubectl proxy --port=0
```

### Replace

```bash
# Replace the config in <config-file>.
kubectl replace -f <config-file>

# Another way to replace the config in <config-file>.
cat <config-file> | kubectl replace -f -

# Another way to replace the config string.
echo '<config-string>' | kubectl replace -f -
```

### Rolling Update

```bash
# Rolling update pods in <rc-name> with <config-file>.
kubectl rolling-update <rc-name> -f <config-file>

# Another way to rolling update pods in <rc-name> with <config-file>.
cat <config-file> | kubectl rolling-update <rc-name> -f -

# Another way to rolling update pods in <rc-name> with the config string.
echo '<config-string>' | kubectl rolling-update -f -

# Update the pods in <rc-name> with a new image.
kubectl rolling-update <rc-name> --image=<image-name>

# Abort and reverse an existing rollout in progress.
kubectl rolling-update <rc-name> --rollback
```

### Rollout

```bash
# View the rollout history of a resource.
kubectl rollout history <resource-type>/<resource-name>

# Pause a resource rollout.
kubectl rollout pause <resource-type>/<resource-name>

# Unpause a resource rollout.
kubectl rollout unpause <resource-type>/<resource-name>

# Rollback a resource rollout.
kubectl rollout rollback <resource-type>/<resource-name>
```

### Run

```bash
# Start a pod with <image-name>.
kubectl run <pod-name> --image=<image-name>

# Start a pod with <image-name> with an environment variable KEY=VALUE.
kubectl run <pod-name> --image=<image-name> --env="KEY=VALUE"

# Start a pod with <image-name>, and let the container expost <port>.
kubectl run <pod-name> --image=<image-name> --port=<port>

# Dry run. Print the corresponding API objects without creating them.
kubectl run <pod-name> --image=<image-name> --dry-run=client

# Run a container interactively.
kubectl run -it <pod-name> --image=<image-name>

# Run a container with <command>.
kubectl run <pod-name> --image=<image-name> -- <command>
```

### Scale

```bash
# Scale a replication controller to <number-of-relicas>.
kubectl scale --replicas=<number-of-relicas> rc/<fc-name>

# Scale a job to <number-of-relicas>.
kubectl scale --replicas=<number-of-relicas> job/<job-name>
```

### Version

```bash
# Print the client and server version information.
kubectl version
```

## Resource

### Common Resource Kinds

|Name|Shortnames|Namespaced|Kind|
|---|---|---|---|
|bindings||true|Binding|
|componentstatuses|cs|false|ComponentStatus|
|configmaps|cm|true|ConfigMap|
|endpoints|ep|true|Endpoints|
|events|ev|true|Event|
|limitranges|limits|true|LimitRange|
|namespaces|ns|false|Namespace|
|nodes|no|false|Node|
|persistentvolumeclaims|pvc|true|PersistentVolumeClaim|
|persistentvolumes|pv|false|PersistentVolume|
|pods|po|true|Pod|
|podtemplates||true|PodTemplate|
|replicationcontrollers|rc|true|ReplicationController|
|resourcequotas|quota|true|ResourceQuota|
|secrets||true|Secret|
|serviceaccounts|sa|true|ServiceAccount|
|services|svc|true|Service|
|mutatingwebhookconfigurations||false|MutatingWebhookConfiguration|
|validatingwebhookconfiguration|s|false|ValidatingWebhookConfiguration|
|customresourcedefinitions|crd,crds|false|CustomResourceDefinition|
|apiservices||false|APIService|
|controllerrevisions||true|ControllerRevision|
|daemonsets|ds|true|DaemonSet|
|deployments|deploy|true|Deployment|
|replicasets|rs|true|ReplicaSet|
|statefulsets|sts|true|StatefulSet|
|tokenreviews||false|TokenReview|
|localsubjectaccessreviews||true|LocalSubjectAccessReview|
|selfsubjectaccessreviews||false|SelfSubjectAccessReview|
|selfsubjectrulesreviews||false|SelfSubjectRulesReview|
|subjectaccessreviews||false|SubjectAccessReview|
|horizontalpodautoscalers|hpa|true|HorizontalPodAutoscaler|
|cronjobs|cj|true|CronJob|
|jobs||true|Job|
|certificatesigningrequests|csr|false|CertificateSigningRequest|
|leases||true|Lease|
|endpointslices||true|EndpointSlice|
|events|ev|true|Event|
|flowschemas||false|FlowSchema|
|prioritylevelconfigurations||false|PriorityLevelConfiguration|
|ingressclasses||false|IngressClass|
|ingresses|ing|true|Ingress|
|networkpolicies|netpol|true|NetworkPolicy|
|runtimeclasses||false|RuntimeClass|
|poddisruptionbudgets|pdb|true|PodDisruptionBudget|
|clusterrolebindings||false|ClusterRoleBinding|
|clusterroles||false|ClusterRole|
|rolebindings||true|RoleBinding|
|roles||true|Role|
|priorityclasses|pc|false|PriorityClass|
|csidrivers||false|CSIDriver|
|csinodes||false|CSINode|
|csistoragecapacities||true|CSIStorageCapacity|
|storageclasses|sc|false|StorageClass|
|volumeattachments||false|VolumeAttachment|

- Either the resource kind or the short name can be used as `<resource-type>` in the following commands in this page.
- For any namespaced resource, the command has to be appended with `-n <namespace>`.

### Resource Config

#### Pod

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: <pod-name>                    # e.g., nginx
  namespace: <namespace>              # e.g., nginx
spec:
  containers:
  - name: <container-name>            # e.g., nginx
    image: <image-name>               # e.g., nginx:1.14.2
    ports:
    - containerPort: <container-port> # e.g., 80
```

Use `kubectl get pod <pod-name> -n <namespace> -o yaml` to see more configurable fields.

#### Deployment

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: <deployment-name>                 # e.g., nginx-deployment
  namespace: <namespace>                  # e.g., nginx
  labels:
    app: <deployment-app-label>           # e.g., nginx
spec:
  replicas: <number-of-replicas>          # e.g., 2
  selector:
    matchLabels:
      app: <app-selector>                 # e.g., nginx
  template:
    metadata:
      labels:
        app: <pod-app-label>              # e.g., nginx
    spec:
      containers:
      - name: <container-name>            # e.g., nginx
        image: <image-name>               # nginx:1.14.2
        ports:
        - containerPort: <container-port> # e.g., 80
```

Use `kubectl get deployment <deployment-name> -n <namespace> -o yaml` to see more configurable fields.

#### Daemonset

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: <ds-name>
  namespace: <namespace>
spec:
  selector:
    matchLabels:
      <label-key>: <label-value>
  template:
    metadata:
      labels:
        <label-key>: <label-value>
    spec:
      containers:
      - name: <container-name>
        image: <image-name>
```

Use `kubectl get ds <ds-name> -n <namespace> -o yaml` to see more configurable fields.

#### Job

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: <job-name>             # e.g., pi
  namespace: <namespace>       # e.g., pi
spec:
  template:
    spec:
      containers:
      - name: <container-name> # e.g., pi
        image: <image-name>    # e.g., perl:5.34.0
        command: <cmd-args>    # e.g., ["perl",  "-Mbignum=bpi", "-wle", "print bpi(2000)"]
      restartPolicy: Never
```

Use `kubectl get job <job-name> -n <namespace> -o yaml` to see more configurable fields.

#### Cronjob

```yaml
apiVersion: batch/v1
kind: CronJob
metadata:
  name: <cronjob-name>
  namespace: <namespace>
spec:
  schedule: <schedule>          # e.g., every five minutes "*/5 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: <container-name>
            image: <image-name>
            imagePullPolicy: IfNotPresent
            command: <cmd-args> # e.g., ["/bin/sh",  "-c", "date; echo Hello from the Kubernetes cluster"]
          restartPolicy: OnFailure
```

Use `kubectl get cronjob <cronjob-name> -n <namespace> -o yaml` to see more configurable fields.

#### Service

```yaml
# ClusterIP Service.
apiVersion: v1
kind: Service
metadata:
  name: <service-name>
  namespace: <namespace>
spec:
  type: ClusterIP                                # the ClusterIP service type. ClusterIP service is only accessible from within the cluster.
  selector:
    <selector-label-key>: <selector-label-value> # selector for the target pods.
  ports:
    - protocol: <protocol>                       # the protocol the service uses, e.g., TCP
      port: <port>                               # the port exposed to the cluster, e.g., 80
      targetPort: <target-port>                  # the port requests are sent to in the pod, e.g., 9736


# NodePort Service.
apiVersion: v1
kind: Service
metadata:
  name: <service-name>
  namespace: <namespace>
spec:
  type: NodePort                                 # the NodePort service type. The service can be accessed from outside via your host node.
  selector:
    <selector-label-key>: <selector-label-value> # selector for the target pods.
  ports:
    - port: <port>                               # the port exposed to the cluster, e.g., 80
      targetPort: <target-port>                  # the port requests are sent to in the pod, e.g., 9736
      nodePort: <node-port>                      # the port the host node is exposed to the outside network, e.g. 30010


# LoadBalancer Service
apiVersion: v1
kind: Service
metadata:
  name: <service-name>
  namespace: <namespace>
spec:
  type: LoadBalancer
  selector:
    <selector-label-key>: <selector-label-value> # selector for the target pods.
  ports:
  - protocol: <protocol>                         # the protocol the service uses, e.g., TCP
    port: <port>                                 # the port exposed to the cluster, e.g., 80
    targetPort: <target-port>                    # the port requests are sent to in the pod, e.g., 9736
```

Use `kubectl get service <service-name> -n <namespace> -o yaml` to see more configurable fields.

#### Service Account

```yaml
kind: ServiceAccount
apiVersion: v1
metadata:
  name: <sa-name>        # the service account name
  namespace: <namespace> # the namespace
```

Use `kubectl get sa <sa-name> -n <namespace> -o yaml` to see more configurable fields.

#### Role & ClusterRole

```yaml
# Role
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  name: <role-name>      # the role name
  namespace: <namespace> # the namespace
rules:
- apiGroups: <api-group> # e.g., [""]
  resources: <resources> # e.g., ["pods"]
  verbs: <verbs>         # e.g., ["get", "watch", "list"]


# ClusterRole
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: <clusterrole-name> # the role name
rules:
- apiGroups: <api-group>   # e.g., [""]
  resources: <resources>   # e.g., ["pods"]
  verbs: <verbs>           # e.g., ["get", "watch", "list"]
```

Use `kubectl get role <role-name> -n <namespace> -o yaml` or `kubectl get clusterrole <clusterrole-name> -o yaml` to see more configurable fields.

#### RoleBinding & ClusterRoleBinding

```yaml
# RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: <rolebinding-name> # the role binding name
  namespace: <namespace>   # the namespace of the role binding
subjects:
- kind: ServiceAccount
  name: <sa-name>          # the sa name
  namespace: <namespace>   # the namespace of the sa
roleRef:
  kind: Role
  name: <role-name>        # the Role name
  apiGroup: rbac.authorization.k8s.io


# ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: <clusterrolebinding-name> # the role binding name
subjects:
- kind: ServiceAccount
  name: <sa-name>                 # the sa name
  namespace: <namespace>          # the namespace of the sa
roleRef:
  kind: ClusterRole
  name: <clusterrole-name>        # the cluster role name
  apiGroup: rbac.authorization.k8s.io
```

Use `kubectl get rolebinding <rolebinding-name> -n <namespace> -o yaml` or `kubectl get clusterrolebinding <clusterrolebinding-name> -o yaml` to see more configurable fields.

#### ConfigMap

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: <cm-name>
  namespace: <namespace>
data:
  <key1>: <value1>
  <key2>: <value2>
```

Use `kubectl get cm <cm-name> -n <namespace> -o yaml` to see more configurable fields.

#### Secret

```bash
# Create a secret from command line.
kubectl create secret generic <secret-name> --from-literal=<key1>=<value1> --from-literal=<key2>=<value2>

# Get the secret in json.
kubectl get secret <secret-name> -o jsonpath='{.data}'

# Decode <key> in the secret.
kubectl get secret <secret-name> -o jsonpath='{.data.<key>}' | base64 --decode
```

Use `kubectl get secret <secret-name> -n <namespace> -o yaml` to see more configurable fields.

#### PersistentVolumeClaim

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: <pvc-name>
  namespace: <namespace>
spec:
  accessModes:
    - <access-mode>           # e.g., ReadWriteOnce, ReadOnlyMany, ReadWriteMany, ReadWriteOncePod
  volumeMode: Filesystem
  resources:
    requests:
      storage: <storage-size> # e.g., 10Gi
  storageClassName: <sc-name> # e.g., standard
```