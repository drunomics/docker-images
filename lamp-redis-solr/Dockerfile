FROM drunomics/lamp-redis:latest
MAINTAINER Stefan Hageneder <stefan.hageneder@drunomics.com>

ADD requirements.yml /root/docker/lamp-redis-solr/
ADD solr.yml /root/playbooks/

RUN cd /root/docker/lamp-redis-solr && \
  ansible-galaxy install -r requirements.yml --force && \

  # Fix issues with connecting to upstart, see
  # https://github.com/docker/docker/issues/1024
  dpkg-divert --local --rename --add /sbin/initctl && ln -sf /bin/true /sbin/initctl && \

  # Run the playbooks.
  cd /root/playbooks && \
  ansible-playbook solr.yml && \

  # Restore initct.
  rm /sbin/initctl && cp /sbin/initctl.distrib /sbin/initctl
