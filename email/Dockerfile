#Dockerfile para SMTP e IMAP
FROM debian:latest

WORKDIR /app

RUN apt-get update \
    && apt-get install -y \
    postfix \
    dovecot-core \
    dovecot-imapd \
    iputils-ping \
    net-tools \
    telnet \
    nano

RUN apt-get upgrade -y

COPY ./imap/10-auth.conf /etc/dovecot/conf.d/10-auth.conf
COPY ./imap/10-mail.conf /etc/dovecot/conf.d/10-mail.conf
COPY ./imap/10-master.conf /etc/dovecot/conf.d/10-master.conf
COPY ./imap/dovecot.conf /etc/dovecot/dovecot.conf

COPY ./smtp/mailname /etc
COPY ./smtp/main.cf /etc/postfix/main.cf
COPY ./smtp/master.cf /etc/postifix

COPY email_00.sh .
#RUN chmod +x email_00.sh
#RUN /app/email_00.sh

COPY users.sh .
#RUN chmod +x users.sh
#RUN /app/users.sh

EXPOSE 25 110 143 993 995

CMD tail -F /dev/null