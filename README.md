# ☁️ Kubernetes Registry Authentication
This Kubernetes Helm chart is designed to simplify and streamline the process of authenticating with private image repositories for application deployment. This chart is mainly essential when working with Kubernetes, which requires specific authentication procedures to pull private images.

⭐ Don't forget to star the project if it helped you!


# 🗄️ Supported Registries
Primarily, this project focuses on tackling the authentication process associated with AWS ECR registries and other Docker-related registries. The supported registries that also have tested are:

1. [Amazon ECR](https://aws.amazon.com/ecr/)
2. [JFrog Artifactory](https://jfrog.com/artifactory/)
3. [Nexus](https://help.sonatype.com/en/docker-registry.html)
4. [Docker Hub](https://hub.docker.com/)
5. [Harbor](https://goharbor.io/) (Not tested)
6. [IBM Cloud Container Registry](https://www.ibm.com/products/container-registry) (Not tested)
7. [Google Artifact Registry](https://cloud.google.com/artifact-registry) (Future support planned)
8. [Azure Container Registry](https://azure.microsoft.com/en-us/products/container-registry) (Future support planned)

> AWS ECR registries specifically require re-authentication every `12 hours`. Hence, we also include a cronjob in our solution that refreshes this login, ensuring you're always authenticated to your registry.

# 📋 Prerequisites
Ensure [Helm](https://helm.sh/docs/intro/install/) version 3 or higher is installed on your system.

# 🚀 Usage
Our Helm chart is an OCI-compatible repository located at `oci://registry-1.docker.io/vaggeliskls/k8s-registry-auth`. When using this chart, the only mandatory configuration is the `registry` field, denoting your targeted registry for authentication.

There are two ways to set the credentials for the registry:

1. Use an existing secret
2. Provide the username and password statically in the values.yaml file

## Examples
1. [AWS ECR Example (Existing Secret)](https://github.com/vaggeliskls/k8s-registry-auth/wiki/Examples#aws-ecr-example-existing-secret)
2. [AWS ECR Example (Existing Secret)](https://github.com/vaggeliskls/k8s-registry-auth/wiki/Examples#aws-ecr-example-existing-secret)
3. [Docker Example (Existing Secret)](https://github.com/vaggeliskls/k8s-registry-auth/wiki/Examples#docker-example-existing-secret)
4. [Docker Example (Static Credentials)](https://github.com/vaggeliskls/k8s-registry-auth/wiki/Examples#docker-example-static-credentials)

## AWS ECR
For using this Helm chart with AWS ECR, use the following command:

**Existing secret**
```
helm upgrade --install k8s-registry-auth oci://registry-1.docker.io/vaggeliskls/k8s-registry-auth  --set registry=123456789123.dkr.ecr.region.amazonaws.com --set awsEcr.enabled=true --set secretConfigName=secret-name
```
**Static credentials**
```
helm upgrade --install k8s-registry-auth oci://registry-1.docker.io/vaggeliskls/k8s-registry-auth  --set registry=123456789123.dkr.ecr.region.amazonaws.com --set awsEcr.enabled=true --set registryUsername=username --set registryPassword=password
```

Please replace 123456789123.dkr.ecr.region.amazonaws.com with your own AWS ECR registry URL.
You can also use spesific version of this oci repository by adding: `--version 1.0.0`


## Docker Based
For using this Helm chart with generic Docker registries, use the following command:

**Existing secret**
```
helm upgrade --install k8s-registry-auth oci://registry-1.docker.io/vaggeliskls/k8s-registry-auth  --set registry=yourdomain.com --set docker.enabled=true --set secretConfigName=secret-name
```
**Static credentials**
```
helm upgrade --install k8s-registry-auth oci://registry-1.docker.io/vaggeliskls/k8s-registry-auth  --set registry=yourdomain.com --set docker.enabled=true --set registryUsername=username --set registryPassword=password
```

# 🐞 Debug Helm Template
To debug your Helm template:
1. Generate template: `helm template k8s-registry-auth ./ --debug`
2. Debug helm install: `helm upgrade --install k8s-registry-auth ./ --dry-run --namespace test`

# 📚 Further Reading and Resources
- [OCI Registries](https://helm.sh/docs/topics/registries/)
- [Helm command](https://helm.sh/docs/helm/helm_upgrade/)
- [Pull from private registry](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)