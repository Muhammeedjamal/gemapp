# Explain all file.yaml 
#(secret.yaml)
This YAML snippet defines a Kubernetes Secret object named mongo-secret. Secrets are used to store sensitive information, such as passwords and tokens, in a secure way.

Here's a breakdown of each element:

apiVersion: v1

apiVersion specifies the version of the Kubernetes API used to create this object.
In this case, v1 refers to the stable version of the Kubernetes API.
kind: Secret

kind indicates the type of Kubernetes resource being defined.
Here, Secret specifies that this object is a Secret.
metadata:

metadata is a mandatory field that provides information about the object, including its name, labels, and annotations.
name: mongo-secret

This defines the name of the Secret. This name will be used to reference the Secret in other Kubernetes resources.
type: Opaque

There are two types of Secrets: Opaque and kubernetes.io/dockerconfigjson.
Opaque is used for general-purpose secrets, while kubernetes.io/dockerconfigjson is specifically designed for storing Docker registry credentials.
This Secret is defined as an Opaque type.
data:

data is a map where key-value pairs store the actual secret data.
Each key is the name of a secret value, and its corresponding value is the actual secret data encoded in base64.
This Secret defines two key-value pairs:
mongo-user: This key stores the username for the MongoDB database. Its value is bW9uZ291c2Vy, which translates to "mongo-user" when decoded from base64.
mongo-password: This key stores the password for the MongoDB database. Its value is bW9uZ29wYXNzd29yZA==, which translates to "mongo-password" when decoded from base64.



-------------------------------------------------------------------------
-------------------------------------------------------------------
#mongoapp.yaml 
These YAML snippets define two Kubernetes resources: a Deployment and a Service.

Deployment:

apiVersion: apps/v1 specifies the version of the Kubernetes API used to create the Deployment object.
kind: Deployment indicates that this object is a Deployment.
metadata defines information about the Deployment, including its name and labels:
name: mongo-deployment is the name of the Deployment.
labels: app: mongo defines a label that identifies pods belonging to this Deployment.
spec defines the desired state of the Deployment:
replicas: 1 specifies that the Deployment should run one replica of the container.
selector: matchLabels: app: mongo defines a selector that matches pods with the label app: mongo. This ensures that the Deployment manages only the desired pods.
template defines the pod configuration:
metadata: labels: app: mongo defines the labels for the pods created by this Deployment.
spec: containers: defines the containers to run in each pod:
- name: mongo specifies the name of the container.
image: mongo:5.0 specifies the container image to run.
ports: - containerPort: 27017 defines a port mapping for the container. This maps the container port 27017 to the host port 27017.
env: defines the environment variables for the container:
- name: MONGO_INITDB_ROOT_USERNAME defines the environment variable MONGO_INITDB_ROOT_USERNAME in the container.
valueFrom: secretKeyRef: name: mongo-secret key: mongo-user specifies that the value for this environment variable should be read from the Secret named mongo-secret with the key mongo-user.
- name: MONGO_INITDB_ROOT_PASSWORD defines the environment variable MONGO_INITDB_ROOT_PASSWORD in the container.
valueFrom: secretKeyRef: name: mongo-secret key: mongo-password specifies that the value for this environment variable should be read from the Secret named mongo-secret with the key mongo-password.
Service:

apiVersion: v1 specifies the version of the Kubernetes API used to create the Service object.
kind: Service indicates that this object is a Service.
metadata defines information about the Service, including its name:
name: mongo-service is the name of the Service.
spec defines how the Service exposes its pods to external traffic:
selector: app: mongo defines a selector that matches pods with the label app: mongo. This ensures that the Service exposes only the pods belonging to the mongo-deployment.
ports: - protocol: TCP port: 27017 targetPort: 27017 defines a port configuration for the Service. This exposes the pods' port 27017 on the host port 27017 with the TCP protocol.

