FROM drunomics/lamp
MAINTAINER drunomics GmbH <hello@drunomics.com>

ADD requirements.yml /root/docker/lamp-memcached/
ADD memcached.yml /root/playbooks/

# Workaround for build-problems on docker hub.
# See https://github.com/ansible/ansible/issues/13652
RUN rm -rf /etc/php5/mods-available/ansible.ini /etc/php5/mods-available/opcache.ini \
  /etc/php5/mods-available/xhprof.ini /etc/php5/mods-available/xdebug.ini

RUN cd /root/docker/lamp-memcached && \
 ansible-galaxy install -r requirements.yml --no-deps --force && \

  # Fix issues with connecting to upstart, see
  # https://github.com/docker/docker/issues/1024
  dpkg-divert --local --rename --add /sbin/initctl && ln -sf /bin/true /sbin/initctl && \

  # Make sure apt sources are recent.
  apt-get update && \

  # Run the playbooks.
  cd /root/playbooks && \
  ansible-playbook memcached.yml && \

  # Restore initctl.
  rm /sbin/initctl && cp /sbin/initctl.distrib /sbin/initctl && \

  # Clean tmp dirs.
  rm -rf /tmp/* /var/tmp/*
