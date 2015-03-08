FROM ubuntu-upstart:14.04
MAINTAINER Stefan Hageneder <hatsch@gmail.com>

# Install Ansible and git
RUN apt-get update && \
apt-get install --no-install-recommends -y software-properties-common && \
apt-add-repository ppa:ansible/ansible && \
apt-get update && \
apt-get install -y ansible git
RUN echo '[local]\nlocalhost ansible_connection=local\n' > /etc/ansible/hosts

RUN mkdir /root/.ssh
RUN ssh-keyscan bitbucket.org  >> /root/.ssh/known_hosts
RUN ssh-keyscan github.com  >> /root/.ssh/known_hosts

ADD requirements.yml /root/docker/drunomics-lamp/
ADD drunomics-lamp.yml /root/playbooks/

WORKDIR /root/docker/drunomics-lamp
RUN ansible-galaxy install -r requirements.yml --force

# Fix issues with connecting to upstart, see
# https://github.com/docker/docker/issues/1024
RUN dpkg-divert --local --rename --add /sbin/initctl && ln -s /bin/true /sbin/initctl

# Run the playbooks.
WORKDIR /root/playbooks
RUN ansible-playbook drunomics-lamp.yml

# Restore initct.
RUN rm /sbin/initctl && cp /sbin/initctl.distrib /sbin/initctl

RUN apt-get clean && apt-get autoclean -y && apt-get autoremove -y
