Kubernetes ReplicaSet
=====================

Let's scale up from one pod to many pods.


Step 0: Build the Image
-----------------------

For this exercise, we're going to be using the `hellonode:0.1` image built in exercise 2.

1. Run `docker image list` and ensure `hellonode:0.1` is present in the list.  If not, return to exercise 2 to build these images.


Step 0: Ensure Kubernetes is running
------------------------------------

1. Run `kubectl cluster-info` and `kubectl version`.  If it errored, return to exercise 0 to ensure you're running Docker Edge, you're in Linux mode, and you've enabled Kubernetes.


Step 1: Craft a deployment.yaml file
-----------------------------

1. Create `replicaset.yaml` file

2. Open `replicatset.yaml` in a text editor.

3. At the very top, add a bunch of blank space above `apiVersion: v1`.


4. Add these lines at the very top of the file:

   ```
   apiVersion: apps/v1
   kind: ReplicaSet
   metadata:
     name: hellonode-replicatset
   spec:
   ```

   This object will be a ReplicaSet, found in the `apps/v1` namespace.  We're naming this replicatset `hellonode-replicatset`.


5. In the `spec` section of the ReplicaSet, let's add content:

   ```
     replicas: 2
   ```

   This says we'd like 2 pods running.  If Kubernetes notices a pod has failed, it'll kill off that pod and spin up a new one.

6. Still in the `spec` section, add these lines:

   ```
     selector:
       matchLabels:
         app: hellonode
   ```

   This is how Kubernetes knows which pods relate to this deployment.  It looks for pods that have metadata that includes `app: hellonode`.  The pods can have additional metadata tags, but to be part of this deployment, they must have at least this tag.

7. Last piece in the `spec` section:

   ```
     template:
   ```

   We're about to tell Kubernetes how to build each pod.

8. Indent the original `pod.yaml` content by 4 spaces so it's nested in the template like so:

   ```
     template:
       apiVersion: v1
       kind: Pod
       metadata:
         name: hellonode
         labels:
           app: hellonode
           version: v0.1
       spec:
         containers:
         - ...
   ```

   We've defined what the pod would look like, but there's some things that don't fit here.  The deployment file is **not valid** yet.

9. **Remove** these lines from the template:

   ```
       apiVersion: v1
       kind: Pod
   ```

   ReplicaSets can only create pods, so we remove this redundancy.

10. **Remove** this line from the template:

    ```
          name: hellonode
    ```

    We can't have two pods with the same name, so we'll let Kubernetes auto-generate pod names.

11. Save the deployment.yaml file.


Step 2: Schedule the replicaset
-------------------------------

1. From a command prompt in the same directory as the `replicaset.yaml` file, type:

   ```
   kubectl apply -f replicaset.yaml
   ```

   This says "please schedule the thing I've got in the yaml file `replicaset.yaml`.

2. Run this command:

   ```
   kubectl get replicasets
   ```

   Do you see your replicaset?

3. Run this command:

   ```
   kubectl get pods
   ```

   Do you see the pods spinning up?

   Good thing we built the image on Kubernetes so it doesn't need to pull this image from Docker hub.

4. Run this command:

   ```
   kubectl describe replicaset hellonode-replicaset
   ```

   This command tells us a lot about the replicaset.

4. Run this command:

   ```
   kubectl get all
   ```

   This shows **most** of the things running in Kubernetes in the default namespace.  Here it shows both the replicaset and the pods.

5. Let's leave the replicaset running, and next build a service to NAT traffic into the pods.


Step 3 Delete a pod:

1. Get all the running pods:
    `kubectl get pods`
 
2. Delete a pod
     `kubectl delete pod pod-name`

You can now see replicaset spinning up new pod and terminating the pod u deleted.


Bonus
-----

1. List the pods, and ask Kubernetes to describe the details of one of them.

   See anything interesting in the pods' labels?
