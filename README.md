# CBI &ndash; Container-Based Infrastructure

## What is this good for?

- Deploying/managing containerized apps in test labs or small private
  environments
- Supports K3s and Docker

It has been successfully tested on:

- Debian 12
- Ubuntu 24.04
- Rocky Linux 9
- openSUSE Leap 15


<br/>

## Requirements

- Server with sufficient RAM, depending on the applications you intend to run
- Firewall/package filters disabled
- `ansible` (community package) and `git` installed on this server

### Special additional requirements on openSUSE:

```
zypper install python3-PyYAML
pip3.11 install kubernetes
```

<br/>

## Clone this repo on your server and ch'dir into directory.

```
git clone https://github.com/ansible-buch/cbi.git
cd cbi
```

## Generate config and review/adjust it.
```
./cbi config

# [Edit env.yml with your favourite editor]
```



## Setup K3s or Docker environment

_Please choose one of the two options. 
Both at the same time is currently not supported!_

### Setup K3s 

You must specify the name the primary network interface.
Add `-e iface=IFACE_NAME`.

```
sudo ./cbi up k3s/environment -e iface=IFACE_NAME
```

To additionally grant Kubernetes access to a non-privileged user,
add `-e user=USERNAME`:

```
sudo ./cbi up k3s/environment -e iface=IFACE_NAME -e user=USERNAME
```

### Setup Docker

```
sudo ./cbi up docker/environment
```

To additionally grant Docker permissions to a non-privileged user,
add `-e user=USERNAME`:

```
sudo ./cbi up docker/environment -e user=USERNAME
```

<br/>


# Kubernetes apps

## Gitea
  ```
  sudo ./cbi up k3s/gitea
  ```
  Username: `root`

## AWX
  ```
  ./cbi up k3s/awx
  ```
  Username: `admin`

## Semaphore
  ```
  ./cbi up k3s/semaphore
  ```
  Username: `admin`




<br/>

# Docker apps

Coming soon!


<br/>

# Internals

## Naming of task files:

### Up tasks
- `U[0-9][0-9]pre*`
- `U[0-9][0-9]main*`
- `U[0-9][0-9]wait*`
- `U[0-9][0-9]post*`

### Down tasks
- `D[0-9][0-9]pre*`
- `D[0-9][0-9]main*`
- `D[0-9][0-9]wait*`
- `D[0-9][0-9]post*`



<br/>

# *Feature ideas*

-
  ```
  ./cbi up/down
  ./cbi start/stop
  
  # (with same meaning as in docker compose)
  ```

- `up/down` commands show somehow "know", whether root permissions are required

- Password in env.yml base64-encoded






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
