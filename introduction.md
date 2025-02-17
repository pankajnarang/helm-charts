off-shelf, well maintained charts may not exist to support our application
Custom charts allow you to define deployment configurations tailored to your app
versioning makes it easier to upgrade and rollback the many related objects of an application
control over all kubernetes resources and their configurations with the possibility of implementing custom logic in the templates
Reuse existing charts (either community or private) as dependencies for the complex applications, while following best practices

chart.yaml
apiVersion : The chart api version (v1 or v2). For helm 3, use v3
name: The name of the chart
version: the version of the chart (uses semantic versioning)
appVersion: The version of the application enclosed 
description: A brief description of the chart
type: Type of chart(eg, application or library)
keywords: A list of keywords respresentative of the project
dependencies: A list of other chart that the current chart depends on

values.yaml
A yaml file containing default configuration values for the chart.
It's recomended to leverage the values.yaml file as much as possible to avoid hard-coding configuration into the chart


