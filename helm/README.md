# Liwo helm-chart

Here you find the helm chart to install Liwo a kubernetes cluster.

## Installation

You need [helm3](https://helm.sh/docs/intro/install/) to install this chart. To install overstroom run the following command.

    helm install <name> <path to liwo helm chart>
    
## Configuration

You can configure the installation by adjusting the values.yaml or by providing your own configuration. All values missing in your own configuration file will be used from the default values.yaml. The --values option in the helm install command can be used to provide your own configuration file:

    helm install --values <path to config.yaml> <name> <path to liwo helm chart>

### configartion options

The following options are available in the values.yaml

- replicacount on top of the values specifies the number of pods for bot backend and geoserver if autoscaling is not enabled
- RWS boolean. Needs to be true in RWS environment
- prefix is added to the names of the different deployments. For instance test/acc/prod
- datasets defines the geoserver data_dir and databasedump used for the installation.
- credentials section has a google service account. This is used to download the datasets
- Use the images section to specify the docker image for backend, database, geoserver adn frontend.
- For each deployment a sections with deployment specific options is defined.
- Ingress section to specify the ingress options.

## Deployment

Installing this chart will give you the following installation in the kubernetes cluster:

 - Geoserver deployment
 - Backend deployment
 - Database deployment
 - Frontend deployment
 - Geoserver service
 - Backend service
 - Database service
 - Frontend service
 - Geoserver configmap
 - Frontend configmap
 - Secret for google storage access
 - ingress

Check pods:

    kubectl get pods

Check deployment:

    kubectl get deployment

Check service:

    kubectl get service

Check configmap:

    kubectl get configmaps

Check ingress

    kubectl get ingress

It can take some time for ingress to be available. First check if all pods are ready. If the pods are ready chec ingress:

    kubectl describe ingress <name>

If ingress marks pods as HEALTHY LIWO should be available on the <ingress.host> adress and geoserver on <ingress.host>/geoserver/

!!! One manual action is to change the geoserver admin password !!!
