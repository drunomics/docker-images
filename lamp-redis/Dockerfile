FROM drunomics/lamp:latest
MAINTAINER Stefan Hageneder <stefan.hageneder@drunomics.com>

ADD requirements.yml /root/docker/lamp-redis/
ADD redis.yml /root/playbooks/

WORKDIR /root/docker/lamp-redis
RUN ansible-galaxy install -r requirements.yml --force

# Fix issues with connecting to upstart, see
# https://github.com/docker/docker/issues/1024
RUN dpkg-divert --local --rename --add /sbin/initctl && ln -sf /bin/true /sbin/initctl

# Run the playbooks.
WORKDIR /root/playbooks
RUN ansible-playbook redis.yml

# Restore initct.
RUN rm /sbin/initctl && cp /sbin/initctl.distrib /sbin/initctl

RUN apt-get clean && apt-get autoclean -y && apt-get autoremove -y
