# Helm Cheatsheet

> Helm packages, configures, and deploys applications on Kubernetes using charts.

## Table of Contents
- [Repositories](#repositories)
- [Search](#search)
- [Install & Upgrade](#install--upgrade)
- [Release Management](#release-management)
- [Charts](#charts)
- [Templating & Debug](#templating--debug)
- [Values](#values)
- [Rollback](#rollback)
- [Plugins](#plugins)

## Repositories

| Command | Description |
| --- | --- |
| `helm repo add NAME URL` | Add a chart repository. |
| `helm repo list` | List configured chart repositories. |
| `helm repo update` | Refresh local repository indexes. |
| `helm repo remove NAME` | Remove a chart repository. |
| `helm repo index DIRECTORY` | Generate an index file for a chart directory. |
| `helm repo add NAME URL --username USER --password PASS` | Add an authenticated chart repository. |

## Search

| Command | Description |
| --- | --- |
| `helm search repo KEYWORD` | Search configured repositories for charts. |
| `helm search repo CHART --versions` | List all available versions of a chart. |
| `helm search hub KEYWORD` | Search Artifact Hub for public charts. |
| `helm show chart REPO/CHART` | Display a chart's metadata. |
| `helm show values REPO/CHART` | Display a chart's default values. |
| `helm show readme REPO/CHART` | Display a chart's README. |

## Install & Upgrade

| Command | Description |
| --- | --- |
| `helm install RELEASE REPO/CHART` | Install a chart as a new release. |
| `helm install RELEASE REPO/CHART -n NAMESPACE --create-namespace` | Install into a newly created namespace. |
| `helm install RELEASE ./chart -f values.yaml` | Install a local chart with a values file. |
| `helm upgrade RELEASE REPO/CHART` | Upgrade an existing release. |
| `helm upgrade --install RELEASE REPO/CHART` | Install the release when it does not exist. |
| `helm upgrade RELEASE REPO/CHART --set key=value` | Upgrade with an inline value override. |
| `helm upgrade RELEASE REPO/CHART --set-string key=value` | Upgrade while preserving a value as a string. |
| `helm upgrade RELEASE REPO/CHART --atomic --timeout 5m` | Upgrade and roll back automatically on failure. |

## Release Management

| Command | Description |
| --- | --- |
| `helm list` | List releases in the current namespace. |
| `helm list -A` | List releases across all namespaces. |
| `helm status RELEASE` | Show a release's state and resources. |
| `helm get all RELEASE` | Retrieve all stored release information. |
| `helm get manifest RELEASE` | Print the resources rendered for a release. |
| `helm get values RELEASE` | Print user-supplied release values. |
| `helm get values RELEASE --all` | Print computed values including defaults. |
| `helm uninstall RELEASE` | Uninstall a release. |

## Charts

| Command | Description |
| --- | --- |
| `helm create NAME` | Scaffold a new chart directory. |
| `helm package DIRECTORY` | Package a chart directory into a tgz archive. |
| `helm lint DIRECTORY` | Check a chart for common issues. |
| `helm dependency list DIRECTORY` | List a chart's declared dependencies. |
| `helm dependency update DIRECTORY` | Update chart dependencies from repositories. |
| `helm dependency build DIRECTORY` | Rebuild dependencies from Chart.lock. |
| `helm pull REPO/CHART` | Download a chart archive locally. |
| `helm pull REPO/CHART --untar` | Download and extract a chart. |

## Templating & Debug

| Command | Description |
| --- | --- |
| `helm template RELEASE REPO/CHART` | Render templates locally without installing. |
| `helm template RELEASE ./chart -f values.yaml` | Render a local chart with a values file. |
| `helm template RELEASE ./chart --debug` | Render templates with debugging information. |
| `helm install RELEASE ./chart --dry-run --debug` | Simulate an install and show rendered output. |
| `helm upgrade RELEASE ./chart --dry-run --debug` | Simulate an upgrade and show rendered output. |
| `helm lint ./chart --strict` | Treat lint warnings as errors. |

## Values

| Command | Description |
| --- | --- |
| `helm install RELEASE REPO/CHART -f values.yaml` | Install using a custom values file. |
| `helm upgrade RELEASE REPO/CHART -f values.yaml -f prod.yaml` | Merge multiple values files in order. |
| `helm upgrade RELEASE REPO/CHART --reuse-values` | Reuse the last release values during upgrade. |
| `helm upgrade RELEASE REPO/CHART --reset-values` | Reset to chart defaults before applying overrides. |
| `helm upgrade RELEASE REPO/CHART --set-file key=FILE` | Set a value from file contents. |
| `helm upgrade RELEASE REPO/CHART --set-json key='{"enabled":true}'` | Set a value from a JSON object. |

## Rollback

| Command | Description |
| --- | --- |
| `helm history RELEASE` | List revisions for a release. |
| `helm rollback RELEASE REVISION` | Roll back a release to a revision. |
| `helm rollback RELEASE REVISION --wait` | Roll back and wait for resources to become ready. |
| `helm rollback RELEASE REVISION --cleanup-on-fail` | Remove new resources if rollback fails. |
| `helm history RELEASE --max 20` | Limit the number of history entries displayed. |
| `helm uninstall RELEASE --keep-history` | Uninstall while retaining release history. |

## Plugins

| Command | Description |
| --- | --- |
| `helm plugin list` | List installed Helm plugins. |
| `helm plugin install URL` | Install a plugin from a repository URL. |
| `helm plugin update NAME` | Update an installed plugin. |
| `helm plugin uninstall NAME` | Remove an installed plugin. |
| `helm env` | Display Helm environment settings and paths. |
| `helm version` | Show the installed Helm version. |
