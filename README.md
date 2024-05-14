# Access-Control
In this project, you are required to create an AppArmor profile controls how Nginx behaves, as well as restrict a container's access to resources. 
## Overview
[AppArmor](https://ubuntu.com/tutorials/beginning-apparmor-profile-development#1-overview) is a a name-based (path-based) Mandatory Access Control (MAC) based on Linux Security Module (LSM). It can restrict
the permissions of an application through path entries and capability entries.
In this project, you are required to create an AppArmor profile controls how Nginx behaves, as well as restrict a container's access to
resources. Note that this homework is run on Ubuntu 22.04
Here’s some common apparmor APIs
1. `aa-easyprof`: provides an easy to use interface for AppArmor policy generation.
2. `aa-logprof`: an interactive tool used to review AppArmor generated messages and update AppArmor security profiles.

## TO DO 
### Task 1. Permission access
In this section, we will be creating AppArmor profiles to allow safe/index.html and not allowing `unsafe/index.html` We will be using Nginx to apply this task.
#### Task 1.1 Setting up Nginx
1. Install Nginx
2. Move `safe/index.html` and `unsafe/index.html` to the root folder(or any folder as long as you remember to include it within your config file) of your Nginx
3. Remember to provide a screenshot to prove that this section works

#### Task 1.2 Creating AppArmor profile
1. Create an AppArmor profile which allows Nginx to: (Note that the profile name should be nspj-nginx)
> a. Read `safe/index.html`
> <br> b. Restrict Ngnix to read `unsafe/index.html`</br>
> c. Entries required for Nginx to work properly
2. If your profile works, you (any user) should be able to see the contents of safe/index.html while you should not be able to see the contents of `unsafe/index.html`
3. Remember to provide a screenshot to prove that this section works.

### Task 2. Restrict a Container's Access to Resources
Background of this task is that since WordPress and its plugins run as PHP. This means an attacker could upload their own malicious plugin to start a shell on WordPress by simply sending a request to the PHP resource to run the malicious code and spin up the shell. The objective of this task is to apply AppArmor to protect WordPress within a docker . The provided .zip file contains the files required
to setup task 2.
#### Task 2.1 Setting up the container
1. Run the following command
   > a. `sudo apt-get update && apt-get install docker-compose`
   > <br> b. `docker build -t nspj:latest .`</br>
   > c. `docker-compose up`
5. After logging in using the username/password provided from within the `docker-compose.yml` file, try to install any plugin from the left-hand navigation pane to install a plugin. (You should be able to install anything from within the plugin page)
#### Task 2.2 Creating AppArmor profile
Here, we will create a profile which prevents malicious themes and plugins from being uploaded and installed on our WordPress
instance.
1. Create an AppArmor profle named nspj-docker
2. Attach the profile into `docker-compose.yml`
3. The profile should be able to do:
   > a. Allow docker to be hosted normally and wordpress to work as intended.
   > <br> b. Restricting everything under ./wp-content except uploads directory(this is used for media usage)</br>
   > c. No network access (ping, traceroute, etc)
