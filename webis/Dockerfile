FROM ubuntu:16.10
MAINTAINER IGAKI

ENV DEBIAN_FRONTEND noninteractive

#set japanese mirror repository for apt
RUN sed -i.bak -e "s%http://archive.ubuntu.com/ubuntu/%http://ftp.iij.ad.jp/pub/linux/ubuntu/archive/%g" /etc/apt/sources.list

#Install and set SSH
RUN apt-get update && apt-get install -y openssh-server
RUN mkdir /var/run/sshd
RUN echo 'root:hoge' | chpasswd
RUN sed -i 's/PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config

# SSH login fix. Otherwise user is kicked off after login
RUN sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

# Upstart and DBus have issues inside docker. 
RUN dpkg-divert --local --rename --add /sbin/initctl && ln -sf /bin/true /sbin/initctl

# Install lxde and add-apt-repository
RUN apt-get install -y lxde software-properties-common

#Install X2Go
RUN add-apt-repository -y ppa:x2go/stable
RUN apt-get update
RUN apt-get install x2goserver x2goserver-xsession x2golxdebindings pwgen firefox pulseaudio libcurl3 libappindicator1 -y
RUN sed -i 's/mesg n || true/tty -s \&\& mesg n/' /root/.profile

# Install Oracle JDK
RUN add-apt-repository -y ppa:webupd8team/java
RUN apt-get update
RUN echo debconf shared/accepted-oracle-license-v1-1 select true | debconf-set-selections
RUN apt-get install -y oracle-java8-installer oracle-java8-set-default

# Install Atom editor
RUN add-apt-repository -y ppa:webupd8team/atom
RUN apt-get update
RUN apt-get install -y atom
RUN apt-get install -y libxss1 libasound2

# Install atom package and bugfix
RUN apm install script
RUN apm install japanese-menu
RUN sed -i 's/BIG-REQUESTS/_IG-REQUESTS/' /usr/lib/x86_64-linux-gnu/libxcb.so.1

# Setup Japanese environment.
RUN cp /usr/share/zoneinfo/Asia/Tokyo /etc/localtime && echo 'Asia/Tokyo' > /etc/timezone && date
RUN echo 'LC_ALL=ja_JP.UTF-8' > /etc/default/locale && echo 'LANG=ja_JP.UTF-8' >> /etc/default/locale &&  locale-gen ja_JP.UTF-8
RUN apt-get install -y ibus-anthy
ENV LC_CTYPE ja_JP.UTF-8

RUN apt-get clean

EXPOSE 22

CMD ["/usr/sbin/sshd", "-D"]
