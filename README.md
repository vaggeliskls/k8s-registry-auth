# Kubernetes Registry Authentication
This Kubernetes Helm chart is designed to simplify and streamline the process of authenticating with private image repositories for application deployment. This chart is mainly essential when working with Kubernetes, which requires specific authentication procedures to pull private images.

Primarily, this project focuses on tackling the authentication process associated with AWS ECR registries and other Docker-related registries. The supported registries that also have tested are:

1. AWS ECR
2. Nexus
3. JFrog Artifactory
4. Any other Docker-based registry

> AWS ECR registries specifically require re-authentication every 12 hours. Hence, we also include a cronjob in our solution that refreshes this login, ensuring you're always authenticated to your registry.

# Usage
This Helm chart is an OCI-compatible repository located at oci://docker.io/vaggeliskls/k8s-registry-auth. The only required field for this chart is the registry field, which indicates the target registry that you want to authenticate with.

There are two ways to set the credentials for the registry:

1. Use an already defined secret
2. Pass the username and password statically on the values.yaml file

## AWS ECR
For using this Helm chart with AWS ECR, use the following command:

### With existing secret
```
helm upgrade --install k8s-registry-auth oci://docker.io/vaggeliskls/k8s-registry-auth  --set registry=123456789123.dkr.ecr.region.amazonaws.com --set awsEcr.enabled=true --set secretConfigName=secret-name
```
### With static credentials
```
helm upgrade --install k8s-registry-auth oci://docker.io/vaggeliskls/k8s-registry-auth  --set registry=123456789123.dkr.ecr.region.amazonaws.com --set awsEcr.enabled=true --set registryUsername=username --set registryPassword=password
```

Please replace 123456789123.dkr.ecr.region.amazonaws.com with your own AWS ECR registry URL.
You can also use spesific version of this oci repository by adding: `--version 0.5.0`


## Docker Based
For using this Helm chart with generic Docker registries, use the following command:
### With existing secret
```
helm upgrade --install k8s-registry-auth oci://docker.io/vaggeliskls/k8s-registry-auth  --set registry=yourdomain.com --set docker.enabled=true --set secretConfigName=secret-name
```
### With static credentials
```
helm upgrade --install k8s-registry-auth oci://docker.io/vaggeliskls/k8s-registry-auth  --set registry=yourdomain.com --set docker.enabled=true --set registryUsername=username --set registryPassword=password
```

# Debug Helm Template
1. Generate template: `helm template k8s-registry-auth ./ --debug`
2. Debug helm install: `helm upgrade --install k8s-registry-auth ./ --dry-run --namespace test`

# References
- [OCI Registries](https://helm.sh/docs/topics/registries/)
- [Helm command](https://helm.sh/docs/helm/helm_upgrade/)
- [Pull from private registry](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/)