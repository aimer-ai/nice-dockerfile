FROM ubuntu:18.04

ARG LOGIN_PASSWORD=123456

RUN apt-get update && apt-get install -y openssh-server
RUN mkdir -p /var/run/sshd \
  && echo "root:${LOGIN_PASSWORD}" | chpasswd \
  && sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin yes/' /etc/ssh/sshd_config \
  && sed 's@session\s*required\s*pam_loginuid.so@session optional pam_loginuid.so@g' -i /etc/pam.d/sshd

ENV NOTVISIBLE "in users profile"
RUN echo "export VISIBLE=now" >> /etc/profile

EXPOSE 22
CMD ["/usr/sbin/sshd", "-D"]
