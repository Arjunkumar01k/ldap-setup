<h1 align="center"><b>LDAP Setup on Podman</b></h1>


## **Requirement** 

[1. Install and configure Ldap 389 DS in the containerised platform with persistence storage][def]

[2. Create organisation keenable.in ][def]
    
[3. Create OU [Dev,Support,POC, Document, Observability]][def]

[4. Create group Admin,Support][def]

[5. Create custom attribute][def]


Environment Info
**Server Info:-**
Os version
NAME="Ubuntu"
VERSION="20.04.6 LTS (Focal Fossa)"
podman version 3.4.2

**Client Info:-**
NAME="Ubuntu"
VERSION="20.04.6 LTS (Focal Fossa)"

Ldap version:- 3

Apache Directory Studio version:- 2.0.0.v20210717-M17

**List of Tools:-**

    1. Podman
    2. Ldap
    3. Apache Directory Studio
   
**LDAP**:- The Lightweight Directory Access Protocol is a communication protocol used to access directory servers and is used to store, update and retrieve data from a directory structure.

**Command for the setup or configuration**

1. Create Bash script for create Pod and container
cat  ldap.sh
Bash script :-
 #!/bin/bash
 #create pod with name ldap389
podman pod create --name ldap389 --publish 3389:3389 --publish 3636:3636
 #create container
podman run -dt\
--pod ldap389 \
--name 389ds-ldap \
-v ~/389ds/data:/data \
-e DS_SUFFIX=dc=keenable, dc=in \
-e DS_DM_PASSWORD=<password> \
docker.io/389ds/dirsrv 
In Pod we have set port 3389 and 3636
In container we have set base Dn as keenable.in and set password of dn


a. Check container list
 **cmd:- podman ps -a –pod**

b. Install Ldap utility on bash machine
**cmd:- sudo apt install ldap-utils**

2.  Setup ApacheDirectory studio for ldap db UI

  a. Install ApacheDirectory studio tar file and extract in directory

  b. Go to new connection and enter some details
ldap connection name
Hostname
ldap port > Press next 
Enter Bind DN name (cn= Directory Manager) 
Enter Bind DN password -> finish



















[def]: #1-install-and-configure-ldap-389-ds-in-the-containerised-platform-with-persistence-storage