#17-04 19:38
#************
#RUN apt-get update
#Installation de postfix
#RUN apt-get install postfix
#RUN sudo apt-get install ;
#**************************
#	POSTFIX
#	   &
#	DOVECOT
#**************************
#Image postfix, system: UBUNTU
FROM catatnight/postfix:latest
#PORT 25 souvent bloqué
#POSTFIX PORT: 587
EXPOSE 25 110 143 587 
#993
#**************************
#Création des utilisateurs*
#**************************
RUN groupadd vmail -g 5000
RUN useradd vmail -r -c 'virtual mail user' -m -d /home/vmail -g vmail -u 5000
#--------------------------
RUN echo mail.wt11.ephec-ti.be > /etc/mailname
RUN echo vmail: vmail@wt11.ephec-ti.be >> /etc/aliases
COPY postfix_conf/ /etc/postfix
RUN apt-get update && apt-get install dovecot-core dovecot-imapd -y
COPY /dovecot_conf /etc/dovecot
RUN touch /var/log/dovecot-deliver.log
RUN chmod o+rw /var/log/dovecot-deliver.log
RUN newaliases
RUN postmap /etc/postfix/virtual
RUN /etc/init.d/postfix restart
RUN dovecot
#hash le mot de passe
#RUN dovecotpw -p test -s SSHA256 

