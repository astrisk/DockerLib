FROM jenkinsci/slave:2.62
MAINTAINER Qiusheng Zhang <zhangqiusheng@dongqiudi.com>

ENV ANDROID_HOME /usr/lib/android-sdk-linux

USER root

RUN dpkg --add-architecture i386 && apt-get update && apt-get install -y libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1 && apt-get clean

USER jenkins

RUN mkdir /home/android-sdk
VOLUME /home/android-sdk

RUN mkdir /home/jenkins/.jenkins
VOLUME /home/jenkins/.jenkins

RUN mkdir /home/jenkins/.gradle
ENV GRADLE_USER_HOME /home/jenkins/.gradle
VOLUME /home/jenkins/.gradle

WORKDIR /home/jenkins

COPY jenkins-slave /usr/local/bin/jenkins-slave

ENTRYPOINT ["jenkins-slave"]