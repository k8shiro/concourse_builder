FROM mzumi/centos7-ssh

ADD https://github.com/concourse/concourse/releases/download/v3.8.0/fly_linux_amd64 /usr/local/bin/fly

RUN chmod 775 /usr/local/bin/fly

RUN echo 'p@ssw0rd' | passwd root --stdin
