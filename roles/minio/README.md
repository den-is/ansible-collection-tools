# MinIO - object storage solution that provides an AWS S3-compatible API

Install MinIO server, MinIO client tool or both.

"Direct binary installation" is a preffered setup method.

Packages installation is not fully tested.

## MinIO versioning
At the moment of writing MinIO is using ugly and inadequeate versioning.
Also package names differ.
Especially all of this relates to OS Packages.

Minio client command differs if installed from package, `mcli` vs `mc` when installed directly (if note renamed). Probably because `mc` clashes with the original mc "Midnight Commander".
```sh
## Query versions from packages without installation
rpm -qp mc.rpm --queryformat "%{VERSION}"
dpkg-deb -f mc.deb Version

## Check installed packages versions
rpm -q mcli --queryformat "%{VERSION}"
dpkg-query --showformat='${Version}' --show mcli

## of course versions differ from what actual commands return from --version
mcli --version | head -n1
## etc
```

## Installing specific version
By default we install latest version of minio components, either using direct binary intallation approach or deb/rpm packages installation.

Get artifact name/version from either place:
- https://dl.min.io/server/minio/release/linux-amd64/
- https://dl.min.io/client/mc/release/linux-amd64/
- https://dl.min.io/server/minio/release/linux-amd64/archive/
- https://dl.min.io/client/mc/release/linux-amd64/archive/
- https://github.com/minio/minio/releases
- https://github.com/minio/mc/releases

Basically you need to set value to complete artifact name found on releases archive page.
In full name it is meant, value should include full string including component name, version and any extensions.
If using binary installation method, set:

```yaml
minio_install_packages: false # default
minio_server_v: minio.RELEASE.2024-06-13T22-53-53Z
minio_client_v: mc.RELEASE.2024-06-12T14-34-03Z
```

If using packages installatio method, set:

```yaml
minio_install_packages: true
# for RPM:
minio_server_v: minio-20240613225353.0.0-1.x86_64.rpm
minio_client_v: mcli-20240612143403.0.0-1.x86_64.rpm

# for DEB:
minio_server_v: minio_20240613225353.0.0_amd64.deb
minio_client_v: mcli_20240612143403.0.0_amd64.deb
```

## Links
- https://min.io
- https://github.com/minio/minio
- https://github.com/minio/mc
