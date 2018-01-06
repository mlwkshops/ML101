# ML101
Machine Learning 101

# Update the JupyterHub notebooks on the server

## Create a new docker image
Changes in this git hub repository need to be reflected in the docker image as well. The docker image comprise of the packages listed in the `requirements.txt` file, and the contents of this repository. A jupyter tool `repo2docker` is used to convert this github repo to a corresponding docker image that we will serve on JupyterHub. This provides an abstraction level for the docker.<br>

Update the corresponding tag after creating a new image. As a best practice use the first 7 digits of the commit SHA as suggested by the jupyterhub documentation<br>
```jupyter-repo2docker https://github.com/mlwkshops/ml101 --image=mlworkshop101/ml101:<TAG> --no-run```
  
## Push the docker image to docker cloud
The docker image that is served on Jupyterhub needs to be available on a public hosting. We are using docker cloud to host the docker image.
**Note**: This step requires docker sign in first<br>
```docker push mlworkshop101/ml101```

## Update in the config.yaml file 
Config.yaml file contains secret tokens, user settings and the docker image reference. The docker image tag can contain a specific tag or `latest`.<br>
```helm upgrade ml101 jupyterhub/jupyterhub --version=v0.5  -f config.yaml```

## Verify setup
Verify that the hub and proxy are running. Also note that for each new user starting their server, a new pod with their username is appearing in the pods list<br>
```kubectl --namespace=ml101 get pod```
<br>
Also verify the running services by<br>
```kubectl --namespace=ml101 get svc```
