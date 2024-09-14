# nerdctl

**contaiNERD CTL** - Docker-compatible CLI for containerd, with support for Compose, Rootless, eStargz, OCIcrypt, IPFS, ...

## Links
- https://github.com/containerd/nerdctl

## Usage examples
```sh
# root
$ sudo systemctl enable --now containerd
$ sudo nerdctl run -d --name nginx -p 80:80 nginx:alpine

# rootless
$ containerd-rootless-setuptool.sh install
$ nerdctl run -d --name nginx -p 8080:80 nginx:alpine

# To run a container with the default bridge CNI network (10.4.0.0/24):
nerdctl run -it --rm alpine

# To build an image using BuildKit:
nerdctl build -t foo /some-dockerfile-directory
nerdctl run -it --rm foo

# To build and send output to a local directory using BuildKit:
nerdctl build -o type=local,dest=. /some-dockerfile-directory

# To run containers from docker-compose.yaml:
nerdctl compose -f ./examples/compose-wordpress/docker-compose.yaml up

# To list local Kubernetes containers:
nerdctl --namespace k8s.io ps -a
nerdctl --namespace k8s.io container ls

# To build an image for local Kubernetes without using registry:
nerdctl --namespace k8s.io build -t foo /some-dockerfile-directory
kubectl apply -f - <<EOF
apiVersion: v1
kind: Pod
metadata:
  name: foo
spec:
  containers:
  - name: foo
    image: foo
    imagePullPolicy: Never
EOF

# To load an image archive (docker save format or OCI format) into local Kubernetes:
nerdctl --namespace k8s.io load < /path/to/image.tar
```
