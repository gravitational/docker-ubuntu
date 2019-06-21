# Customized Docker Ubuntu images

## Customizations

All images are shipped with [dumb-init](https://github.com/Yelp/dumb-init).
The main purpose of it is to manage zombie processes and properly pass signals
into container.

There are also special cleaning script for each image. If you want to keep your
image slim, add this to the end of your Dockerfile:
```dockerfile
RUN test -f /cleanup.sh && sh /cleanup.sh
```

## Ubuntu Tall [![Docker Repository on Quay](https://quay.io/repository/gravitational/ubuntu-tall/status "Docker Repository on Quay")](https://quay.io/repository/gravitational/ubuntu-tall)

Contains:

* libc
* ca-certificates
* busybox

Main purpose of this image is to run Go or static-linked binaries. No package
manager is present.

## Ubuntu Grande [![Docker Repository on Quay](https://quay.io/repository/gravitational/ubuntu-grande/status "Docker Repository on Quay")](https://quay.io/repository/gravitational/ubuntu-grande)

Contains cut debootstrapped system (`minbase` variant). `dpkg` works here.

## Ubuntu Venti [![Docker Repository on Quay](https://quay.io/repository/gravitational/ubuntu-venti/status "Docker Repository on Quay")](https://quay.io/repository/gravitational/ubuntu-venti)

Image with Go build environment and batteries included. For start as Docker-in-docker use `wrapdocker` as entrypoint or just run it inside container.

## Usage

```shell
make ubuntu-tall
make ubuntu-grande
make ubuntu-venti
```

or simply

```shell
make all
```

Also, if you have caching http-proxy you can use it in build:

```shell
http_proxy=http://proxy.addr.ess:port make debian-tall
```
