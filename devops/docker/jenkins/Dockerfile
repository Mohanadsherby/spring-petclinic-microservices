# Jenkins with the tools my pipeline needs: docker, kubectl, helm.
FROM jenkins/jenkins:lts

# Installing packages needs root.
USER root

# Docker CLI (talks to the host engine through the mounted socket).
RUN apt-get update && apt-get install -y docker.io curl

# kubectl
RUN curl -LO "https://dl.k8s.io/release/v1.31.3/bin/linux/amd64/kubectl" \
    && chmod +x kubectl \
    && mv kubectl /usr/local/bin/

# helm
RUN curl -fsSL https://get.helm.sh/helm-v3.16.4-linux-amd64.tar.gz | tar xz \
    && mv linux-amd64/helm /usr/local/bin/ \
    && rm -rf linux-amd64

# Let the jenkins user use the docker socket (socket group is root).
RUN usermod -aG root jenkins

# Back to the normal jenkins user.
USER jenkins
