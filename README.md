
<p align="left">
  <img src="https://img.shields.io/github/license/clastix/kubectl"/>
  <a href="https://github.com/clastix/kubectl/releases">
    <img src="https://img.shields.io/github/v/release/clastix/kubectl"/>
  </a>
</p>

<p align="center">
  <img src="assets/logo/kubexarm.png" />
</p>

---

# Kubectl

Your [k8s](https://kubernetes.io) cluster swiss army knife, running in a container.

## Why should you use this?

Because CLASTIX kubectl image is :

- lightweight
- secure
- multiarch

New stable versions will be built and pushed automatically by *GitHub action* [workflow](https://github.com/clastix/kubectl/blob/master/.github/workflows/docker-ci.yml).

### Supported tags

| kubectl | amd64 | arm64 | armv7 |
| :---: | :---: | :---: | :---: |
|v1.20.7| :heavy_check_mark: | :heavy_check_mark: | :heavy_check_mark: |

Keep watching our [quay.io](https://quay.io/repository/clastix/kubectl) repository for latest updates!

---

## Quickstart

### Prerequisites

Make sure you have a containerization software (e.g. _[Docker](https://www.docker.com/)_ ) installed on your device :

```
$ docker version

Client: Docker Engine - Community
 Cloud integration: 1.0.14
 Version:           20.10.6
 API version:       1.41
 Go version:        go1.13.15
 Git commit:        370c289
 Built:             Fri Apr  9 22:46:45 2021
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true
[...]
```

### Take our image

Just pull the desired version from [quay.io](https://quay.io/repository/clastix/kubectl) :

```
$ docker pull quay.io/clastix/kubectl:v1.20.7

v1.20.7: Pulling from clastix/kubectl
540db60ca938: Already exists 
9f38dcb1a41d: Already exists 
71cd9ea851af: Already exists 
Digest: sha256:513848b048dcb2194f1896f56c7a8f6e4a2db8c33b52958a73a09012a1b1a12c
Status: Downloaded newer image for quay.io/clastix/kubectl:v1.20.7
quay.io/clastix/kubectl:v1.20.7
```

or

### Build your own image

running :

```
$ docker build . -t foo/bar/kubectl:v1.20.7 --build-arg KUBECTL_VERSION=v1.20.7
```

or using **Makefile** :
```
$ make docker-build
```
**N.B.** make sure to export desired kubectl version as follow :

```
$ export KUBECTL_VERSION=<desired_version>
```

otherwise, Makefile will retrieve the right tag from branch commit sha;
finally, if no tag comes out, it will use "stable" binary.

### Launch the container

```
$ docker run --name kubectl quay.io/clastix/kubectl:v1.20.7 kubectl version --client

Client Version: version.Info{Major:"1", Minor:"20", GitVersion:"v1.20.7", GitCommit:"132a687512d7fb058d0f5890f07d4121b3f0a2e2", GitTreeState:"clean", BuildDate:"2021-05-12T12:40:09Z", GoVersion:"go1.15.12", Compiler:"gc", Platform:"linux/amd64"}
```

you can also use your own _kubeconfig_

```
$ docker run --name kubectl -v ~/.kube/config:/home/nonroot/.kube/config quay.io/clastix/kubectl:v1.20.7 kubectl get nodes

NAME       STATUS   ROLES                  AGE   VERSION
master01   Ready    control-plane,master   21d   v1.20.7
master02   Ready    control-plane,master   21d   v1.20.7
master03   Ready    control-plane,master   21d   v1.20.7
worker01   Ready    worker                 21d   v1.20.7
worker02   Ready    worker                 21d   v1.20.7
[...]
```

#### Removal
If you want to leave no trace of what appened, just :

1. Remove your kubectl container :

    ```
    $ docker rm kubectl
    ```

3. Remove your kubectl image :

    ```
    $ docker rmi -f quay.io/clastix/kubectl:v1.20.7
    ```

## FAQ
- Q. Does it work with my architecture?

  A. We succesfully tested our kubectl proprietary image on amd and arm architectures; have a look at "[Supported tags](https://github.com/clastix/kubectl#supported-tags)" section for more informations.

- Q. Can I contribute?

  A. Absolutely!

## License

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at :

http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.
