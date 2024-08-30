FROM ubuntu:20.04

WORKDIR /app

COPY gmt-sources.zip ./

RUN apt-get update && apt-get install -y zip

RUN apt-get install -y curl

SHELL ["/bin/bash", "--login", "-c"]

RUN curl -s "https://get.sdkman.io" | bash

RUN source "/root/.sdkman/bin/sdkman-init.sh"  && \
    sdk install java 8.0.412-amzn && \
    sdk install sbt 1.5.5 && \
    sdk use java 8.0.412-amzn

RUN unzip gmt-sources.zip

ENV NVM_DIR /usr/local/nvm
RUN mkdir -p $NVM_DIR
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
ENV NODE_VERSION v18.18.0
RUN /bin/bash -c "source $NVM_DIR/nvm.sh && nvm install $NODE_VERSION && nvm use --delete-prefix $NODE_VERSION"
ENV NODE_PATH $NVM_DIR/versions/node/$NODE_VERSION/lib/node_modules
ENV PATH      $NVM_DIR/versions/node/$NODE_VERSION/bin:$PATH