# Helm

## References

- https://www.golinuxcloud.com/kubernetes-helm-charts/

- https://phoenixnap.com/kb/what-is-helm

- https://github.com/helm/helm/releases

- https://helm.sh/docs/

## Introduction

- Helm is a Kubernetes deployment tool for automating creation, packaging, configuration, and deployment of applications and services to Kubernetes clusters.

- Kubernetes is a powerful container-orchestration system for application deployment. There are multiple independent resources to deal with, and each requires a dedicated YAML manifest file.

## What is Helm?

- If Kubernetes were an operating system, Helm would be the package manager. Ubuntu uses apt, CentOS uses yum, and Kubernetes uses helm.

- Helm deploys packaged applications to Kubernetes and structures them into charts. The charts contain all pre-configured application resources along with all the versions into one easily manageable package.

- Helm streamlines installing, upgrading, fetching dependencies, and configuring deployments on Kubernetes with simple CLI commands. Software packages are found in repositories or are created.

## Why Do We Need Helm?

- Kubernetes objects are challenging to manage. With helpful tools, the Kubernetes learning curve becomes smooth and manageable. Helm automates maintenance of YAML manifests for Kubernetes objects by packaging information into charts and advertises them to a Kubernetes cluster.

- Helm keeps track of the versioned history of every chart installation and change. Rolling back to a previous version or upgrading to a newer version is completed with comprehensible commands.

  - ![image](https://github.com/nayanrajani/Helm/assets/57224583/052496c0-ff9b-40d8-8d4f-bbc9abc0a33c)

## What Can You Do With Helm?

- Helm allows software developers to deploy and test an environment in the simplest possible way. Less time is needed to get from development to testing to production.

- Besides boosting productivity, Helm presents a convenient way for developers to pack and send applications to end users for installation.

## How Does Helm Work?

- Helm and Kubernetes work like a client/server application. The Helm client pushes resources to the Kubernetes cluster. The server-side depends on the  version: Helm 2 uses Tiller while Helm 3 got rid of Tiller and entirely relies on the Kubernetes API.

  - ![image](https://github.com/nayanrajani/Helm/assets/57224583/abca70b1-2790-4cb4-8ebb-749f77ee8760)

## What Is a Helm Chart?

- Helm charts are Helm packages consisting of YAML files and templates which convert into Kubernetes manifest files. Charts are reusable by anyone for any environment, which reduces complexity and duplicates. Folders have the following structure:

  - ![image](https://github.com/nayanrajani/Helm/assets/57224583/8ba35773-6fa0-401f-af7f-9b3182d7cb02)


## How Do Helm Charts Work?

- The three basic concepts of Helm charts are:

    1. Chart – Pre-configured template of Kubernetes resources.

    2. Release – A chart deployed to a Kubernetes cluster using Helm.

    3. Repository – Publicly available charts.

- The workflow is to search through repositories for charts and install them to Kubernetes clusters, creating releases.

  - Helm Chart Structure

    - The files and directories of a Helm chart each have a specific function:

      - ![image](https://github.com/nayanrajani/Helm/assets/57224583/98b4c68a-3a51-4de2-b39a-ae63c384dcf5)

## Cheat Sheet

- Helm cheatsheet featuring all the necessary commands required to manage an application through Helm.

- Basic interpretations/context

- Chart:
  - It is the name of your chart in case it has been pulled and untarred.
  - It is <repo_name>/<chart_name> in case the repository has been added but chart not pulled.
  - It is the URL/Absolute path to the chart.

- Name:
  - It is the name you want to give to your current helm chart installation.

- Release:
  - Is the name you assigned to an installation instance.

- Revision:
  - Is the value from the Helm history command

- Repo-name:
  - The name of a repository.

- DIR:
  - Directory name/path

### Chart Management

- helm create <name>                      # Creates a chart directory along with the common files and directories used in a chart.
- helm package <chart-path>               # Packages a chart into a versioned chart archive file.
- helm lint <chart>                       # Run tests to examine a chart and identify possible issues:
- helm show all <chart>                   # Inspect a chart and list its contents:
- helm show values <chart>                # Displays the contents of the values.yaml file
- helm pull <chart>                       # Download/pull chart 
- helm pull <chart> --untar=true          # If set to true, will untar the chart after downloading it
- helm pull <chart> --verify              # Verify the package before using it
- helm pull <chart> --version <number>    # Default-latest is used, specify a version constraint for the chart version to use
- helm dependency list <chart>            # Display a list of a chart’s dependencies:

### Install and Uninstall Apps

- helm install <name> <chart>                           # Install the chart with a name
- helm install <name> <chart> --namespace <namespace>   # Install the chart in a specific namespace
- helm install <name> <chart> --set key1=val1,key2=val2 # Set values on the command line (can specify multiple or separate values with commas)
- helm install <name> <chart> --values <yaml-file/url>  # Install the chart with your specified values
- helm install <name> <chart> --dry-run --debug         # Run a test installation to validate chart (p)
- helm install <name> <chart> --verify                  # Verify the package before using it 
- helm install <name> <chart> --dependency-update       # update dependencies if they are missing before installing the chart
- helm uninstall <name>                                 # Uninstall a release

### Perform App Upgrade and Rollback

- helm upgrade <release> <chart>                            # Upgrade a release
- helm upgrade <release> <chart> --atomic                   # If set, upgrade process rolls back changes made in case of failed upgrade.
- helm upgrade <release> <chart> --dependency-update        # update dependencies if they are missing before installing the chart
- helm upgrade <release> <chart> --version <version_number> # specify a version constraint for the chart version to use
- helm upgrade <release> <chart> --values                   # specify values in a YAML file or a URL (can specify multiple)
- helm upgrade <release> <chart> --set key1=val1,key2=val2  # Set values on the command line (can specify multiple or separate valuese)
- helm upgrade <release> <chart> --force                    # Force resource updates through a replacement strategy
- helm rollback <release> <revision>                        # Roll back a release to a specific revision
- helm rollback <release> <revision>  --cleanup-on-fail     # Allow deletion of new resources created in this rollback when rollback fails

### List, Add, Remove, and Update Repositories

- helm repo add <repo-name> <url>   # Add a repository from the internet:
- helm repo list                    # List added chart repositories
- helm repo update                  # Update information of available charts locally from chart repositories
- helm repo remove <repo_name>      # Remove one or more chart repositories
- helm repo index <DIR>             # Read the current directory and generate an index file based on the charts found.
- helm repo index <DIR> --merge     # Merge the generated index with an existing index file
- helm search repo <keyword>        # Search repositories for a keyword in charts
- helm search hub <keyword>         # Search for charts in the Artifact Hub or your own hub instance

### Helm Release monitoring

- helm list                       # Lists all of the releases for a specified namespace, uses current namespace context if namespace not specified
- helm list --all                 # Show all releases without any filter applied, can use -a
- helm list --all-namespaces      # List releases across all namespaces, we can use -A
- helm -l key1=value1,key2=value2 # Selector (label query) to filter on, supports '=', '==', and '!='
- helm list --date                # Sort by release date
- helm list --deployed            # Show deployed releases. If no other is specified, this will be automatically enabled
- helm list --pending             # Show pending releases
- helm list --failed              # Show failed releases
- helm list --uninstalled         # Show uninstalled releases (if 'helm uninstall --keep-history' was used)
- helm list --superseded          # Show superseded releases
- helm list -o yaml               # Prints the output in the specified format. Allowed values: table, json, yaml (default table)
- helm status <release>           # This command shows the status of a named release.
- helm status <release> --revision <number>   # if set, display the status of the named release with revision
- helm history <release>          # Historical revisions for a given release.
- helm env                        # Env prints out all the environment information in use by Helm.

### Download Release Information

- helm get all <release>      # A human readable collection of information about the notes, hooks, supplied values, and generated  manifest file of the given release.
- helm get hooks <release>    # This command downloads hooks for a given release. Hooks are formatted in YAML and separated by the YAML '---\n' separator.
- helm get manifest <release> # A manifest is a YAML-encoded representation of the Kubernetes resources that were generated from this  release's chart(s). If a chart is dependent on other charts, those resources will also be included in the manifest.
- helm get notes <release>    # Shows notes provided by the chart of a named release.
- helm get values <release>   # Downloads a values file for a given release. use -o to format output 

### Plugin Management

- helm plugin install <path/url1>     # Install plugins
- helm plugin list                    # View a list of all installed plugins
- helm plugin update <plugin>         # Update plugins
- helm plugin uninstall <plugin>      # Uninstall a plugin
