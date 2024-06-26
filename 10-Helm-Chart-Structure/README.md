# Understand Helm Chart Folder Structure

- Reference: 
  - https://helm.sh/docs/topics/charts/
  - Start with new tutorial:
    - https://digitalvarys.com/introduction-to-helm-kubernetes-package-manager/
    - https://digitalvarys.com/helm-part-2-helm-chart-files-and-folder-structure-tutorial/

## Step-01: Introduction
- Understand Helm Chart Folder Structure

## Step-02: Helm Create Chart
```t
# Helm Create Chart
helm create <CHART-NAME>
helm create basechart
Observation: 
1. It will create a Helm Chart template 
2. We can call it like a helm chart created from a default starter chart
```

## Step-03: Helm Chart Structure
```
└── basechart
    ├── .helmignore
    ├── Chart.yaml
    ├── LICENSE
    ├── README.md
    ├── charts
    ├── templates
    │   ├── NOTES.txt
    │   ├── _helpers.tpl
    │   ├── deployment.yaml
    │   ├── hpa.yaml
    │   ├── ingress.yaml
    │   ├── service.yaml
    │   ├── serviceaccount.yaml
    │   └── tests
    │       └── test-connection.yaml
    └── values.yaml
```

- The typical folder structure of a Helm chart includes the following directories and files:

  - charts/: This directory contains subcharts that can be included as dependencies in the main chart. Subcharts are themselves Helm charts that can be used to organize and package related resources together.

  - templates/: This directory contains the Kubernetes manifest files that define the resources to be deployed onto the cluster. These files are typically written in YAML format and can include Deployment, Service, ConfigMap, and other types of Kubernetes resources.
    - Just like values and Chart files, we have a template/ folder created under the same directory when you execute the helm create command. This particular folder will have the default folders as mentioned below.

      - NOTE.txt file is like the document file which will be displayed when you run the helm install command.

      - Deployment.yaml will have the manifest to create Kubernetes Deployment objects.

      - Service.yaml is the file which will have the manifest for creating a service endpoint you’re your deployments.

      - _helpers.tpl file will have the re-usable component throughout the chart.

  - values.yaml: This file contains default configuration values for the chart. Users can override these values by providing a custom values file or passing individual values as command line arguments during installation.

  - Chart.yaml: This file contains metadata about the chart, including the chart name, version, description, maintainer information, dependencies, and other details.

  - README.md: This file provides documentation for the chart, including instructions on how to deploy the chart, configure it, and use it effectively.

  - .helmignore: This file specifies files that should be ignored when packaging the chart for deployment. This is useful for excluding temporary files, build artifacts, or other unnecessary files from the chart package.

  - Chart.lock: This file contains information about the exact versions of dependencies that are included in the chart. Helm uses this file to ensure that the same versions of dependencies are used when the chart is deployed on different environments.

Overall, the folder structure of a Helm chart is designed to organize and package the necessary files and resources for deploying applications onto a Kubernetes cluster. By following this structure, users can easily create, share, and deploy Helm charts that encapsulate their applications and services in a reusable and maintainable package.


wordpress/
  Chart.yaml          # A YAML file containing information about the chart
  LICENSE             # OPTIONAL: A plain text file containing the license for the chart
  README.md           # OPTIONAL: A human-readable README file
  values.yaml         # The default configuration values for this chart
  values.schema.json  # OPTIONAL: A JSON Schema for imposing a structure on the values.yaml file
  charts/             # A directory containing any charts upon which this chart depends.
  crds/               # Custom Resource Definitions
  templates/          # A directory of templates that, when combined with values,
                      # will generate valid Kubernetes manifest files.
  templates/NOTES.txt # OPTIONAL: A plain text file containing short usage notes