# Intro to our computing projects

## ML with docker containers

As a first step into develop our computing resources we will develop a docker container with some [python](https://swcarpentry.github.io/python-novice-inflammation/) and [ROOT](https://root.cern/doc/master/group__Tutorials.html) libraries. We will focus on a [modified version](https://github.com/alefisico/machine-learning-das) of [this tutorial](https://indico.cern.ch/event/1088671/timetable/#90-period-5-short-exercise-mac), which contains all the libraries we need for further studies.

The docker container is located in this [Docker Hub repo](https://hub.docker.com/repository/docker/alefisico/echep/general), which can be downloaded as:

```{code-cell}
docker pull alefisico/echep:v0
```

And it can be run as:

```{code-cell}
docker run -it -p 8888:8888 alefisico/echep:v0
```

The output of this will be something like this:

```
...
[C 19:49:38.011 NotebookApp]

    To access the notebook, open this file in a browser:
        file:///home/physicist/.local/share/jupyter/runtime/nbserver-1-open.html
    Or copy and paste one of these URLs:
        http://f722708eb2b8:8888/?token=9071fa4bvasdvfdsvadsvfsvfsdvf
     or http://127.0.0.1:8888/?token=9071fa4bf97dfafwegffdsvfdvsdf

```

The docker will automatically open a `jupyter-notebook` with the notebooks to run, to open in your browser, copy the last link in your browser and open it.

The books need to run the kernel called `python-analysis-env`.

### Data for the tutorials

In this version (v0) of the docker, the data for notebooks 4 and above is located inside the container, in the `data/` folder. This data is located [here](https://cernbox.cern.ch/remote.php/dav/public-files/MBdDqUTlNiRpuLo/data.tar.gz). As a next step, we can try to locate these data outside the container and develop a way to access it through the docker/kubernetes tools.
