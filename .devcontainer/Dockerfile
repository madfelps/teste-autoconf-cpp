# if you get error: 
# "pull access denied for sha256, repository does not exist or may require 'docker login' : denied: requested access to the resource is denied"
# when opening the project, this may mean that base SDK container has been deleted 
# or that the project has been moved to a different machine where such container does not exist, 
# you can re-build it by pressing F1 in Visual Studio Code and selecting:
# "Torizon: Rebuild SDK and reload in container"
# after this operation you should be able to re-open your project inside a container
FROM cpptesteautoconf_arm64v8-debian-no-ssh_bullseye_debug_9ba52bbc-20a1-49b5-b321-193dcd224e7d_sdk_image

# add automake/autoconf to our base SDK container
RUN apt-get update && apt-get install -y \
    --no-install-recommends --no-install-suggests \
    automake autoconf libtool locales locales-all \
    && apt-get clean && apt-get autoremove \
    && rm -rf /var/lib/apt/lists/*

# avoid warnings when running autotools
ENV LANGUAGE=en_US.UTF-8
ENV LANG=en_US.UTF-8
ENV LC_ALL=en_US.UTF-8

RUN locale-gen en_US.UTF-8 && \
    dpkg-reconfigure --frontend=noninteractive locales && \
    update-locale LANG=en_US.UTF-8

# This is required to allow regular user inside the container to access docker socket
RUN addgroup docker && groupmod --non-unique --gid 136 docker && adduser torizon docker
