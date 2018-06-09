[![License](https://img.shields.io/github/license/ysoffner/ionic-docker.svg)]()
[![Build Status](https://travis-ci.org/ysoffner/ionic-docker.svg?branch=master)](https://travis-ci.org/ysoffner/ionic-docker)
[![Version](https://images.microbadger.com/badges/version/ysoffner/ionic-docker.svg)](https://microbadger.com/images/ysoffner/ionic-docker)
[![Layers](https://images.microbadger.com/badges/image/ysoffner/ionic-docker.svg)](https://microbadger.com/images/ysoffner/ionic-docker)

# Simple image to run ionic framework

## Usage

```
docker run -ti --rm -p 8100:8100 -p 35729:35729 ysoffner/ionic-docker
```
If you have your own ionic sources, you can launch it with:

```
docker run -ti --rm -p 8100:8100 -p 35729:35729 -v /path/to/your/ionic-project/:/myApp:rw ysoffner/ionic-docker:tag_version
```

### Automation
With this alias:

```
alias ionic="docker run -ti --rm -p 8100:8100 -p 35729:35729 --privileged -v /dev/bus/usb:/dev/bus/usb -v ~/.gradle:/root/.gradle -v \$PWD:/myApp:rw ysoffner/ionic-docker:tag_version ionic"
```

> Due to a bug in ionic, if you want to use ionic serve, you have to use --net host option :

```
alias ionic="docker run -ti --rm --net host --privileged -v /dev/bus/usb:/dev/bus/usb -v ~/.gradle:/root/.gradle -v \$PWD:/myApp:rw ysoffner/ionic-docker:tag_version ionic"
```

> Know you need gradle for android, I suggest to mount ~/.gradle into /root/.gradle to avoid downloading the whole planet again and again

you can follow the [ionic tutorial](http://ionicframework.com/getting-started/) (except for the ios part...) without having to install ionic nor cordova nor nodejs on your computer.

```bash
ionic start myApp tabs
cd myApp
ionic serve
# If you didn't used --net host, be sure to chose the ip address, not localhost, or you would not be able to use it
```
open http://localhost:8100 and everything works.

### Android tests
You can test on your android device, just make sure that debugging is enabled.

```bash
cd myApp
ionic platform add android
ionic build android
ionic run android
```

## FAQ
* The application is not installed on my android device
  * Try `docker run -ti --rm -p 8100:8100 -p 35729:35729 --privileged -v /dev/bus/usb:/dev/bus/usb -v \$PWD:/myApp:rw ysoffner/ionic-docker adb devices` your device should appear
* The adb devices show nothing whereas I can see it when I do `adb devices` on my computer
  * You can't have adb inside and outside docker at the same time, be sure to `adb kill-server` on your computer before using this image

## Coming next
Support for android emulation with X11 forwarding

```bash
ionic platform emulate android
```
## Versions Latest
> https://www.npmjs.com/package/npm
> https://www.npmjs.com/package/node
> https://www.npmjs.com/package/ionic
> https://www.npmjs.com/package/cordova
> https://services.gradle.org/versions/current

based from [`agileek`](https://github.com/agileek)