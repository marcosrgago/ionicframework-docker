# ionicframework-docker

## Commands to create a base with Android 11, Node 18 and Cordova CLI 11 (with android 11 project):
```
cd android-node-cordova && docker build . -t acodevs/android-node-cordova:2022.12.04
```

## Commands to create a project of ionic framework version 6.20.3 with capacitor and cordova:
### for '*Vue*'
```
cd ionicframework && docker build . --build-arg ionic_type=vue -t acodevs/ionicframework:2022.12.04-vue
```
### or for '*React*'
```
cd ionicframework && docker build . --build-arg ionic_type=react -t acodevs/ionicframework:2022.12.04-react
```
### or for '*Angular*'
```
cd ionicframework && docker build . --build-arg ionic_type=angular -t acodevs/ionicframework:2022.12.04-angular
```
