# software_containerization_G43


# Diagram
![image](https://github.com/zhang-mickey/k8s-containerization/assets/145342600/c15b3101-c91a-414c-8839-78a60c222427)

# Prequisites

# Application upgrade and re-deployment
re-build the application after a source code change 
```

```
upgrade the running application in two ways: deployment rollout and canary update
```
```

# PostgreSQL

use a pre-built docker image for this database

the Service exposed by the database is such that it can be accessed by the REST API, but not by users outside of the cluster 

Ensure that the configuration of the database makes use of ConfigMaps and Secrets appropriately

# RESTAPI  
create your own Dockerfile for this image

can read and write to the database

# Web front-end
we build the frontend files into flask application image. 
# Helm Chart
```
How to install?
cd to the location of helm
Run the command: helm install ./grocery-test --generate-name

```
# TLS
use **cert-manager** 
We use a **self-signed ClusterIssuer** to create a self-signed certificates cluster-wide.certificates(signed by a self-made certificate authority). 
Then, use it to bootstrap a **root certificate** which is stored in a secret(root-secret)
Next, we can configure ingress with a certificate signed by CA Issuer. 
Once we have built the TLS connection,we can check whether the application is accessible via https:
```
https://
```
check if http request can be directed to https:
![https](https://github.com/calvinhaooo/software_containerization_G43/assets/145265103/1de732b4-e269-42dc-a3b5-08a21a39e323)
```
http://
```

# Network Policy
For the database, we define a policy which only allows ingress from the flask API.
For the backend, we define a policy which only allows egress to the PostgreSQL.

To test the network policy we have defined:
```
To create a pod with the labels of postgres
sudo microk8s kubectl run test-$RANDOM --rm -i -t --image=alpine --labels="app=postgres" -- sh
Then u will see
If you don't see a command prompt, try pressing enter.
/ #
Type the command
wget -qO- http://grocery-service-1

```



# RBAC
check user permissions as follows

```
sudo microk8s kubectl auth can-i list pod --namespace default --as calvin

sudo microk8s kubectl auth can-i get pod --namespace default --as calvin

sudo microk8s kubectl auth can-i create pod --namespace default --as calvin

sudo microk8s kubectl auth can-i update pod --namespace default --as calvin

```

# google cloud
enable calico k8s network policy
upload the file to the cluster through cloudshell
```
docker build .
```

push the image to the repository, tag it with the repository name and then push the image‘
```
docker tag dockerID us-east1-docker.pkg.dev/poised-rock-413209/grocery/zhang
docker push us-east1-docker.pkg.dev/poised-rock-413209/grocery/zhang
```

```
helm install ./grocery-test --generate-name


```
# commands on Microk8s

```
microk8s enable cert-manager
/etc/hosts
127.0.0.1 mygrocery-g43.com
```
