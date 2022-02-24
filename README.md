# EPTS docker configuration with nginx reverse proxy (all partners)

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
|           ├── {ariel-v2-dump-file.sql}        # Download 2.x database dumps find link below
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
│   ├── docker-compose.yml              	
│   ├── ariel                           	# Ariel files
│       ├── OpenMRS
|           ├── modules                 	# Folder for 1.x modules
│       ├── webapps
|           ├── ariel.war               	# 1.x war file
|       └── ariel-runtime.properties
│   ├── ccs
|   ...
│
├── v2                                  	# OpenMRS v2.3.3 configuration files
│   ├── docker-compose.yml
│   ├── ariel                           	# Ariel files
│       ├── OpenMRS
|           ├── modules                 	# Folder for 2.x modules
│       ├── webapps
|           ├── ariel.war               	# 2.x war file
|       └── ariel-v2-runtime.properties
│   ├── ccs                             	# CCS  files
|   ...
.
```
# Initial configuration
The following steps will guide you through the process of installing all the technology you need to use the docker configurations available in this project.

1. Install Docker via terminal ```curl https://get.docker.com/ | sh -``` or install Docker using the link below, follow all the steps and most importantly, ensure that there is no previous docker installed while following these instructions.
2. Install Docker Compose, follow all the steps here and use the recommend example version which is the latest stable release.
3. Install Git ```sudo apt install git```
4. Clone the repository for setting up a docker image ```git clone https://github.com/jembi/epts-docker-config.git```
6. Download 1.x database dumps are in [this link](https://drive.google.com/drive/folders/1FnYHrrx0RC7pSyiH4bL1Idyq8xUqX3cC)
7. Download 2.x database dumps are in [this link](https://drive.google.com/drive/folders/1NcEwWuK1L3-sGitbrRpUe7W1sN_isASl)
8. Download 1.x modules from [this link](https://drive.google.com/drive/folders/1PgDwI6URrWeKfT0Sv7cd3JUaIF1nck0y)
9. Download 2.x modules from [this link](https://drive.google.com/drive/folders/1-lK_cA3NiXZIkkwg6OWmXKobyfISlEeH)
10. Download 1.x [war file here](https://drive.google.com/drive/folders/1yFkg5Q5pU116fK7GUkPUU5WblJkrMqjK/) and rename it to partner's name
11. Download 2.x [war file here](https://drive.google.com/drive/folders/1Q0gN17FcohcgQMPc5sORdNuKwEdhZg3S/) and rename it to partner's name
12. Download the [runtime.properties file here](https://drive.google.com/drive/folders/1t0CbpwaZiTLarnYmeA-uwYRPjem3wH7f)
13. Navigate into the dump folder and head to the desired partner folder. Copy and paste the corresponding dump file into the chosen partner folder where you at.
14. In the `nginx` folder, you'll find a `docker-compose.yml` file with only one service for the nginx server to be independent from the other (v1 and v2 folders) compose files. This file defines a new container for nginx and it also does the overriding of the nginx's configuration files.
15. Now switch to the folder of the corresponding OpenMRS version you'd like to configure an instance, i.e. if you are willing to setup an OpenMRS 1.x instance go to folder `v1` else if you are willing to setup an OpenMRS 2.x go to folder `v2`.
16. In the folders v1 and v2 you'll find a `docker-compose.yml` file with the container definitions for the partners instances. Here you can add new resources to the already configured containers or add new containers as you need.
   In the v1 and v2 folders you'll also find folders with the partner's names. These latter have the initial setup files for OpenMRS.

`Tip1`: After downloading a war file, remember to rename it to the corresponding partner name. Ex: fgh.war

`Tip2`: After downloading the openmrs-runtime.properties file, remember to change the connection.url to point to the host and port that you defined in you yml file.

`Tip3`: For reverse proxy, remember to put v1 and v2 instances in the same docker network as nginx.

`Tip4`: Always start your containers first and then start the nginx container, in order to make the instances visible to the nginx proxy.
