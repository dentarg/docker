FROM ubuntu:18.04
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    # utilities
    ca-certificates \
    git \
    gnupg \
    iproute2 \
    wget \
    # add-apt-repository command
    software-properties-common \
    # for puma
    ragel \
    # for jruby: https://github.com/jruby/jruby/issues/3955#issuecomment-254504589
    netbase \
    # save space
    && rm -rf /var/lib/apt/lists/*

# From https://github.com/actions/virtual-environments/blob/dd518dff50e3ec08dc55c4a63360f53a20549301/images/linux/scripts/installers/java-tools.sh
RUN wget -qO - "https://adoptopenjdk.jfrog.io/adoptopenjdk/api/gpg/key/public" | apt-key add - \
    && add-apt-repository --yes https://adoptopenjdk.jfrog.io/adoptopenjdk/deb/ \
    && apt-get -y install adoptopenjdk-8-hotspot=\* \
    && echo "JAVA_HOME_8_X64=/usr/lib/jvm/adoptopenjdk-8-hotspot-amd64" | tee -a /etc/environment

# Inspiration from https://github.com/cpuguy83/docker-jruby/blob/0fae1b0ed8b70928da49130e3491a531c3d1bb44/9000/jdk8/Dockerfile
ARG JRUBY_VERSION
ENV JRUBY_VERSION="${JRUBY_VERSION}"
RUN mkdir -p /home/runner/.rubies \
  && wget -qO /tmp/jruby.tar.gz https://github.com/ruby/ruby-builder/releases/download/enable-shared/jruby-${JRUBY_VERSION}-ubuntu-18.04.tar.gz \
  && tar -xz -C /home/runner/.rubies -f /tmp/jruby.tar.gz \
  && rm /tmp/jruby.tar.gz
ENV PATH /home/runner/.rubies/jruby-${JRUBY_VERSION}/bin:$PATH

RUN gem install bundler -v "~> 2" --no-document
ENV BUNDLE_SILENCE_ROOT_WARNING=1

CMD ["bash"]
