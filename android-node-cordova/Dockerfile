FROM openjdk:11.0-slim AS openjdk11
FROM beevelop/android:v2022.06.1

RUN apt-get update --fix-missing && apt-get install -y curl gnupg2 lsb-release nodejs npm git bzip2 openssh-client

RUN curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | apt-key add - && \
    apt-key fingerprint 1655A0AB68576280 && \
    export VERSION=node_18.x && \
    export DISTRO="$(lsb_release -s -c)" && \
    echo "deb https://deb.nodesource.com/$VERSION $DISTRO main" | tee /etc/apt/sources.list.d/nodesource.list && \
    echo "deb-src https://deb.nodesource.com/$VERSION $DISTRO main" | tee -a /etc/apt/sources.list.d/nodesource.list && \
    node -v && npm -v && \
    npm install -g yarn && \
    yarn -v && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV CORDOVA_VERSION 11.0.0

ENV ANDROID_SDK_ROOT=/opt/android
ENV ANDROID_HOME=/opt/android
ENV PATH="${PATH}:${ANDROID_HOME}/tools"
ENV PATH="${PATH}:${ANDROID_HOME}/cmdline-tools"
ENV PATH="${PATH}:${ANDROID_HOME}/cmdline-tools/bin"
ENV PATH="${PATH}:${ANDROID_HOME}/build-tools/32.0.0"
ENV PATH="${PATH}:${ANDROID_HOME}/platform-tools"

WORKDIR "/tmp"

# RUN npm config set fetch-retries 100 && \
#    npm config set fetch-retry-mintimeout 100000 && \
#    npm config set fetch-retry-maxtimeout 600000 && \
#    npm set timeout=600000

RUN npm i -g cordova@${CORDOVA_VERSION} && \
    cordova -v && \
    cd /tmp && \
    cordova create myApp com.myCompany.myApp myApp

RUN cd myApp && \
    cordova plugin add cordova-plugin-camera --save && \
    cordova plugin add cordova-plugin-media --save && \
    cordova plugin add cordova-plugin-media-capture --save && \
    cordova plugin add cordova-plugin-splashscreen --save && \
    cordova plugin add cordova-plugin-statusbar --save && \
    cordova plugin add cordova-plugin-inappbrowser --save && \
    cordova plugin add cordova-plugin-geolocation --save && \
    cordova plugin add cordova-plugin-file --save && \
    cordova plugin add cordova-plugin-dialogs --save && \
    cordova plugin add cordova-plugin-network-information --save && \
    cordova plugin add cordova-plugin-nativestorage --save && \
    cordova plugin add cordova-sqlite-storage --save && \
    cordova platform add android@11.0.0 --save && \
    cordova requirements android

COPY --from=openjdk11 /usr/local/openjdk-11 /usr/lib/jvm/java-11

ENV JAVA_HOME=/usr/lib/jvm/java-11
ENV PATH="${PATH}:${JAVA_HOME}"

COPY gradle-7.4.2-all.zip /tmp/myApp/platforms/android/gradle/wrapper/opt/android/gradle-7.4.2-all.zip

ENV CORDOVA_ANDROID_GRADLE_DISTRIBUTION_URL=opt/android/gradle-7.4.2-all.zip

RUN cd myApp && \
    cordova build android --verbose

RUN rm -rf /var/lib/apt/lists/* && apt-get clean