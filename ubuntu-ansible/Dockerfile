FROM ubuntu-upstart:14.04
MAINTAINER Stefan Hageneder <stefan.hageneder@drunomics.com>

# Install Ansible and Git.
RUN apt-get update && \
  apt-get install --no-install-recommends -y software-properties-common && \
  apt-add-repository ppa:ansible/ansible && \
  apt-get update && \
  apt-get install -y ansible git && \
  echo '[local]\nlocalhost ansible_connection=local\n' > /etc/ansible/hosts

RUN mkdir /root/.ssh && \
  ssh-keyscan bitbucket.org  >> /root/.ssh/known_hosts && \
  ssh-keyscan github.com  >> /root/.ssh/known_hosts
