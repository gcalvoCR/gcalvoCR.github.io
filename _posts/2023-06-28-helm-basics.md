---
title: Helm Basics
author: gcalvoCR
date: 2023-06-20 12:00:00 -0600
categories: [concepts, Markdown]
tags: [concepts, md] # tag names should always be lowercase
---

# Helm

Helm is a tool that helps you package, deploy, and manage applications on Kubernetes by providing a streamlined and standardized approach, reducing the complexity of working with Kubernetes resources.

## Main features

1. It serves as a **package manager** for Kubernetes. Helm allows users to manage and distribute applications as packages called charts. It packages YAML Files and distribute them in *public* or *private* repositories.

It is the apt, yum, or homebrew for K8s.

2. It serves as a **templating engine**. It uses *"Go Templates"* underneath. It allows users to define dynamic placeholders or variables within Helm charts. Go Templates provide functionality for parameterization, conditionals, loops, and variable substitution.

## Useful links

 - [Helm HUB](https://artifacthub.io/)
 - [Helm charts GitHub Project](https://github.com/helm/charts)
 - [Installing Helm](https://helm.sh/docs/intro/install/)
 - [Helm v3 release notes](https://helm.sh/blog/helm-3-released/)


 ## Structure

 ```scss
 Chart Name/
├── Chart.yaml
├── values.yaml
├── charts/
│   ├── (dependency1)/
│   ├── (dependency2)/
│   └── ...
├── templates/
│   ├── deployment.yaml
│   ├── service.yaml
│   ├── ingress.yaml
│   └── ...
└── ...
 ```

 ### Explanation of tree structure:
- **-Chart Name**: The root directory of the chart, named after the application or component being packaged.

- **Chart.yaml**: A file that contains metadata about the chart, including the name, version, description, maintainers, and other relevant information.

- **values.yaml**: A file that holds the default or user-defined configuration values for the chart. It allows users to customize the deployment by overriding default values.

- **charts/**: A directory where the dependencies (other charts) of the main chart are stored. Each dependency has its own subdirectory within this directory.

- **templates/**: A directory that contains Kubernetes manifests and templates used to define the desired resources for deploying the application. Templates are written using the Go template language and can include placeholders for dynamic values.


## Commands

Here's a basic list of many useful commands

1. Initialize a new chart:
```sh
helm create <chart-name>
```

2. Install a chart:
 ```sh
helm install <release-name> <chart-name>
```

3. Upgrade a chart:
 ```sh
helm upgrade <release-name> <chart-name>
# example passing values as arguments
helm upgrade --namespace default mysql-release bitnami/mysql --set auth.rootPassword=$ROOT_PASSWORD
# example passing values
helm upgrade --namespace default mydb bitnami/mysql --values values.yaml
# Example to force upgrade
# this option has down time
helm upgrade myserver bitnami/apache --force
# it could be dangling configmaps or secrets
helm upgrade myserver bitnami/apache --cleanup-on-failure

```

4. List installed releases:
 ```sh
helm list
# Examples with specific namespaces
helm list -n teamtwo
helm list --namespace teamtwo
```

5. Uninstall a release:
 ```sh
helm uninstall <release-name>
# When a chart is installed secrets are created to keep the history
# Before helm 3 when uninstalling the secrets were kept, now only if we add the following arg 
helm uninstall <release-name> --keep-history
# Check that by doing
kubectl get secrets
```

6. Fetch and update the latest charts from repositories:
 ```sh
helm repo update
```

7. Search for charts in repositories:
 ```sh
helm search repo <chart-name>
# Example
helm search repo mysql
# Example with versions
helm search repo database --versions
```

8. Inspect the content of a chart:
 ```sh
helm show chart <chart-name>
```

9. Inspect the values defined for a release:
 ```sh
 helm show values <release-name>
 ```

10. Inspect the status of a release:
 ```sh
 helm status <release-name>
 # example
 helm status mydb
 ```

11. Rollback a release to a previous version:
 ```sh
 helm rollback <release-name> <revision-number>
 ```

12. Package a chart:
 ```sh
 helm package <chart-directory>
 ```

13. Install a chart from a local package:
 ```sh
 helm install <release-name> ./<chart-package>.tgz
 # Example
 helm install mydb bitnami/mysql
 # Example using specific version
 helm install my-mongodb bitnami/mongodb --version 10.5.2
 # Example passing args
 helm install mydb bitnami/mysql --set auth.rootPassword
 # Example using values
 helm install --values values.yaml
 # Example to autogenerate the name, rather than providing it
helm install mysrever bitnami/apache --wait 
# Example adding --wait waits to overwrite the default 300s
helm install mysrever bitnami/apache --wait --timeout 5m10s
# Example to automatically rollback if install fails we pass the --atomic option
helm install mysrever bitnami/apache --atomic --wait --timeout 7m12s
# Example to autogenerate the name, rather than providing it
helm install bitnami/apache --generate-name
# to be more specific
helm install bitnami/apache --generate-name --name-template "myserver-{{randAlpha 7 | lower}}"
 ```

14. Check the validity of a chart:
 ```sh
 helm lint <chart-directory>
 ```

15. Customize chart values during installation:
 ```sh
 helm install <release-name> <chart-name> --set key=value
 ```

16. Customize chart values using a values file:
 ```sh
 helm install <release-name> <chart-name> -f <values-file.yaml>
 ```

17. Override specific values using multiple value files:
 ```sh
 helm install <release-name> <chart-name> -f <values-file1.yaml> -f <values-file2.yaml>
 ```

18. Basic listing, adding, removing repo
```sh
helm repo list
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo remove bitnami

```

19. Create a namespace and install helm in that specific namespace
```sh
kubectl create ns teamtwo
helm install -n teamtwo mydb bitnami/mysql
helm install --namespace teamtwo mydb bitnami/mysql
```

20. Dry-runs
```sh
helm install mydb bitnami/mysql --values ./values.yaml --dry-run
```

21. Helm template
```sh
helm template mydb bitnami/mysql --values ./values.yaml
```

The `helm install --dry-run` command **simulates the installation process for a chart without actually installing it**. This command generates the rendered YAML manifests for a chart and prints them to the console, but it does not send the manifests to the Kubernetes API server. This is useful for verifying that the chart is rendered correctly before actually installing it. The --debug flag can also be used with helm install --dry-run to display additional information such as the values that will be used during installation.

The `helm template` command, on the other hand, **generates the rendered YAML manifests for a chart without performing any installation or validation**. This command outputs the rendered YAML manifests to the console, which can be piped to a file or directly applied to a Kubernetes cluster using kubectl apply. The helm template command can be useful when you want to inspect the generated YAML or when you need to customize the generated YAML before installation.


23. To Get manifest
```sh
helm get manifest <releasename>
```