## Kubectl Commands

### Minikube

- To create a single-node cluster with minikube
    `minikube start`
    
- `kubectl version`

- `kubectl create -f ./my-manifest.yaml`           # create resource(s)
- `kubectl create -f ./my1.yaml -f ./my2.yaml`     # create from multiple files
- `kubectl create -f ./dir`                        # create resource(s) in all manifest files in dir
- `kubectl create -f https://git.io/vPieo`         # create resource(s) from url
- `kubectl create deployment nginx --image=nginx`  # start a single instance of nginx

#### Get commands with basic output
- `kubectl get services`                          # List all services in the namespace
- `kubectl get pods --all-namespaces`             # List all pods in all namespaces
- `kubectl get pods -o wide`                      # List all pods in the namespace, with more details
- `kubectl get deployment my-dep`                 # List a particular deployment

#### Describe commands with verbose output
- `kubectl describe nodes my-node`
- `kubectl describe pods my-pod`

#### Scaling
- `kubectl scale --replicas=3 rs/foo`                                 # Scale a replicaset named 'foo' to 3
- `kubectl scale --replicas=3 -f foo.yaml`                            # Scale a resource specified in "foo.yaml" to 3

#### Delete commands
- `kubectl delete -f ./pod.json`                                              # Delete a pod using the type and name specified in pod.json
- `kubectl delete pod,service baz foo`                                        # Delete pods and services with same names "baz" and "foo"
- `kubectl delete pods,services -l name=myLabel`                              # Delete pods and services with label name=myLabel

#### logs
- `kubectl logs my-pod`                                 # dump pod logs (stdout)
