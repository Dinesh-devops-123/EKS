Namespace - it represents a cluster inside anothert cluster
kubernetes components will be grouped logically using namespace

Note: we can considert namespace as a package in java (dao pkg, service pkg, util pkg, controller pkg)

We can have multiple namespace in k8s cluster
#we can get all namespace using below cmd 
$ kubeclt get namespace or $ kubectl get ns

Note: It is not recommended to run our pods using default namespace .we have to create our own namespace to run our PODS

#create own namespace
$ kubectl create namespace <namespace-name>
eg: 
$ kubectl create namespace sbi-customer-app
$ kubectl create namespace sbi-agent-app 

we can our app in 2 ways
 1.interactive
 2.declarative

 1)interactive - it approach means using cmd we can create pod
  eg: kubectl run --name javawebapppod --image=techimgwithdinesh/java

  2)declerative - it approach means using manifest file (YAML) we can create a pod

  apiVersion:
  kind:
  metadata:
  spec:

  Meaning of the APi, kind ,metadata:
  > apiVersion - represents version of our api like v1,v2,v3
  > kind - represents what is the purpose of this manifest file
  > metadata - represents data about the (labels)
  > spec - represents specification (what you want to use for this manifest)

javawebapppod.yml

apiVersion: v1                # Represents version of the Kubernetes API (v1, v1beta1, etc.)
kind: Pod                    # Represents the type of resource (Here, we're creating a Pod)
metadata:                    # Data about the pod (name, labels, etc.)
  name: javawebapppod        # Name of the pod
  labels:                    # Labels help in grouping and selecting pods
    app: javawebapp          # Label with key 'app' and value 'javawebapp'
spec:                        # Specification of the pod — what it should contain
  containers:
    - name: javawebappcontainer      # Name of the container inside the pod
      image: techwithdinesh/tomcat9  # Image to be used (from Docker Hub or other registry)
      ports:
        - containerPort: 8080        # Port the container exposes
