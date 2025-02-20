FROM debian:bookworm

RUN apt-get update && \
    apt-get install -y curl git make unzip gcc xclip ripgrep fontconfig && \
    useradd -ms /bin/bash neo && \
    echo 'FONTFACE="Agave Nerd Font Mono"' >> /etc/default/console-setup && \
    echo 'FONTSIZE="8x16"' >> /etc/default/console-setup

USER neo
WORKDIR /home/neo

COPY ./Agave-nerd-font-v37.zip /home/neo/Agave.zip
COPY ./nvim-linux-x86_64-0.10.4.tar.gz /home/neo/nvim.tar.gz

RUN mkdir -p /home/neo/.local/share/fonts && \
    unzip /home/neo/Agave.zip -d /home/neo/.local/share/fonts && \
    tar xzvf nvim.tar.gz && \
    git clone https://github.com/byronic/kickstart.nvim.git "${XDG_CONFIG_HOME:-$HOME/.config}"/nvim && \
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y && \
    echo 'alias ll="ls -alF"' >> /home/neo/.bashrc && \
    echo 'alias nvim="/home/neo/nvim-linux-x86_64/bin/nvim"' >> /home/neo/.bashrc && \
    . /home/neo/.cargo/env && \
    rustup component add rust-analyzer 

ENTRYPOINT ["tail", "-f", "/dev/null"]
