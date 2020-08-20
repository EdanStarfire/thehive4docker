FROM ubuntu:latest

# Java Virtual Machine Install
RUN apt-get update \
    && apt-get install -y openjdk-8-jre-headless \
    && echo JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64" >> /etc/environment \
    && export JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64" \
    && apt-get clean

# Fix certificate issues
RUN apt-get update && \
    apt-get install ca-certificates-java && \
    apt-get clean && \
    update-ca-certificates -f;

# User Setup
RUN useradd -m -s /bin/bash thehive

# Attachment Storage
RUN mkdir -p /opt/thp_data/files/thehive \
    && chown -R thehive:thehive /opt/thp_data

# Install TheHive4
RUN apt-get update \
    && apt-get install -y curl gnupg \
    && apt-get clean

RUN curl https://raw.githubusercontent.com/TheHive-Project/TheHive/master/PGP-PUBLIC-KEY | apt-key add - \
    && echo 'deb https://deb.thehive-project.org stable main' >> /etc/apt/sources.list.d/thehive-project.list \
    && apt-get update \
    && apt-get install -y thehive4 \
    && apt-get clean \
    && chown -R thehive:thehive /opt/thehive \
    && chown -R thehive:thehive /opt/thehive4


# Run TheHive4
CMD /opt/thehive/bin/thehive -Dconfig.file=/etc/thehive/application.conf