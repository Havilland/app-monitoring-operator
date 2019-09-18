# app-monitoring-operator


This ansible operator will deploy prometheus and grafana into an openshift project. It is based on my previous ansible role prometheus-ocp.

More information will follow soon.

## How to build and deploy

For building the operator on OpenShift use the buildconfig in the build folder (buildconfig.yml). 

To use the operator, you can use the following commands:

```bash
oc new-project app-monitor
oc create -f build/buildconfig/buildconfig.yml
oc start-build app-monitor -w
oc create -f deploy/role.yaml
oc create -f deploy/service_account.yaml
oc create -f deploy/role_binding.yaml
oc create -f deploy/crds/appmonitoring_v1_appmonitor_crd.yaml
oc create -f deploy/operator.yaml
oc create -f deploy/crds/appmonitoring_v1_appmonitor-base-install_cr.yaml
```

To use preprovisioned Grafana Dashboards create a ConfigMap with the name `grafana-dashboards` in the project where the custom resource will be used and set `grafana_dashboard_configmap: true` in the AppMonitor CR.

If you want to use a ConfigMap named other than `grafana-dashboards`, set `grafana_dashboard_configmap_name` to the name of the ConfigMap.

## Usage

The operator deploys and configures Prometheus and Grafana into a project. Both deployments use oauth-proxy for authentication. Prometheus will be deployed with the help of prometheus-operator.
