FROM ubuntu:bionic

RUN apt-get -y update \
 && apt-get -y upgrade

RUN apt-get -y install apt-utils \
 && apt-get -y install libltdl7 \
 && apt-get -y install rsync \
 && apt-get -y install nano \
 && apt-get -y install joe \
 && apt-get -y install less\
 && apt-get -y install procps \
 && apt-get -y install telnet

RUN apt-get -y install bzip2 \
 && apt-get -y install p7zip

RUN apt-get -y install wget \
 && apt-get -y install libtool \
 && apt-get -y install iproute2 \
 && apt-get -y install net-tools \
 && apt-get -y install curl

RUN apt-get -y install openjdk-8-jdk
#RUN apt-get -y install openjdk-11-jdk

RUN apt-get -y install libreadline5
RUN apt-get -y install unzip

#install java11
##RUN wget  https://download.java.net/java/GA/jdk11/9/GPL/openjdk-11.0.2_linux-x64_bin.tar.gz -O /tmp/jdk.tar.gz
##RUN mkdir -p /usr/lib/jvm
##RUN tar xzvf /tmp/jdk.tar.gz --directory /usr/lib/jvm
##RUN rm -f /tmp/jdk.tar.gz

##RUN for bin in /usr/lib/jvm/jdk-11.0.2/bin/*; do update-alternatives --install /usr/bin/$(basename $bin) $(basename $bin) $bin 100; done
##RUN for bin in /usr/lib/jvm/jdk-11.0.2/bin/*; do update-alternatives --set $(basename $bin) $bin; done


#Download and install WCO2
RUN mkdir -p /wso2am/
COPY payload/wso2am-? /wso2am/
#COPY payload/wso2am-3.0.0.zip /wso2am/
RUN cat /wso2am/wso2am-? > /wso2am/wso2am.zip
RUN unzip /wso2am/wso2am.zip -d /wso2am/
RUN rm /wso2am/wso2am-?
RUN rm /wso2am/wso2am.zip

RUN mv /wso2am/wso2am-3.0.0/repository /wso2am/wso2am-3.0.0/repository.bak
RUN mkdir -p /wso2am/wso2am-3.0.0/repository

RUN echo alias ll='ls -l --color=auto' >> /etc/profile

RUN touch /.bash_history
RUN cp /root/.bash* / \
 && chown -R :0 /.bash* \
 && chmod -R g+rw /.bash* \
 && chmod -R o+r /.bash* \
 && echo PS1=\"\\[\\w\\]\\nuser@\\h:\\\\$ \" >> \.bashrc \
 && echo cd / >> /.bashrc

RUN chown -R :0 /wso2am/
RUN chmod -R g+rw /wso2am/

# && echo export no_proxy=$no_proxy,10.104.204.110 >> /.bashrc
# && echo export NO_PROXY=$no_proxy,10.104.204.110 >> /.bashrc

EXPOSE 9443
EXPOSE 8243
EXPOSE 8280

VOLUME /wso2am/wso2am-3.0.0/repository

ENV JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
##ENV JAVA_HOME=/usr/lib/jvm/jdk-11.0.2
WORKDIR /wso2am/wso2am-3.0.0/bin
ENTRYPOINT ["/wso2am/wso2am-3.0.0/bin/wso2server.sh", "--console"]
