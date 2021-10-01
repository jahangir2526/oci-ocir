# OCI Container Registry using Docker CLI (Login | Push|Pull Image)



## A. Login using Docker CLI
##### 1. At first gather following information

```
OCI Username: <oci-username>	# eg: oracleidentitycloudservice/user01_idcs
OCI Auth Token: <oci-auth-token>	
Tenancy Name: <tenancy-name>	
Tenancy Namespace: <tenancy-namespace>	# object storage namespace, eg: ansh81vru1zp

Region Key: <region-key>	# eg: iad

OCIR Docker Username: <tenancy-namespace>/<oci-username>	# eg: ansh81vru1zp/oracleidentitycloudservice/user01_idcs

OCIR Docker Password: <oci-auth-token>

```

##### 2. Login to OCIR using docker CLI

```
$ docker login <region-key>.ocir.io
## provide "OCIR Docker Username"
## provide "OCIR Docker Password

```



## B. Push Image using Docker CLI

##### 1. Complete step A1
##### 2. Create OCIR repository using OCI console in desire region and compartment

```
OCIR Repo Name: # <ocir-repo-name> # eg: project01/mywebapp
OCIR Repo Compartment: <ocir-comp-name>	#
OCIR Region: <ocir-region> # eg: Mumbai
```
##### 3. In client machine build the docker image then add a tag

```
## Assuming the image is built in client machine
$ docker images

## tag the image with fully qualified part to target location of OCIR
$ docker tag <image-identifier> <region-key>.ocir.io/<tenancy-namespace>/<ocir-repo-name>:<tag>
eg: docker tag 8e0506e14874 iad.ocir.io/ansh81vru1zp/project01/mywebapp:v1

## login to OCIR, Refer to step A2 # if not done already

## push image from client machine to OCIR
$ docker push iad.ocir.io/ansh81vru1zp/project01/mywebapp:v1
```



## C. Pull Image from Container Registry using Docker CLI
##### 1. Complete A1 (if not done already)
##### 2. Pull the Docker image from Container Registry to the client machine by entering

```
$ docker pull <region-key>.ocir.io/<tenancy-namespace>/<repo-name>:<tag>
eg:
$ docker pull iad.ocir.io/ansh81vru1zp/project01/mywebapp:v1

## check the image was pulled successfully
$ docker image
```
