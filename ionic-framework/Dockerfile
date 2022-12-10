FROM acodevs/android-node-cordova:2022.12.04

ENV IONIC_VERSION 6.20.4
ARG ionic_type=angular

RUN npm --without-ssl --insecure install -g --unsafe-perm @ionic/cli@${IONIC_VERSION} native-run cordova-res && \
    ionic --version && \
    cd /tmp

ENV HOME /tmp/.cache
ENV CYPRESS_CACHE_FOLDER /tmp/.cache

RUN mkdir /tmp/.cache && \
    mkdir /tmp/.cache/Cypress && \
    chmod -R 777 /tmp/.cache && \
    chmod -R 777 /tmp/.cache/Cypress

RUN ionic start myNewProject blank --type=${ionic_type} --capacitor && \
    cd myNewProject && \
    ionic build && \
    ionic capacitor build android --no-open

RUN rm -rf /var/lib/apt/lists/* && apt-get clean