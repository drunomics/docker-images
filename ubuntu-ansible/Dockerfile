FROM ubuntu-upstart:14.04
MAINTAINER Stefan Hageneder <stefan.hageneder@drunomics.com>

ADD ansible_1.9.4-1ppa~trusty_all.deb /root
# Install Ansible and Git.
RUN apt-get update && \
    apt-get install python-support python-jinja2 python-yaml python-paramiko python-httplib2 python-crypto sshpass -y && \
    dpkg -i  /root/ansible_1.9.4-1ppa~trusty_all.deb  && \
    echo '[local]\nlocalhost ansible_connection=local\n' > /etc/ansible/hosts 

RUN mkdir /root/.ssh && \
  ssh-keyscan bitbucket.org  >> /root/.ssh/known_hosts && \
  ssh-keyscan github.com  >> /root/.ssh/known_hosts
