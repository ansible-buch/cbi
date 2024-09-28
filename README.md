# CBI &ndash; Container-Based Infrastructure

## What is this good for?

- Deploying/managing containerized apps in test labs or small private
  environments
- Supports Docker (via Compose) and K3s


## Requirements:

- Server with at least 4 GB RAM
- Root access on this server
- `ansible`, `curl` and `git` installed on this server


## Clone this repo on your server and ch'dir into directory:

```
git clone https://github.com/ansible-buch/cbi.git
cd cbi
```

## Generate config and review/adjust it:
```
./cbi config

# [Edit env.yml with your favourite editor]
```


## Setup container management platform of your choice:

```
./cbi up k3s/environment
```

__or__:

```
./cbi up docker/environment
# CURRENTLY NOT IMPLEMENTED!
# Please use https://github.com/ansible-buch/docker-installer instead.
```




# Kubernetes apps:

- Gitea
  ```
  ./cbi up k3s/gitea
  ```








# Internals

## Naming of task files:

### Up tasks:
- `U01pre*`
- `U01main*`
- `U01wait*`
- `U01post*`

### Down tasks:
- `D01pre*`
- `D01main*`
- `D01wait*`
- `D01post*`









<!--
## Start apps/init:
```
./cbi start apps/init
```

## Start step-ca (if needed):
```
./cbi start apps/base/step-ca
```

## Start Traefik (the most important part of the puzzle :-)
```
./cbi start apps/base/traefik
```


## Apps:

- Development (Gitea)
  ```
  ./cbi start apps/development/gitea
  ```
