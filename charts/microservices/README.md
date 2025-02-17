# helm-charts

# Versioning,makes it easier to upgrade and rollback the many related objects of your application
# Enforce Organizational policies & best practices, allowing teams to standardize how applications are deployed within our organization
# Re-use of existing charts
# Control overall kubernetes resources & their configurations with the possibility of implementing custom logic in the templates
# Custom charts allow you to define deployment configurationstailored to your app.

# Chart.yaml - mandatory, contains metadata of our chart
# Values.yaml - provide values for dynamic helm chart, prevents hardcoding
# Charts - contains any chart dependencies (subcharts). These dependencies should be informed in the chart.yaml file and will be saved and downloaded locally.
# Templates - Contains all kubernetes manifests logic yaml files
    - test : Contains tests to be executed when running the helm test command
    - Notes.txt : Contexts are printed on the screen upon successful chart installation or upgrade
    - _helpers.tpl : Contains template helper functions, which can be used to remove duplication. Files preceded with _ are not included in the final rendering of helm.

A public repository on helm charts that can be used as a plug and play for any deployment strategies

helm repo add <local_chart_name> <hosted_chart_url>
Eg: helm repo add elastic https://helm.elastic.co
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
every repository chart has a index.yaml that contains the metadata of the chart

helm repo update
helm repo --helm 

helm search repo eck-stack # will see the results only from the repo we have added in out system

helm search repo prometheus --max-col-width 20

helm show chart prometheus-community/prometheus

helm show readme prometheus-community/prometheus
helm show values prometheus-community/prometheus #default values.yaml


helm list -A #to list installed releases
helm install <installation_name> <chart_name> -n <namespace>
helm install my-prometheus prometheus-community/prometheus --version 27.1.0
helm install local-wp bitnami/wprdpress --version=23.1.20 \
    --set "mariadb.auth.rootPassword=$mariadbrootPassword" \
    --set mariadb.auth.password=$myuserPassword"
helm install my-prometheus prometheus-community/prometheus --version 27.1.0 --values=custom-values.yaml


helm get noted <installed_name>
helm get metadata <installed_name>

helm get values <installed_name>
helm get values <installed_name> --all
helm upgrade <installation_name> <chart_name> -n <namespace>
helm upgrade <installation_name> . -n <namespace>

helm upgrade --reuse-values --values=custom-values.yaml local-wp bitname/wprdpress --version 23.1.20

helm repo update
helm search repo bitnami/wordpress --vaersions

helm upgrade --reuse-values --values=custom-values.yaml local-wp bitnami/wprdress --version 23.1.28 --atomin --cleanup-on-fail --debug --timeout 2m

helm get values <release_name> --revision 2
helm get values <release_name> --revision 3

28 non-breaking, no new features, patch update
non breaking, new features
might have breaking change

helm history <release_name>
helm get values <release_name>
helm get values <release_name> --revision 1

helm rollback <installation_name> <revision_number> -n <namespace>
helm history <release_name>

helm template . 
helm lint .

{{- hyphens are to remote the extra blank lines added by the conditionals or go comments}}
3 top level keys i.e. values, release and keys. For ex:
{{ .Values.Name}}
{{ .Release.Name}}
{{ .Charts.Name}}

functions
{{ replace " " "-" .Values.test}}
{{ lower .Values.test }}
{{ lower (replace " " "-" .Values.test})}} or {{ replace " " "-" .Values.test | lower}}


kubectl get pods --watch
kubectl get svc
kubectl get secrets
kubectl describe pod <pod_name> -n <namespace>
kubectl expose deploy <pod_name> --type=NodePort --name=<some_name>
kubectl get secret <secret_name> -o jsonpath='{.data.<secret_variable_name>}' | base64 -d


helm list
helm uninstall <installed_name>

kubectl get pods
kubectl get svc
kubectl get secrets

kubectl get pv, pvc

kubectl describe pvc
kubectl describe storageclass standard


