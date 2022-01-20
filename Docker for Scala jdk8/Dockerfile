# create new
FROM ubuntu
LABEL MarcosGois <marcosvagois@outlook.com>

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install sudo
RUN sudo apt-get install apt-transport-https curl gnupg -yqq
RUN echo "deb https://repo.scala-sbt.org/scalasbt/debian all main" | sudo tee /etc/apt/sources.list.d/sbt.list
RUN echo "deb https://repo.scala-sbt.org/scalasbt/debian /" | sudo tee /etc/apt/sources.list.d/sbt_old.list
RUN curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | sudo -H gpg --no-default-keyring --keyring gnupg-ring:/etc/apt/trusted.gpg.d/scalasbt-release.gpg --import
RUN sudo chmod 644 /etc/apt/trusted.gpg.d/scalasbt-release.gpg
RUN sudo apt-get update
RUN sudo apt-get install sbt -y
RUN sudo apt-get install build-essential curl file git nano vim -y
RUN sudo apt-get install unzip zip -y
# To install SDKMAN
RUN curl -s "https://get.sdkman.io?rcupdate=false" | bash

#RUN /bin/bash -c "source $HOME/.sdkman/bin/sdkman-init.sh"
#RUN ["/bin/sh" "-c" "source $HOME/.sdkman/bin/sdkman-init.sh"]
# RUN . $HOME/.sdkman/bin/sdkman-init.sh
# RUN ["/bin/bash", "-c", "source $HOME/.sdkman/bin/sdkman-init.sh"]
# To install JAVA and SBT
RUN /bin/bash -c 'source $HOME/.sdkman/bin/sdkman-init.sh &&\
    sdk install java 8.0.302-open &&\
    sdk install sbt'
# To install JAVA and SBT
# RUN sdk install java 8.0.302-open
# RUN sdk install sbt

RUN mkdir /home/Oberon 
WORKDIR /home/Oberon
RUN chmod -R 0777 /home/Oberon
# Clonning the repository
RUN git clone https://github.com/UnBCIC-TP2/Oberon-Scala.git .
# docker push marcosgois/scalajdk8:tagname

EXPOSE 80

CMD bash