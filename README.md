# docker-gitbook-builder

A Docker Image for building ebook with [Gitbook](https://github.com/GitbookIO/gitbook) and [Noto CJK Fonts](https://www.google.com/get/noto/).

Docker Hub: [https://hub.docker.com/r/shuoshuo/gitbook-builder/](https://hub.docker.com/r/shuoshuo/gitbook-builder/)

## Basic

Read the official documentation [GitbookIO/gitbook](https://github.com/GitbookIO/gitbook#how-to-use-it) first.

```bash
# run
docker run -ti --name="gitbook-builder" -v "$PWD:/home" shuoshuo/gitbook-builder /bin/bash
```

## Integrate with Gitlab CI

This docker image is originally designed for generating ebook with [Gitlab CI](https://about.gitlab.com/gitlab-ci/). You could configure your Gitlab CI as following:

```yml
before_script:
  - env
  - export LC_ALL=zh_TW.UTF-8

stages:
  - build

ebook:
  stage: build
  script:
    - gitbook pdf
  artifacts:
    paths:
      - book.pdf
  only:
    - master
  tags:
    - gitbook
  image: shuoshuo/gitbook-builder:latest
  allow_failure: true
```

## Additional Features

This docker image also has [OpenJDK 7](http://openjdk.java.net) installed. The Java runtime allows you to run Gitbook [PlantUML](http://plantuml.com) plugin.

## Customization

To install your own favorite fonts, add the following RUN command in Dockerfile

```bash
## Install Fonts
RUN apt-get update && \
    apt-get install -y --no-install-recommends your-favorite-fonts && \
    rm -rf /var/lib/apt/lists/*
```

## Acknowledge

The project is sponsored under **Productivity Side Project** plan of [ECOWORK Inc.](www.ecowork.com)

[ECOWORK](www.ecowork.com) is a Taiwan-based software and service company and is also hiring now:

* **Cloud Architect**, Cloud Arch Team
* **Cloud Platform Engineer**, Cloud Arch Team
* **iOS/Android Engineer,** Mobile Team
* **Ruby/Go/Node Engineer**, Application Team
* **Operation Engineer**, Service Team

The working location of the above opportunities is Taipei, Taiwan. Resume and inquiry are welcome to resume@ecoworkinc.com.

