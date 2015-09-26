FROM debian:jessie

MAINTAINER Arnauld <arnauld.loyer@gmail.com>

ENV UPDATED 2015-09-27

# utf8
ENV LC_ALL C.UTF-8

# Make apt-get happy
ENV DEBIAN_FRONTEND noninteractive

#
# Update list
#
RUN apt-get update

#
# MISC
#
RUN apt-get -y install \
      build-essential \
      software-properties-common \
      git \
      libncurses5-dev \
      openssl \
      libssl-dev \
      wget \
      curl \
      vim \
      tmux \
      colord \
      man \
      zsh

#
# Install Zsh
#
RUN git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh && \
    cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc && \
    chsh -s /bin/zsh

#
# my dotfiles
#
RUN git clone https://github.com/Arnauld/dotfiles.git ~/.dotfiles && \
    chmod +x ~/.dotfiles/setup.sh && \
    ~/.dotfiles/setup.sh

#
# TPP - CLI presentation tool
#
# http://www.ngolde.de/tpp.html
# https://github.com/cbbrowne/tpp

RUN apt-get -y install \
      ruby-full \
      libncurses5-dev \
      toilet \
      figlet

ENV FIGLET_FONTS /usr/share/figlet/

ADD http://www.figlet.org/fonts/bell.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/big.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/bulbhead.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/contessa.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/cyberlarge.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/cybermedium.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/cybersmall.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/doh.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/doom.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/epic.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/ivrit.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/jerusalem.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/ntgreek.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/ogre.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/rectangles.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/serifcap.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/slant.flf ${FIGLET_FONTS}
ADD http://www.figlet.org/fonts/smslant.flf ${FIGLET_FONTS}


RUN gem install curses && \
    gem install ncurses-ruby

RUN cd /usr/src && \
    git clone https://github.com/Arnauld/tpp.git && \
    cd tpp && \
    make install

#
# ERLANG & rebar
#

RUN cd /tmp && \
    wget https://packages.erlang-solutions.com/erlang-solutions_1.0_all.deb && \
    dpkg -i erlang-solutions_1.0_all.deb && \
    apt-get update && \
    apt-get -y install esl-erlang && \
    rm erlang-solutions_1.0_all.deb

RUN wget https://s3.amazonaws.com/rebar3/rebar3 -O /usr/local/bin/rebar3 && \
    chmod +x /usr/local/bin/rebar3 && \
    mkdir -p $HOME/.config/rebar3/ && \
    echo '{plugins, [rebar3_hex]}.' > $HOME/.config/rebar3/rebar.config && \
    rebar3 update && rebar3 plugins upgrade rebar3_hex

CMD ["zsh"]
