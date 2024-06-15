# Kubernetes Registry Authentication


# Debug Helm Template
1. Generate template: `helm template k8s-registry-auth ./ --debug`
2. Debug helm install: `helm upgrade --install k8s-registry-auth ./ --dry-run --namespace test`