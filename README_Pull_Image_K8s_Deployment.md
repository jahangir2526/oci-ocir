# Pull Image from Container Registry during Kubernetes Deployment

#### Assumptions

- Image is already available in OCIR



##### 1. Gather Info

```
OCI Username: <oci-username>	# eg: oracleidentitycloudservice/user01_idcs
OCI Auth Token: <oci-auth-token>	
Tenancy Name: <tenancy-name>	
Tenancy Namespace: <tenancy-namespace>	# object storage namespace, eg: ansh81vru1zp

Region Key: <region-key>	# eg: iad

OCIR Docker Username: <tenancy-namespace>/<oci-username>	# eg: ansh81vru1zp/oracleidentitycloudservice/user01_idcs

OCIR Docker Password: <oci-auth-token>

=========================================
OCIR Repo Name: # <ocir-repo-name> # eg: project01/mywebapp
OCIR Repo Compartment: <ocir-comp-name>	#
OCIR Region: <ocir-region> # eg: Mumbai
```

##### 2. Create a Docker registry secret

```
$ kubectl create secret docker-registry <secret-name> --docker-server=<region-key>.ocir.io --docker-username='<tenancy-namespace>/<oci-username>' --docker-password='<oci-auth-token>' --docker-email='<email-address>'

eg:

$ kubectl create secret docker-registry ocirsecret --docker-server=phx.ocir.io --docker-username='ansh81vru1zp/jdoe@acme.com' --docker-password='k]j64r{1sJSSF-;)K8' --docker-email='jdoe@acme.com'
```

##### 3. Refer secret in the manifest file

```
apiVersion: v1
kind: Pod
metadata:
  name: ngnix-image
spec:
  containers:
    - name: ngnix
      image: iad.ocir.io/ansh81vru1zp/project01/mywebapp:v1
      imagePullPolicy: Always
      ports:
      - name: nginx
        containerPort: 8080
        protocol: TCP
  imagePullSecrets:
    - name: ocirsecret
```

