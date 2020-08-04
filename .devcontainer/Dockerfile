## Dockerfile for a haskell environment
FROM haskell:8.6.5

# Configure apt
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
  && apt-get -y install --no-install-recommends apt-utils 2>&1

# Install haskell ide engine dependencies
RUN apt-get -y install libicu-dev libtinfo-dev libgmp-dev zlib1g-dev

# Install ZSH
RUN apt-get -y install zsh

# Create symlink bind directory for build or haskell ide engine
RUN mkdir -p $HOME/.local/bin

# Install haskell language server
RUN stack upgrade \
  && git clone https://github.com/haskell/haskell-language-server --recurse-submodules \
  && cd haskell-language-server \
  && stack install.hs hls-8.6.5 \
  && stack install.hs data || true

# Clean up
RUN apt-get autoremove -y \
  && apt-get clean -y \
  && rm -rf /var/lib/apt/lists/*
ENV DEBIAN_FRONTEND=dialog

# Set the default shell to bash rather than sh
ENV SHELL /bin/zsh