# repo2docker-githubci
a template for building [JupyterHub](https://jupyter.org/hub) environments with [Repo2Docker](https://repo2docker.readthedocs.io/en/latest/) and [GitHub Actions CI](https://help.github.com/en/actions/automating-your-workflow-with-github-actions) 

![Action Status](https://github.com/scottyhq/repo2docker-githubci/workflows/Repo2Docker/badge.svg)
![Docker Pulls](https://img.shields.io/docker/pulls/scottyhq/repo2docker-githubci)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/scottyhq/repo2docker-githubci/master?urlpath=lab)

### How to use

1) click the "Use this template" button to create your own repo

1) create DockerHub account that matches your GitHub username
(could make this configurable)
For example: https://hub.docker.com/u/scottyhq

1) add DOCKER_USERNAME and DOCKER_PASSWORD to repo encrypyted secrets
https://help.github.com/en/actions/automating-your-workflow-with-github-actions/creating-and-using-encrypted-secrets

1) modify readme links and any files in the `binder/` folder

1) build with GitHub Actions by pushing to GitHub
* commits to master branch trigger re-building image tagged by github short sha and 'latest'
```
git commit -a -m "modified binder/environment to my liking"
git push
```
* pushing a tag results in a docker image with the same tag:
```
git tag -am "tagging 2.3.2" 2.3.2
git push --tags
```

### Pull your image to run a local JupyterLab session
```
export IMAGE=scottyhq/repo2docker-github
export TAG=latest
docker pull docker.pkg.github.com/$IMAGE:$TAG
docker run -it --name repo2docker -p 8888:8888 $IMAGE:$TAG jupyter lab --ip 0.0.0.0
docker stop repo2docker
docker rm repo2docker
```

### Run your image on a BinderHub
Now that you have images on DockerHub, you can re-use them in many ways. For example, create a BinderHub compatible content repository with 'binder' branch that points to a specific image. All your notebooks and scripts can be in the 'master' branch, and are pulled into a BinderHub session with [nbgitpuller](https://github.com/jupyterhub/nbgitpuller). Structuring things this way means that changes to your scripts won't trigger rebuilding large images:
https://github.com/scottyhq/githubci-binder-example
