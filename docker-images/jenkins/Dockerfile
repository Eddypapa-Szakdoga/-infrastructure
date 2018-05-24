FROM jenkins/jenkins:lts

LABEL maintainer="Adam Toth"

USER root
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update -q && apt-get install -y --no-install-recommends apt-utils && apt-get upgrade -y && apt-get dist-upgrade -y
RUN apt-get install apt-transport-https ca-certificates curl gnupg2 software-properties-common sshpass sudo net-tools -y
RUN curl -fsSL https://download.docker.com/linux/$(. /etc/os-release; echo "$ID")/gpg | sudo apt-key add -
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/$(. /etc/os-release; echo "$ID") $(lsb_release -cs) stable"
RUN apt-get update && apt-get install -y libvirt0 libvirt-clients docker-ce openconnect sudo
RUN gpasswd -a jenkins docker
RUN echo "Defaults    env_reset" > /etc/sudoers && \
    echo "Defaults    mail_badpass" >> /etc/sudoers && \
    echo "Defaults    secure_path=\"/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin\"" >> /etc/sudoers && \
    echo "root        ALL=(ALL:ALL) ALL" >> /etc/sudoers && \
    echo "jenkins     ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
RUN apt-get clean
RUN echo 'DOCKER_OPTS="--insecure-registry localhost:5000"' >> /etc/default/docker
USER jenkins
