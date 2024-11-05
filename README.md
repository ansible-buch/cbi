# CBI &ndash; Container-Based Infrastructure

## What is this good for?

- Deploying/managing containerized apps in test labs or small private
  environments
- Supports K3s and Docker

The K3s environment has been successfully tested on:

- Debian 12
- Ubuntu 24.04
- Rocky Linux 9
- openSUSE Leap 15

The Docker environment has been successfully tested on:

- Debian 12

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

### K3s 

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

### Docker

```
sudo ./cbi up docker/environment
```

To additionally grant Docker permissions to a non-privileged user,
add `-e user=USERNAME`:

```
sudo ./cbi up docker/environment -e user=USERNAME
```

If you are currently using this non-privileged account, please
re-login now, so that the new group membership comes into effect.

<br/>


# General usage

- `./cbi up APP_PATH`: Create and start app
- `./cbi down APP_PATH`: Stop and purge app
- `./cbi start APP_PATH`: Start existing app
- `./cbi stop APP_PATH`: Stop existing app


<br/>


# Kubernetes apps

|App |App_Path |Root/sudo? |Login Username |
|---|---|---|---|
|Gitea |`k3s/gitea` |Yes |`root` |
|AWX |`k3s/awx`   |No |`admin` |
|Semaphore |`k3s/semaphore` |No |`admin` |



<br/>

# Docker apps


|App |App_Path |Root/sudo? |Username (Password)|
|---|---|---|---|
|Step-CA |`docker/step-ca` |Yes |- |
|Traefik |`docker/traefik` |No |`admin` |
|Portainer |`docker/portainer` |No |`admin` |
|OpenLDAP |`docker/openldap`|Yes |- |
|SSP (Self Service Password) |`docker/ssp`|No |- |
|Gitea |`docker/gitea` |No |`root` |
|Nextcloud |`docker/nextcloud` |No |`admin` |
|Roundcube |`docker/roundcube` |No |*Mail address* |
|Mailserver |`docker/mailserver` |No |- |
|Guacamole |`docker/guacamole` |No |- |
|BookStack |`docker/bookstack` |No |`admin@admin.com` (`password`)|
|Redmine |`docker/redmine` |No |`admin` (`admin`)|

- Roundcube
  
  FQDN: mail.{{domain}}
- Mailserver

  Only useable with OpenLDAP, Letsencrypt + Roundcube!
  
  FQDN: mail.{{domain}}



<br/>

# Internals

## Content of an app directory:

- `app.yml`: Optional file that contains app-specific informations
  like required permissions or version information
- `blueprint`: contains Jinja-Templates and `info.yml`, which describes
  the transformation sources and targets
- `tasks`: Task files
- `run`: All generated files and bind mounts (in case of Docker)

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

### Start tasks
- `S[0-9][0-9]pre*`
- `S[0-9][0-9]main*`
- `S[0-9][0-9]wait*`
- `S[0-9][0-9]post*`

### Stop tasks
- `K[0-9][0-9]pre*`
- `K[0-9][0-9]main*`
- `K[0-9][0-9]wait*`
- `K[0-9][0-9]post*`


<!--
<br/>

# *Feature ideas*
-->



