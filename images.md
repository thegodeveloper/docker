# Docker Images

- App binaries and dependencies.
- Metadata about the image data and how to run the image.
- Official definition: An image is an ordered collection of root filesystem changes and the corresponding execution parameters for use within a container runtime.
- Not a complete OS. No kernel, kernel modules (e.g. drivers).
- Small as one file (your app binary) like a goland static binary.
- Big as an Ubuntu distro with apt, and Apache, PHP and more installed.

## Pull Nginx Image

```shell
docker pull nginx
Using default tag: latest
latest: Pulling from library/nginx
Digest: sha256:28402db69fec7c17e179ea87882667f1e054391138f77ffaf0c3eb388efc3ffb
Status: Image is up to date for nginx:latest
docker.io/library/nginx:latest

What's next:
    View a summary of image vulnerabilities and recommendations → docker scout quickview nginx
```

## List of Docker Images

```shell
docker image list
REPOSITORY                                      TAG                                                                           IMAGE ID       CREATED         SIZE
mysql                                           latest                                                                        22aaacaafc0e   11 days ago     624MB
<none>                                          <none>                                                                        faa4168728b7   13 days ago     49.2MB
mongo                                           latest                                                                        68afe625d91a   2 weeks ago     845MB
nginx                                           alpine                                                                        577a23b5858b   3 weeks ago     50.8MB
nginx                                           latest                                                                        4b196525bd3c   3 weeks ago     197MB
alpine                                          latest                                                                        c157a85ed455   7 weeks ago     8.83MB
bitnami/kafka                                   latest                                                                        868827ee2f82   7 weeks ago     666MB
mariadb                                         latest                                                                        85b6807bea65   7 weeks ago     435MB
registry.k8s.io/metrics-server/metrics-server   v0.7.2                                                                        5548a49bb60b   8 weeks ago     65.5MB
nginx                                           <none>                                                                        195245f0c792   2 months ago    193MB
registry.k8s.io/coredns/coredns                 v1.11.3                                                                       2f6c962e7b83   2 months ago    60.2MB
httpd                                           latest                                                                        721aa0022a96   3 months ago    178MB
httpd                                           <none>                                                                        1d5e4fd251ce   3 months ago    178MB
docker/desktop-kubernetes                       kubernetes-v1.30.2-cni-v1.4.0-critools-v1.29.0-cri-dockerd-v0.3.11-1-debian   5ef3082e902d   3 months ago    419MB
registry.k8s.io/kube-apiserver                  v1.30.2                                                                       84c601f3f72c   4 months ago    112MB
registry.k8s.io/kube-scheduler                  v1.30.2                                                                       c7dd04b1bafe   4 months ago    60.5MB
registry.k8s.io/kube-controller-manager         v1.30.2                                                                       e1dcc3400d3e   4 months ago    107MB
registry.k8s.io/kube-proxy                      v1.30.2                                                                       66dbb96a9149   4 months ago    87.9MB
public.ecr.aws/docker/library/redis             7.2.4-alpine                                                                  7927e7385b93   5 months ago    46.4MB
quay.io/argoproj/argocd                         v2.10.6                                                                       c69bdb1ca593   6 months ago    434MB
zookeeper                                       latest                                                                        c7ecfb51da0f   7 months ago    305MB
registry.k8s.io/etcd                            3.5.12-0                                                                      014faa467e29   8 months ago    139MB
ghcr.io/dexidp/dex                              v2.38.0                                                                       9ba45f47b359   9 months ago    95.9MB
kindest/node                                    v1.29.0                                                                       c5bea7e09f54   10 months ago   872MB
registry.k8s.io/coredns/coredns                 v1.11.1                                                                       2437cf762177   14 months ago   57.4MB
postgres                                        latest                                                                        38da3d5fc5bf   17 months ago   360MB
docker/desktop-vpnkit-controller                dc331cb22850be0cdd97c84a9cfecaf44a1afb6e                                      3750dfec169f   17 months ago   35MB
postgres                                        15.1-alpine                                                                   91c930beec93   21 months ago   241MB
ubuntu                                          14.04                                                                         55b7b4f7c5d6   2 years ago     187MB
registry.k8s.io/pause                           3.9                                                                           829e9de338bd   2 years ago     514kB
elasticsearch                                   8.4.3                                                                         e0856752e5da   2 years ago     682MB
centos                                          7                                                                             c9a1fdca3387   2 years ago     301MB
centos                                          latest                                                                        e6a0117ec169   3 years ago     272MB
edenhill/kcat                                   1.7.0                                                                         19bf67fb247a   3 years ago     38.3MB
docker/desktop-storage-provisioner              v2.0                                                                          c027a58fa0bb   3 years ago     39.8MB
justincormack/nsenter1                          latest                                                                        d598f2517351   3 years ago     118kB
```