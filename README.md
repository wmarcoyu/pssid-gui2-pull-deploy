# pssid-gui2-pull-deploy
An Ansible script that pulls pre-built Docker images of pssid-gui2 from Docker Hub
and runs the services.

## Prerequisites
* Ansible is installed locally. If not, install it with
```
sudo apt-get update && sudo apt-get install ansible
```

## Usage
!!! **FOR DEVELOPERS**: change `dockerhub_username` in `playbook.yml` to
an "official" Docker Hub user.

1. *Optionally* open `pssid_gui.conf` and edit the `PSSID_GUI_ROOT_DIR` entry.

This is the root directory of the application.
Note that since you will be directly running
pulled Docker images, the root directory is not for the source code. Instead, it
will have four subdirectories, `bin`, `lib`, `mongo`, and `output`. `bin` contains
the `provision.sh` script. `lib` contains files that the GUI depends on, epsecially
archiver and test options. `mongo` contains the database files that users do not
have to manage explicitly. And `output` contains `hosts.ini` and `pssid_config.json
that the GUI generates.

2. Run the script with
```
ansible-playbook --inventory inventory --ask-become-pass playbook.yml
```
which should generate a `docker-compose.yml` file out of the template, pull the
images from Docker Hub, and start the services.
