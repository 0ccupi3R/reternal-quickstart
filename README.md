#  RE:TERNAL
-------------

<img src="https://i.postimg.cc/7hwhx4Dp/reternal.png" alt="Drawing" style="width: 300px;"/>

![version](https://img.shields.io/badge/Version-Alpha_0.0.1-orange.svg)



---------------------

#### Note: Still under development, only use for testing and do not expose interfaces! Current compose doesn't work yet, only try when you know what you're doing #####

RE:TERNAL is a centralised purple team orchestration service to manage third-party C2 frameworks. Agents are installed on endpoints to  to execute various known
red-teaming techniques in order to test blue-teaming capabilities. The simulations are mapped to the MITRE ATT&CK framework. This repo contains
the compose file in order to set up the reternal platform via docker. 



## Reternal components
| Component        | Description | Code           | Build  |
| ------------- |:-------------- |:--------------| :------| 
| [API](https://github.com/d3vzer0/reternal-backend)      | Administrative API to schedule tasks | ![Python](https://img.shields.io/badge/Python-3.6-green.svg) | [![Build Status](https://travis-ci.com/d3vzer0/reternal-backend.svg?branch=development)](https://travis-ci.com/d3vzer0/reternal-backend) |
| [UI](https://github.com/d3vzer0/reternal-ui)     | VueJS-based UI buildscript and NGinx webserver |![VueJS](https://img.shields.io/badge/VueJS-2-green.svg) | [![Build Status](https://travis-ci.com/d3vzer0/reternal-ui.svg?branch=development)](https://travis-ci.com/d3vzer0/reternal-ui)|
| [C2](https://github.com/d3vzer0/reternal-c2) | Seperate API endpoint that agents use to communicate with | ![Python](https://img.shields.io/badge/Python-3.6-green.svg) | [![Build Status](https://travis-ci.com/d3vzer0/reternal-c2.svg?branch=development)](https://travis-ci.com/d3vzer0/reternal-c2) |
| [Mitre](https://github.com/d3vzer0/reternal-mitre)     | Repository containing already existing mapped techniques for reternal |


| Component        | Description | Build  |
| ------------- |:-------------- | :------| 
| Total Stack | Build verifying entire stack via docker-compose in this repository | [![Build Status](https://travis-ci.com/d3vzer0/reternal-quickstart.svg?branch=development)](https://travis-ci.com/d3vzer0/reternal-quickstart) |


## Install and Configuration
This repository contains an Ansible deployment playbook to automate the installation and configuration for Reternal. The guide can be found on the repo's Wiki @ https://github.com/d3vzer0/reternal-quickstart/wiki/1.A-Ansible-Install-Guide. A manual docker-compose file is also available for local testing.


## Devmode
Only use the following steps when developing, services will only be exposed to localhost and no credentials are used:

1. Run the container dependencies: docker-compose up -d mongodb redis empire
2. Run empire and obtain API key: docker exec -ti <empire_container_id> /bin/bash
2b. ./empire --rest
3. Export the token to your environment: export RT_TOKEN_EMPIRE="token_here"
... TODO



## Developers and Contact

Joey Dreijer < joeydreijer@gmail.com >  
Yaleesa Borgman < yaleesa@gmail.com >

## Whats up with the name?

This project has been re-developed so many times, it will probably never really finish. Hence RE (Redo) and Ternal (Eternal).

#### Special Thanks
  - Rabobank DeTTECT - Framework for mapping your log coverage against MITRE ATT&CK. Used the fundementals for the internal coverage rating and scenario suggestions: https://github.com/rabobank-cdc/DeTTECT
  - MITRE ATT&CK - Framework used for mapping simulations: https://attack.mitre.org/wiki/Main_Page
  - Uber Metta -  Using Metta's templates for MITRE techniques with small (optional) adjustments to the purple_action format: https://github.com/uber-common/metta

## Examples and screenshots
All of the features will be documented on the Welcome page of the Wiki @ https://github.com/d3vzer0/reternal-quickstart/wiki. Below are a few examples of the main components.

### Actor / Technique mapping
Reternal automatically maps available commands and techniques to actors. You can directly add all the techniques commonly used by actors to your set of tasks.
<img width="1226" alt="actor_mapping" src="screenshots/actor_mapping.png">

### Recipe / Graph builder
Scheduling tasks to be run on an agent is called a graph. You can add manual commands to a graph or select one of the existing mapped techniques or actor TTPs. You can drag/drop to change the order of the tasks in your graph.

<img width="1180" alt="campaign" src="screenshots/graph_builder.png">

### C2 interaction
Reternal acts as a piece of middleware and interacts with external C2 frameworks. An example is shown below how Reternal manages external listeners and generates stagers.
<img width="1226" alt="actor_mapping" src="screenshots/listener_mgt.png">

<img width="1226" alt="actor_mapping" src="screenshots/stager_builder.png">

### Coverage rating (based on Rabo DeTTECT)
Specify what datasources are available in your environment. Reternal will suggest specific campaigns to execute based on your coverage rating.

<img width="1226" alt="actor_mapping" src="screenshots/dettect_coverage.png">

With an overview of your coverage compared to all the ATT&CK techniques:
<img width="1226" alt="attck_archive" src="screenshots/attck_archive.png">

### Campaign state and dashboard
The main dashboard displays the state of your running campaigns and displays the expected coverage of your datasources vs techniques


<img width="1226" alt="attck_archive" src="screenshots/campaign_state.png">

