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
./cbi setup k3s
```

__or__:

```
./cbi setup docker
# (This currently only gives a hint about an external installer.)
```




# Kubernetes apps:

- Gitea
  ```
  ./cbi start k3s/gitea
  ```



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
