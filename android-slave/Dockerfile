FROM jenkinsci/slave:2.62-alpine
MAINTAINER Qiusheng Zhang <zhangqiusheng@dongqiudi.com>

ENV ANDROID_HOME /usr/lib/android-sdk-linux

USER root

# 设置时区
RUN apk --no-cache add tzdata  && \
    ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime && \
    echo "Asia/Shanghai" > /etc/timezone

# 安装 android 环境
RUN cd /usr/lib/ && \
    set -x && \
    wget http://dl.google.com/android/android-sdk_r24.0.1-linux.tgz && \
    tar xvzf android-sdk_r24.0.1-linux.tgz && \
    echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter android-23 && \
    echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter platform-tools && \
    echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter build-tools-23.0.2 && \
    echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter extra-android-m2repository && \
    echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter extra-google-google_play_services && \
    echo y | android-sdk-linux/tools/android --silent update sdk --no-ui --all --filter extra-google-m2repository && \
    rm android-sdk_r24.0.1-linux.tgz && \
    apk update

USER jenkins
RUN mkdir /home/jenkins/.jenkins
VOLUME /home/jenkins/.jenkins
RUN mkdir /home/jenkins/.gradle

ENV GRADLE_USER_HOME /home/jenkins/.gradle
VOLUME /home/jenkins/.gradle

WORKDIR /home/jenkins

COPY jenkins-slave /usr/local/bin/jenkins-slave

ENTRYPOINT ["jenkins-slave"]
