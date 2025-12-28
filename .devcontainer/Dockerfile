# https://mcr.microsoft.com/v2/devcontainers/cpp/tags/list
# https://github.com/devcontainers/images/tree/main/src/cpp/history
# https://docs.docker.com/build/building/variables/
ARG GET_ALL_NON_BREAKING_CHANGES=1
ARG ONLY_GET_FIXES=1.2
FROM mcr.microsoft.com/devcontainers/cpp:${GET_ALL_NON_BREAKING_CHANGES}-ubuntu-24.04

# https://cmake.org/download/
ARG REINSTALL_CMAKE_VERSION_FROM_SOURCE="4.2.1"

# Optionally install the cmake for vcpkg
COPY ./reinstall-cmake.sh /tmp/

RUN if [ "${REINSTALL_CMAKE_VERSION_FROM_SOURCE}" != "none" ]; then \
        chmod +x /tmp/reinstall-cmake.sh && /tmp/reinstall-cmake.sh ${REINSTALL_CMAKE_VERSION_FROM_SOURCE}; \
    fi \
    && rm -f /tmp/reinstall-cmake.sh

# [Optional] Uncomment this section to install additional vcpkg ports.
# RUN su vscode -c "${VCPKG_ROOT}/vcpkg install <your-port-name-here>"

# [Optional] Uncomment this section to install additional packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>



# dev
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        gcc-14 g++-14 \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/* \
    && update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-14 1 \
    && update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-14 1

# admin tools
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        ascii \
        bat \
        feh \
        file \
        fish \
        hwinfo \
        lsd \
        mc \
        rename \
        scrot \
        tree \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# dev tools
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        automake \
        bison \
        cmake-format \
        dialog \
        dos2unix \
        doxygen \
        expect \
        flex \
        graphviz \
        mkdocs \
        netpbm \
        shellcheck \
        xa65 \
        xxd \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*
    
# deps
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        autoconf \
        autoconf-archive \
        libtool \
        libgl1-mesa-dev \
        libglu1-mesa-dev \
        python3-jinja2 \
        python3-pip \
        libltdl-dev \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# deps abuse
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        libx11-dev libxft-dev libxext-dev \
        libwayland-dev libxkbcommon-dev libegl1-mesa-dev \
        libibus-1.0-dev \
        # libsdl2-dev libvpx-dev \
        # libxinerama-dev libxcursor-dev xorg-dev libglu1-mesa-dev pkg-config \
        # libasound2-dev libx11-dev libxrandr-dev libxi-dev libgl1-mesa-dev libglu1-mesa-dev libxcursor-dev libxinerama-dev libwayland-dev libxkbcommon-dev \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*

# audio
RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
    && apt-get -y install --no-install-recommends \
        alsa-base \
        alsa-utils \
        beep \
        libsndfile1-dev \
        pulseaudio \
    && apt-get autoremove -y && apt-get clean -y && rm -rf /var/lib/apt/lists/*
    
# starship
RUN curl -fsSL https://starship.rs/install.sh | sh -s -- -y

# zsh config
USER vscode
RUN <<EOF
{
    echo 'eval "$(starship init zsh)"';
    echo 'alias ls="lsd"';
    echo 'alias cat="batcat"';
} >> ~/.zshrc
EOF

ARG GITHUB_BRANCH_NAME="Xenoveritas-abuse"
ENV WORKSPACE_ROOT="/workspaces/${GITHUB_BRANCH_NAME}"
