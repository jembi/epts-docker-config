# EPTS docker configurations with nginx reverse proxy (all partners)

This repository provides information on how to configure multiple OpenMRS versions 2.3.3 and 1.11.7 instances alongside using non-related docker compose files and publish them through nginx reverse proxy.

The folder structure is as follows:
```
.
├── dump
|   ├── v1                              	# OpenMRS v1.11.7
│       ├── ariel
|           ├── {ariel-dump-file.sql}    	# Download 1.x database dumps find link below
│       ├── ccs
|           ├── {ccs-dump-file.sql}
|       ...
|   ├── v2                             		# OpenMRS v2.3.3
│       ├── ariel
|           ├── {ariel-v2-dump-file.sql}    # Download 2.x database dumps find link below
│       ├── ccs
|           ├── {ccs-v2-dump-file.sql}
|       ...
|
├── nginx
│   ├── docker-compose.yml              	# File to define the services and networks needed
│   ├── empty.conf                      	# File to override nginx's /etc/nginx/conf.d/default.conf
|   └── openmrs-reverse-proxy.conf      	# File with all proxy rules that goes to /etc/nginx/conf.d/
│
├── v1                                  	# OpenMRS v1.11.7 configuration files
│   ├── docker-compose.yml              	# File to define the services and networks needed under OpenMRS v1.11.7
│   ├── ariel                           	# Ariel files
│       ├── OpenMRS
|           ├── modules                 	# Download 1.x modules find link below
│       ├── webapps
|           ├── ariel.war               	# Download 1.x war file and rename it to partner's name
|       └── ariel-runtime.properties
│   ├── ccs
|   ...
│
├── v2                                  	# OpenMRS v2.3.3 configuration files
│   ├── docker-compose.yml              	# File to define the services and networks needed under OpenMRS v2.3.3
│   ├── ariel                           	# Ariel files
│       ├── OpenMRS
|           ├── modules                 	# Download 2.x modules find link below
│       ├── webapps
|           ├── ariel.war               	# Download 2.x war file and rename it to partner's name
|       └── ariel-v2-runtime.properties
│   ├── ccs                             	# CCS  files
|   ...
.
```
# Initial configuration

1. Clone the repo

```sh
git clone https://github.com/jembi/epts-docker-config
```

2. Install Docker and Docker Compose

```sh
Get Docker: https://docs.docker.com/get-docker/
Install Docker Compose: https://docs.docker.com/compose/install/
```
3. 1.x database dumps are in [this link](https://drive.google.com/drive/folders/1FnYHrrx0RC7pSyiH4bL1Idyq8xUqX3cC)
4. 2.x database dumps are in [this link](https://drive.google.com/drive/folders/1NcEwWuK1L3-sGitbrRpUe7W1sN_isASl)
5. Download 1.x modules from [this link](https://drive.google.com/drive/folders/1PgDwI6URrWeKfT0Sv7cd3JUaIF1nck0y)
6. Download 2.x modules from [this link](https://drive.google.com/drive/folders/1-lK_cA3NiXZIkkwg6OWmXKobyfISlEeH)
7. Download 1.x [war file here](https://drive.google.com/drive/folders/1yFkg5Q5pU116fK7GUkPUU5WblJkrMqjK/) and rename it to partner's name
8. Download 2.x [war file here](https://drive.google.com/drive/folders/1Q0gN17FcohcgQMPc5sORdNuKwEdhZg3S/) and rename it to partner's name
9. Switch to the dump folder and head to the desired partner folder. Copy and paste the corresponding dump file into the chosen partner folder where you at.
10. In the `nginx` folder, you'll find a `docker-compose.yml` file with only one service for the nginx server to be independent from the other (v1 and v2 folders) compose files. This file defines a new container for nginx and it also does the overriding of the nginx's configuration files.
11. Now switch to the folder of the corresponding OpenMRS version you'd like to configure an instance, i.e. if you are willing to setup an OpenMRS 1.x instance go to folder `v1` else if you are willing to setup an OpenMRS 2.x go to folder `v2`.
12. In the folders v1 and v2 you'll find a `docker-compose.yml` file with the container definitions for the partners instances. Here you can add new resources to the already configured containers or add new containers as you need.
   In the v1 and v2 folders you'll also find folders with the partner's names. These latter have the initial setup files for OpenMRS.

`Tip1`: After downloading a war file, remember to rename it to the corresponding partner name. Ex: fgh.war

`Tip2`: For reverse proxy, remember to put v1 and v2 instances in the same docker network as nginx.

`Tip3`: Always start your containers first and then start the nginx container, in order to make the instances visible to the nginx proxy.
