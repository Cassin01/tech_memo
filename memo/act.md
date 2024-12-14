```yaml
title: act
date: 2024-12-14
categories: [programming]
tags: [command]
```


```.actrc
--container-daemon-socket=unix:///var/run/docker.sock
--container-architecture linux/amd64
-P ubuntu-latest-arm64=catthehacker/ubuntu:act-latest
```

```sh
$ act -W .github/workflows/pull_request_to_update.yml -s GITHUB_TOKEN="$(gh auth token)"
```
