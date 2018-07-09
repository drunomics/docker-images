FROM ubuntu-upstart:14.04
MAINTAINER drunomics GmbH <hello@drunomics.com>

# Install Ansible and Git.
RUN apt-get update && \
    apt-get install python-support python-jinja2 python-yaml python-paramiko python-httplib2 python-crypto sshpass software-properties-common -y && \
    # Ensure python has SNI support.
    apt-get install python-pip python-openssl python-pyasn1 -y && pip install ndg-httpsclient && \
    # Install ansible, but stick to 2.3 for now.
    add-apt-repository ppa:ansible/ansible-2.3 && apt-get update && \
    apt-get install ansible -y  && \
    echo '[local]\nlocalhost ansible_connection=local\n' > /etc/ansible/hosts 

# Ensure security updates are installed.
RUN unattended-upgrade -d

RUN mkdir /root/.ssh && \
  ssh-keyscan bitbucket.org  >> /root/.ssh/known_hosts && \
  ssh-keyscan github.com  >> /root/.ssh/known_hosts
