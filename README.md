[linuxserverurl]: https://linuxserver.io
[forumurl]: https://forum.linuxserver.io
[ircurl]: https://www.linuxserver.io/irc/
[podcasturl]: https://www.linuxserver.io/podcast/
[appurl]: https://github.com/DobyTang/LazyLibrarian
[hub]: https://hub.docker.com/r/lsioarmhf/lazylibrarian-aarch64/

[![linuxserver.io](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/linuxserver_medium.png)][linuxserverurl]

The [LinuxServer.io][linuxserverurl] team brings you another container release featuring easy user mapping and community support. Find us for support at:
* [forum.linuxserver.io][forumurl]
* [IRC][ircurl] on freenode at `#linuxserver.io`
* [Podcast][podcasturl] covers everything to do with getting the most from your Linux Server plus a focus on all things Docker and containerisation!

# lsioarmhf/lazylibrarian-aarch64
[![](https://images.microbadger.com/badges/version/lsioarmhf/lazylibrarian-aarch64.svg)](https://microbadger.com/images/lsioarmhf/lazylibrarian-aarch64 "Get your own version badge on microbadger.com")[![](https://images.microbadger.com/badges/image/lsioarmhf/lazylibrarian-aarch64.svg)](http://microbadger.com/images/lsioarmhf/lazylibrarian-aarch64 "Get your own image badge on microbadger.com")[![Docker Pulls](https://img.shields.io/docker/pulls/lsioarmhf/lazylibrarian-aarch64.svg)][hub][![Docker Stars](https://img.shields.io/docker/stars/lsioarmhf/lazylibrarian-aarch64.svg)][hub][![Build Status](https://ci.linuxserver.io/buildStatus/icon?job=Docker-Builders/arm64/arm64-lazylibrarian)](https://ci.linuxserver.io/job/Docker-Builders/job/arm64/job/arm64-lazylibrarian/)

[LazyLibrarian][appurl] is a program to follow authors and grab metadata for all your digital reading needs. It uses a combination of Goodreads Librarything and optionally GoogleBooks as sources for author info and book info.  This container is based on the DobyTang fork.

[![lazylibrarian](https://raw.githubusercontent.com/linuxserver/docker-templates/master/linuxserver.io/img/lazylibrarian-icon.png)][appurl]

## Usage

```
docker create \
  --name=lazylibrarian \
  -v <path to data>:/config \
  -v <path to data>:/downloads \
  -v <path to data>:/books \
  -e PGID=<gid> -e PUID=<uid>  \
  -e TZ=<timezone> \
  -p 5299:5299 \
  lsioarmhf/lazylibrarian-aarch64
```

## Parameters

`The parameters are split into two halves, separated by a colon, the left hand side representing the host and the right the container side. 
For example with a port -p external:internal - what this shows is the port mapping from internal to external of the container.
So -p 8080:80 would expose port 80 from inside the container to be accessible from the host's IP on port 8080
http://192.168.x.x:8080 would show you what's running INSIDE the container on port 80.`


* `-p 5299` - Port for webui
* `-v /config` Containers lazylibrarian config and database
* `-v /downloads` lazylibrarian download folder
* `-v /books` location of ebook library
* `-e PGID` for GroupID - see below for explanation
* `-e PUID` for UserID - see below for explanation
* `-e TZ` for setting timezone information, eg Europe/London

It is based on alpine linux with s6 overlay, for shell access whilst the container is running do `docker exec -it lazylibrarian /bin/bash`.

### User / Group Identifiers

Sometimes when using data volumes (`-v` flags) permissions issues can arise between the host OS and the container. We avoid this issue by allowing you to specify the user `PUID` and group `PGID`. Ensure the data volume directory on the host is owned by the same user you specify and it will "just work" ™.

In this instance `PUID=1001` and `PGID=1001`. To find yours use `id user` as below:

```
  $ id <dockeruser>
    uid=1001(dockeruser) gid=1001(dockergroup) groups=1001(dockergroup)
```

## Setting up the application
`IMPORTANT... THIS IS THE ARM64 VERSION`

Access the webui at `<your-ip>:5299/home`, for more information check out [LazyLibrarian][appurl]..

## Info

* To monitor the logs of the container in realtime `docker logs -f lazylibrarian`.

* container version number 

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lazylibrarian`

* image version number

`docker inspect -f '{{ index .Config.Labels "build_version" }}' lsioarmhf/lazylibrarian-aarch64`

## Versions

+ **21.07.17:** Inital Release.
