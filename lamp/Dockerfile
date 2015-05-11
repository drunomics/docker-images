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

ADD requirements.yml /root/docker/lamp/
ADD lamp.yml /root/playbooks/

RUN cd /root/docker/lamp && \
  ansible-galaxy install -r requirements.yml --force && \

  # Fix issues with connecting to upstart, see
  # https://github.com/docker/docker/issues/1024
  dpkg-divert --local --rename --add /sbin/initctl && ln -s /bin/true /sbin/initctl && \

  # Run the playbooks
  cd /root/playbooks && \
  ansible-playbook lamp.yml && \

  # Restore initctl.
  rm /sbin/initctl && cp /sbin/initctl.distrib /sbin/initctl && \

  # Clean tmp dirs.
  rm -rf /tmp/* /var/tmp/* && \

  # Save disk space by removing inno db logfiles.
  rm /var/lib/mysql/ib_logfile*

VOLUME /var/lib/mysql