############################################################################
Project - Docker Management using Ansible
171041004 - 171041006
############################################################################

Follow the below steps in order to deploy docker container to host computers:

############################################################################
Implementation on Master Computer
############################################################################

1)Updated apt-get libraries on the Master computer.

$ sudo apt-get update

2)Installe Docker CE 17.03 package from “https://download.docker.com/linux/ubuntu/dists/xenial/pool/stable/amd64/” using the following command,

$ sudo dpkg -i /path/to/package.deb

3)Create a group for docker which grant root permission and added the user to the group

$ sudo groupadd docker
$ sudo usermod -aG docker $USER

4) To Change Proxy settings for Docker so that we can use it behind the proxy firewall, Create a systemd drop-in directory for the docker service:

$ mkdir -p /etc/systemd/system/docker.service.d

6) Create a file called /etc/systemd/system/docker.service.d/http-proxy.conf that adds the HTTP_PROXY environment variable:

[Service]
Environment="HTTP_PROXY=172.16.19.10:80/"

7)Create a file called /etc/systemd/system/docker.service.d/https-proxy.conf that adds the HTTPS_PROXY environment variable:

[Service]
Environment="HTTPS_PROXY=172.16.19.10:80/"

8)Flush changes & Restart Docker:

$ sudo systemctl daemon-reload
$ sudo systemctl restart docker

9) Installed OpenSSH server and enabled SSH.

$ sudo apt-get install openssh-server

10)Installed Ansible via apt-get

$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo apt-add-repository ppa:ansible/ansible
$ sudo apt-get update
$ sudo apt-get install ansible

11) Installed latest version of ‘docker-py’ and ‘docker-compose’ using pip install.

$ sudo pip install docker-py
$ sudo pip install docker-compose

12) Add host computer information to the Ansible hosts(inventory) file,

$sudo gedit /etc/Ansible/hosts
[lab]
172.16.51.73 ansible_user=test ansible_sudo_pass=test ansible_ssh_pass=test

13) Run the ansible-playbook "sql.yml" present under the src folder to deploy the MySQL docker container on the host machine.

$ ansible-playbook sql.yml

14) Run the ansible-playbook "nginx.yml" present under the src folder to deploy the nginx docker container on the host machine.

$ ansible-playbook nginx.yml


############################################################################
Implementation on Host Computer
############################################################################

1)Create a “test” user with root permissions and set the password.

$ sudo adduser test
$ usermod -aG sudo test

2)Updated apt-get libraries on the host computer.

$ sudo apt-get update

3)Installed Docker CE 17.03 package from “https://download.docker.com/linux/ubuntu/dists/xenial/pool/stable/amd64/” using the following command,

$ sudo dpkg -i /path/to/package.deb

4)Create a group for docker which grant root permission and added the user to the group

$ sudo groupadd docker
$ sudo usermod -aG docker $USER

5)Change Proxy settings for Docker so that we can use it behind the proxy firewall, Create a systemd drop-in directory for the docker service:

$ mkdir -p /etc/systemd/system/docker.service.d

6) Create a file called /etc/systemd/system/docker.service.d/http-proxy.conf that adds the HTTP_PROXY environment variable:

[Service]
Environment="HTTP_PROXY=172.16.19.10:80/"

7) Create a file called /etc/systemd/system/docker.service.d/https-proxy.conf that adds the HTTPS_PROXY environment variable:

[Service]
Environment="HTTPS_PROXY=172.16.19.10:80/"

8) Flush changes & Restart Docker:

$ sudo systemctl daemon-reload
$ sudo systemctl restart docker

9)Installed OpenSSH server and enabled SSH.

$ sudo apt-get install openssh-server

12) Once the image is built and container is created using ansible, we can run the nginx and MySQL containers
$ docker run -it <imagename or image id>

