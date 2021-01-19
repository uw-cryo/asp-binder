# Ames Stereo Pipeline JupyterHub Image Builder
[![Action Status](https://github.com/uw-cryo/asp-binder/workflows/CI/badge.svg)](https://github.com/uw-cryo/asp-binder/actions)
[![Docker Pulls](https://img.shields.io/docker/pulls/uwcryo/asp-binder)](https://hub.docker.com/r/uwcryo/asp-binder/tags)
![DockerHub Version](https://img.shields.io/docker/v/uwcryo/asp-binder?sort=date)
[![Binder](https://mybinder.org/badge_logo.svg)](https://mybinder.org/v2/gh/uw-cryo/asp-binder/master?urlpath=lab)

### How to use

build with GitHub Actions simply by pushing to GitHub

* pull requests trigger image building without pushing to DockerHub
* commits to master branch (except readme.md changes) trigger re-building image 
* successfully built image is tagged by github sha and 'latest' and pushed to [DockerHub](https://hub.docker.com/r/uwcryo/asp-binder/tags)
```
git commit -a -m "modified binder/environment to my liking"
git push
```

### Run a local JupyterLab session with the latest image
```
# map current directory to jupyterlab home directory
docker run -it --name ASP -p 8888:8888 -v $PWD:/home/jovyan uwcryo/asp-binder:latest jupyter lab --ip 0.0.0.0
docker stop ASP
docker rm ASP
```

### Point to a specific tagged image in JupyterHub config
(uwcryo/asp-binder:b0db94de639a)
https://zero-to-jupyterhub.readthedocs.io/en/latest/reference/reference.html?highlight=profile_list#singleuser-profilelist


### Build locally
```
git clone https://github.com/uw-cryo/asp-binder.git 
cd asp-binder/binder
docker build -t uwcryo/asp-binder:test .
```

