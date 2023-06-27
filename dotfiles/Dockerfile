FROM --platform=linux/x86_64 python:3
USER root

#envs
ENV DIR_DEV='/.'

#pip3
RUN pip install --upgrade pip

#many installs
#language
RUN apt update && apt-get update
RUN apt install -y curl git ripgrep tar unzip vim wget zsh tree fzf tmux
RUN apt-get -y install locales && \
    localedef -f UTF-8 -i ja_JP ja_JP.UTF-8
ENV LANG ja_JP.UTF-8
ENV LANGUAGE ja_JP:ja
ENV LC_ALL ja_JP.UTF-8
ENV TZ JST-9
ENV TERM xterm

#nvim install
RUN wget https://github.com/neovim/neovim/releases/download/v0.9.1/nvim-linux64.tar.gz && \
    tar -zxvf nvim-linux64.tar.gz && \
    mv nvim-linux64/bin/nvim usr/bin/nvim && \
    mv nvim-linux64/lib/nvim usr/lib/nvim && \
    mv nvim-linux64/share/nvim/ usr/share/nvim && \
    rm -rf nvim-linux64 && \
    rm nvim-linux64.tar.gz

RUN pip3 install neovim pynvim

RUN git clone https://github.com/sai708th/dotfiles.git

RUN echo 'source /dotfiles/_zshrc' > ~/.zshrc   &&\
    rm ~/.bashrc                                &&\
    echo 'source /dotfiles/_bashrc' > ~/.bashrc 

#XDG Directory Configuration
RUN mkdir /XDG && cd /XDG             &&\
    mkdir cache                       &&\
    mkdir runtime                     &&\
    mkdir config                      &&\
    mkdir config/nvim                 &&\
    mkdir -p data/nvim/site/autoload  &&\
    ln -s /dotfiles/init.vim /XDG/config/nvim/init.vim

#deno
RUN curl -fsSL https://deno.land/install.sh | DENO_INSTALL=/usr/local sh

#env XDG_HOME='/XDG'
#env XDG_CACHE_HOME='/XDG/cache'
#env XDG_DATA_HOME='/XDG/data'
#env XDG_CONFIG_HOME='/XDG/config'
#env XDG_RUNTIME_DIR='/XDG/runtime'

#plug
RUN curl -fLo "${XDG_DATA_HOME:-$HOME/.local/share}"/nvim/site/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
#+ means -c 
#https://github.com/junegunn/vim-plug/issues/675
RUN zsh -ic "nvim +'PlugInstall' +qa"

RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - &&\
    apt install -y nodejs && \
    npm install -g vim-language-server

CMD zsh
