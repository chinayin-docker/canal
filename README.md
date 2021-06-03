# Canal Base Image

[![Docker Image CI](https://github.com/chinayin-docker/canal/actions/workflows/ci.yml/badge.svg?event=schedule)](https://github.com/chinayin-docker/canal/actions/workflows/ci.yml)
![Docker Image Version (latest semver)](https://img.shields.io/docker/v/chinayin/canal?sort=semver)
![Docker Image Size (latest semver)](https://img.shields.io/docker/image-size/chinayin/canal?sort=semver)
![Docker Pulls](https://img.shields.io/docker/pulls/chinayin/canal)

阿里巴巴 MySQL binlog 增量订阅&消费组件

### Supported tags and respective `Dockerfile` links

![](https://img.shields.io/docker/v/chinayin/canal/1.1.5)

### Image Variants

- `canal:<version>`

### Use Canal

You can use the image directly, e.g.

```
docker run --rm -it chinayin/canal:1.1.5
```

The images are built daily and have the security release enabled, so will contain any security updates released more
than 24 hours ago.

You can also use the images as a base for your own Dockerfile:

```
FROM chinayin/canal:1.1.5
```
