ARG TAG=latest
FROM ataber/ruby_bionic:$TAG

RUN apt-get update --fix-missing \
&&  apt-get upgrade -y --force-yes \
&&  DEBIAN_FRONTEND=noninteractive apt-get install -y --force-yes \
    libssl-dev \
    libomp-dev \
    curl \
    git \
    redis-tools \
    libreadline-dev \
    libpq-dev \
    tzdata \
    libxml2-dev \
    libopenmpi-dev \
&&  apt-get clean \
&&  rm -rf /var/cache/apt/archives/* /var/lib/apt/lists/*

RUN mkdir -p /app
WORKDIR /app

RUN gem install bundler
ENV BUNDLE_GEMFILE=/app/Gemfile \
    BUNDLE_JOBS=2 \
    BUNDLE_PATH=/bundle

# node.js LTS install
RUN curl --silent --location https://deb.nodesource.com/setup_8.x | bash - \
    && apt-get install -y nodejs \
    && npm -g up

EXPOSE 3000
