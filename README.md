# kube-query

kube-query is an extension for osquery. letting you visualize your cluster using sql queries.

Deployment
===
### Prerequisites
#### Go v1.12+

### build
```bash
$ export GO111MODULE=on 
$ go build kube-query.go 
```

## Running kube-query
**When running the kube-query, you should always pass the `-kubeconfig` flag, specifying the path to your kubeconfig file.**

## osqueryi 
when using the [osqueryi tool](https://osquery.readthedocs.io/en/stable/introduction/using-osqueryi/) you can easily register kube-query by passing the -socket parameter to kube-query on another process. for example:  
`./kube-query -socket="/path/to/osquery/socket" -kubequery="/path/to/kubeconfig.yml"` 


But there are many other options to automatically [register extensions](https://osquery.readthedocs.io/en/stable/deployment/extensions/).

###

Examples Queries
===
```sql
# query all kube-system pods
SELECT * FROM kubernetes_pods WHERE namespace="kube-system";

# query all containers created by kuberentes
SELECT * FROM kubernetes_containers;

# query all pods that runs with a privileged container   
SELECT * 
 FROM kubernetes_containers 
 JOIN kubernetes_pods 
 ON kubernetes_containers.pod_name=kubernetes_pods.name 
 WHERE privileged="True";
```