FROM jenkins/jnlp-slave

# # install Maven
USER root
RUN apt update -y

RUN apt install -y apt-transport-https  ca-certificates  curl  gnupg2  software-properties-common
RUN curl -fsSL https://apt.dockerproject.org/gpg | apt-key add -
RUN apt-add-repository "deb https://apt.dockerproject.org/repo debian-$(lsb_release -cs) main"
RUN apt-get update
RUN apt-cache policy docker-engine
RUN apt-get install -y docker-engine=1.13.1-0~debian-stretch
VOLUME /root/.docker
RUN cd /usr/bin && curl -LO https://storage.googleapis.com/kubernetes-release/release/v1.17.0/bin/linux/amd64/kubectl
RUN chmod +x /usr/bin/kubectl
COPY config /root/.kube/
RUN wget -O /root/helm.tar.gz https://get.helm.sh/helm-v2.15.2-linux-amd64.tar.gz
RUN cd /root && tar -zxvf helm.tar.gz
RUN cd /root && mv /root/linux-amd64/helm /usr/bin/helm
RUN chmod +x /usr/bin/helm
RUN cp -a /usr/bin/helm /usr/local/bin/helm
RUN helm init --upgrade
USER root