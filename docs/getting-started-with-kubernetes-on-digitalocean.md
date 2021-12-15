# Getting Started With Kubernetes on DigitalOcean

[![Getting Started With Kubernetes on DigitalOcean](https://img.youtube.com/vi/cJKdo-glRD0/0.jpg)](https://www.youtube.com/watch?v=cJKdo-glRD0 "Getting Started With Kubernetes on DigitalOcean")

Learn how to spin up a Kubernetes cluster, deploy an application to the cluster and set up an ingress so that the application is available on the internet.

What You’ll Learn
- Creating and connecting to a DigitalOcean Managed Kubernetes (DOKS) cluster
- Deploying an application into the cluster
- Installing nginx-ingress to expose the application to the internet

|    Time | Description
|--------:|-----------------------------------------------------
|   00:00 | Introduction
|   01:31 | Learning goals today
|   03:54 | Containerize a Python application
|   09:49 | Push the container image to a registry
|   16:20 | Set up a Kubernetes cluster
|   35:15 | Deploy at least 3 replicas of the Python app in the cluster
|   47:40 | Expose the app to the internet
|   56:50 | Estimated costs
|   57:55 | What we've learned today
| 1:01:08 | Reducing costs
| 1:04:32 | CrashLoopBackOff
| 1:05:49 | Summary

Resources: <https://www.digitalocean.com/community/tech_talks/getting-started-with-kubernetes-on-digitalocean>

Presented By
* [Kim Schlesinger](https://www.linkedin.com/in/kimschlesinger/), Developer Advocate, DigitalOcean [Twitter: @kimschles]
* [Mason Egger](https://www.linkedin.com/in/mason-egger/), Senior Developer Advocate, DigitalOcean [Twitter: @megger]

- - - - - - - - - -

New to DigitalOcean? Get US $100 in credit when you sign up: <https://do.co/build​​​​>

Learn and gain inspiration with DigitalOcean Tech Talks: <https://www.digitalocean.com/community/tags/tech-talks>

Subscribe to the DigitalOcean YouTube channel:
<https://www.youtube.com/digitalocean>

Write for DOnations — Share your knowledge and get paid, while supporting tech-focused nonprofits and charities:
<https://www.digitalocean.com/community/pages/write-for-digitalocean>

- - - - - - - - - -

About DigitalOcean<br>
The DigitalOcean Developer Cloud™ simplifies modern app creation for new generations of developers working independently, at tech startups, and within small-to-medium sized businesses around the world.

\#Kubernetes \#DOKS \#DOTechTalks

## Introduction

([Video 00:00](https://www.youtube.com/watch?v=cJKdo-glRD0&t=0s))

### Getting Started with Kubernetes on DigitalOcean

#### DigitalOcean

13 October 2021


## Learning goals today

([Video 01:31](https://www.youtube.com/watch?v=cJKdo-glRD0&t=91s))

### Goals

* Containerize a Python application
* Push the container image to a registry
* Set up a Kubernetes cluster
* Deploy at least 3 replicas of the Python app in the cluster
* (stretch) Expose the app to the internet


## Containerize a Python application

([Video 03:54](https://www.youtube.com/watch?v=cJKdo-glRD0&t=234s))

### Sample Python app

#### Directory listing

```bash
[10:06:31] megger:python-k8s-demo-app git:(main) $ ll
total 16K
-rw-r--r-- 1 megger megger 133 Oct 12 16:41 Dockerfile
-rw-r--r-- 1 megger megger  21 Oct 12 16:40 README.md
-rw-r--r-- 1 megger megger 230 Oct 12 16:45 main.py
-rw-r--r-- 1 megger megger   6 Oct 12 16:40 requirements.txt
```

#### File `main.py`

```python
from flask import Flask
import socket

app = Flask(__name__)

@app.route("/")
def hello():
    hostname = socket.gethostname()
    return f"Hello from {hostname}"


if __name__ == "__main__":
    app.run(host='0.0.0.0', port=8080)
```

#### File `Dockerfile`

```Dockerfile
FROM python

RUN mkdir /app
WORKDIR /app
ADD . /app/
RUN pip install -r requirements.txt

EXPOSE 5000
CMD ["python", "/app/main.py"]
```

#### File `requirements.txt`

```txt
Flask
```

#### Build the Docker image

```bash
docker build -t python-k8s .
``` 

**NOTE**: If you do not have Docker installed

```bash
sudo snap install docker
```

If the "docker" command fails, try prepending it with "sudo".

#### Running it locally inside a Docker container

```bash
docker run -p 8080:8080 python-k8s
```

then launch your browser and open <http://localhost:8080/>

## Push the container image to a registry

([Video 09:49](https://www.youtube.com/watch?v=cJKdo-glRD0&t=589s))

A registry is a place where you can store container images, and there are things like [Docker Hub](https://hub.docker.com/), and there is [Quay](https://quay.io/), and DigitalOcean has a registry called [DOCR](https://www.digitalocean.com/products/container-registry/) which stands for "DigitalOcean Container Registry". We are going to push Mason's images to that registry.

After logging into the [DigitalOcean Control Panel](https://cloud.digitalocean.com/) click on "Container Registry" and choose your preferred plan (there is a free plan to start) to create your own container registry.

We have already created a registry whose URL is `registry.digitalocean.com/sammy`, so we first need to login to the registry using command

```bash
doctl registry login
```

**NOTE**: If you do not have the `doctl` command installed, please refer to <https://docs.digitalocean.com/reference/doctl/how-to/install/>


```bash
docker tag python-k8s registry.digitalocean.com/sammy/python-k8s
docker push registry.digitalocean.com/sammy/python-k8s
```

* Q1(Michael Potter): What software is being used to create this live stream? That is, what are they using to project the screen and web cams?
  - A: [StreamYard](https://streamyard.com/)

* Q2(Gilles Fauvie): If main.py takes a while to execute, do I need kubernetes to be able to get and answer multiple http requests?
  - A: ... You should probably use [uWSGI](https://uwsgi-docs.readthedocs.io/en/latest/) and then Kubernetes

Let's look back at the DO Console and confirm that the image has been pushed to the Container Registry.

TODO


## Set up a Kubernetes cluster

(Video 16:20)

TODO


## (35:15) Deploy at least 3 replicas of the Python app in the cluster

TODO


## (47:40) Expose the app to the internet

TODO


## (56:50) Estimated costs

TODO


## (57:55) What we've learned today

TODO


## (1:01:08) Reducing costs

TODO


## (1:04:32) CrashLoopBackOff

TODO


## (1:05:49) Summary

TODO


<!-- EOF -->
