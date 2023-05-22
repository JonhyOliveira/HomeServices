FROM ubuntu:latest

RUN rm -rf /var/cache/bind

RUN apt update
RUN apt install bind9 -y

CMD [ "/bin/bash", "/usr/sbin/named", "-f", "-g" ]
