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
