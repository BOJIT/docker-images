FROM ubuntu:22.04

# Ensure that we are using bash as default shell
SHELL ["/bin/bash", "-c"]
RUN echo "dash dash/sh boolean false" | debconf-set-selections
RUN DEBIAN_FRONTEND=noninteractive dpkg-reconfigure dash

# Set the locale and timezone
RUN apt-get update && apt-get install -y locales \
    && rm -rf /var/lib/apt/lists/* \
    && locale-gen "en_US.UTF-8"
ENV LANG=en_US.UTF-8 \
    LANGUAGE=en_US:en \
    LC_ALL=en_US.UTF-8 \
    TZ=Etc/UTC
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Install Doxygen + Deps
RUN apt-get update && apt-get install -y \
    doxygen \
    git \
    graphviz \
    perl \
    python3-dev \
    python3-pip

# Install system-wide python with useful build/templating packages
RUN python3 -m pip install \
    gitpython \
    Jinja2 \
    PyYAML

# Install NodeJS
RUN apt-get update && apt-get install curl -y
RUN curl -sL https://deb.nodesource.com/setup_20.x | bash
RUN apt-get install nodejs

# Color terminal
ENV TERM=xterm-256color

# Final cleanup
RUN apt-get autoremove -y
