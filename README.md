# ML101
Machine Learning 101

# How to
## After each update in the config.yaml file 
Config.yaml file contains secret tokens, user settings and the docker image reference.
```helm upgrade jupyterhub/jupyterhub --version=v0.5 --name=ml101 --namespace=ml101 -f config.yaml```

## Creating a new docker image after changes in the github repo
Remember to update the corresponding tag after creating a new image. As a best practice use the first 6 digits of the commit SHA as suggested by the jupyterhub documentation
```jupyter-repo2docker https://github.com/mlwkshops/ml101 --image=mlworkshop101/ml101:<TAG> --no-run```
  
## Push the docker image to docker cloud 
Note: This step requires docker sign in first
```docker push mlworkshop101/ml101```
