FROM ubuntu-upstart:14.04
MAINTAINER Stefan Hageneder <hatsch@gmail.com>

# Install Ansible and git
RUN apt-get update && \
apt-get install --no-install-recommends -y software-properties-common && \
apt-add-repository ppa:ansible/ansible && \
apt-get update && \
apt-get install -y ansible git
RUN echo '[local]\nlocalhost ansible_connection=local\n' > /etc/ansible/hosts

WORKDIR /root/
RUN mkdir .ssh
RUN ssh-keyscan bitbucket.org  >> /root/.ssh/known_hosts
RUN ssh-keyscan github.com  >> /root/.ssh/known_hosts


RUN mkdir -p /root/docker/drunomics-lamp
RUN mkdir -p /root/playbooks

WORKDIR /root
ADD requirements.yml docker/drunomics-lamp/
ADD drunomics-lamp.yml playbooks/

WORKDIR /root/docker/drunomics-lamp
RUN ansible-galaxy install -r requirements.yml --force

#run the playbooks
WORKDIR /root/playbooks
RUN ansible-playbook drunomics-lamp.yml