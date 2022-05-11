# Istio on K8S

This action automates Istio installation using istioctl for Kubernetes based environment. It allows you to create custom config files and deploy it on Kubernetes. Also it has extended kubectl support providing an input that allows you to pick a specific kubectl version that matches with your Kubernetes cluster.

## Inputs
| Input                 | Description                                                         | Default      | Required    |
|-----------------------|---------------------------------------------------------------------|--------------|-------------|
| ```istio_version```   | Istio Version to be downloaded from Istio repo                      | 1.13.3       | ```true```  |
| ```target_arch```     | Target system arch                                                  | x86_64       | ```false``` |
| ```custom_file```     | Path to custom yaml file                                            | custom.yaml  | ```true```  |
| ```kubectl_version``` | Kubectl version required by istioctl to interact with a k8s cluster | latest       | ```false``` |
| ```namespace```       | Target Istio namespace                                              | istio-system | ```false``` |`

## Environment
| Input                 | Description                                                         | Default      | Required    |
|-----------------------|---------------------------------------------------------------------|--------------|-------------|
| ```kubeconfig```   | Kubeconfig file that connects to the k8s cluster                      |        | ```true```  |

A Kubeconfig file must be stored as secret in your repo or in your organization and you must reference in your Workflow. You can find more about how to store encrypted secrets on [GitHub Docs Here](https://docs.github.com/en/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository).

## Example

```yaml
on: [push]
  
jobs:
  deploy:
    runs-on: ubuntu-latest
    name: A job to install a custom istio
    steps:
      - uses: actions/checkout@v3
      - uses: lucasmellos/istio-action@main
        with:
          istio_version: "1.13.3"
          custom_file: "my-config.yaml"
        env:
          kubeconfig: ${{ secrets.KUBECONFIG }} 

```