FROM drunomics/lamp-redis:latest
MAINTAINER Stefan Hageneder <hatsch@gmail.com>

ADD requirements.yml /root/docker/drunomics-lamp-redis-solr/
ADD drunomics-lamp-redis-solr.yml /root/playbooks/

WORKDIR /root/docker/drunomics-lamp-redis-solr
RUN ansible-galaxy install -r requirements.yml --force

# Fix issues with connecting to upstart, see
# https://github.com/docker/docker/issues/1024
RUN dpkg-divert --local --rename --add /sbin/initctl && ln -sf /bin/true /sbin/initctl

# Run the playbooks.
WORKDIR /root/playbooks
RUN ansible-playbook drunomics-lamp-redis-solr.yml

# Restore initct.
RUN rm /sbin/initctl && cp /sbin/initctl.distrib /sbin/initctl

RUN apt-get clean && apt-get autoclean -y && apt-get autoremove -y
