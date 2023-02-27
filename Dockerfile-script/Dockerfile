FROM jenkins/jenkins:2.332.3-jdk11

USER root

RUN apt-get update && apt-get install -y lsb-release curl unzip

RUN curl -fsSLo /usr/share/keyrings/docker-archive-keyring.asc \
  https://download.docker.com/linux/debian/gpg

RUN echo "deb [arch=$(dpkg --print-architecture) \
  signed-by=/usr/share/keyrings/docker-archive-keyring.asc] \
  https://download.docker.com/linux/debian \
  $(lsb_release -cs) stable" > /etc/apt/sources.list.d/docker.list

RUN apt-get update && apt-get install -y docker-ce-cli

# Install AWS CLI
RUN curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip" && \
    unzip awscliv2.zip && \
    ./aws/install

# Install necessary packages
RUN apt-get update && apt-get install -y wget unzip python3 python3-pip nodejs npm redis-server && npm install -g npm && rm -rf /var/lib/apt/lists/*

# Install Terraform
ARG TERRAFORM_VERSION=1.1.5
RUN wget -O /tmp/terraform.zip https://releases.hashicorp.com/terraform/${TERRAFORM_VERSION}/terraform_${TERRAFORM_VERSION}_linux_amd64.zip && \
    unzip /tmp/terraform.zip -d /usr/local/bin && \
    rm /tmp/terraform.zip

USER jenkins

RUN jenkins-plugin-cli --plugins "blueocean:1.25.3 docker-workflow:1.28"
