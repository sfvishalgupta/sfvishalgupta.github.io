#### [Back](./README.md)

# Helm Chart

Helm Chart is a package manager for K8 that similifies the process of installing, upgradin, and managing applications on a K8 Cluster

A Helm Chart is a collection of templates and configuration files thata defines a deployable application on a K8 Cluster. Charts can be thought of as a packaged application that can be easily installed, upgraded and managed.

## Components of a Help Chart
1. **values.yaml:** A file that defines the default values for the chart.
2. **Chart.yaml**: A file that defines the chart's metadata, such as its name, version, and description.
3. **requirements.yaml:** A file that defines the chart's dependencies.
4. **templates:** A directory that contains template files for kuberneters resources, such as Deployment, Services, and ConfigMaps.
5. **hooks** A directory that contains hook scripts that can be executed during the chart's installation, upgrade.or deletion.

## Benefits of Using Helm Charts
1. **Easy application deployment:** Helm Charts simplify the process of deploying applications on a Kubernetes cluster.
2. **Versioning and upgrades:** Helm Charts allow you to easily manage different versions of an application and upgrade or downgrade as needed.
3. **Dependency management:** Helm Charts can manage dependencies between applications, making it easier to deploy complex applications.
4. **Reusability:** Helm Charts can be reused across different environments and clusters.

## Popular Helm Chart Repositories
1. **Helm Hub:** The official Helm Chart repository, which provides a wide range of charts for popular applications.
2. **Bitnami:** A popular repository that provides charts for a wide range of applications, including databases, messaging queues, and more.
3. **Stable:** A repository that provides charts for stable and widely-used applications.

## Tools for Working with Helm Charts
1. **Helm CLI:** The official command-line tool for working with Helm Charts.
2. **Helmfile:** A tool that allows you to manage multiple Helm Charts and dependencies in a single file.
3. **Chart Museum:** A tool that allows you to manage and store Helm Charts in a centralized repository.

## Installing a Helm Chart via CLI

```bash
brew install helm
```

## Important command 

* ### Create a template
```bash
helm create webapp
```

* ### Install a chart
```bash
helm install webapp-release webapp
```

* ### Upgrade a chart
```bash
helm upgrade webapp-release webapp
```

* ### Uninstall a release
```bash
helm unstall webapp-release
helm delete webapp-release
```

* ### List all Release
```bash
helm ls
helm list
```
* ### Status of a Release
```bash
helm status webapp-release
```

* ### Get Release
```bash
helm get webapp-release
```









