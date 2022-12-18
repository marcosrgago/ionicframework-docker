FROM acodevs/android-node-cordova:2022.12.04

ENV IONIC_VERSION 6.20.5

RUN npm --without-ssl --insecure install -g --unsafe-perm @ionic/cli@${IONIC_VERSION} native-run cordova-res && \
    ionic --version && \
    cd /tmp

ENV HOME /tmp/.cache
ENV CYPRESS_CACHE_FOLDER /tmp/.cache

RUN mkdir /tmp/.cache && \
    mkdir /tmp/.cache/Cypress && \
    chmod -R 777 /tmp/.cache && \
    chmod -R 777 /tmp/.cache/Cypress

RUN ionic start myNewProjectVue blank --type=vue --capacitor --no-git && \
    cd myNewProjectVue && \
    ionic build && \
    ionic capacitor build android --no-open

RUN ionic start myNewProjectAngular blank --type=angular --capacitor --no-git && \
    cd myNewProjectAngular && \
    ionic build && \
    ionic capacitor build android --no-open

RUN ionic start myNewProjectReact blank --type=react --capacitor --no-git && \
    cd myNewProjectReact && \
    ionic build && \
    ionic capacitor build android --no-open

RUN rm -rf /var/lib/apt/lists/* && apt-get clean