debian-packages
===============
Custom DEB packages for the following codenames:
- **wheezy**: Debian 7
- **vivid**: Ubuntu 15.04

Installing the packages
-----------------------
Install signing key:
```
wget -O - http://debian-packages.cargomedia.ch/conf/signing.key | apt-key add -
```

Add to your `sources.list`:
```
deb http://debian-packages.cargomedia.ch <codename> main
```

Available packages
------------------

#### vivid

**arcconf**
 - Version: 2.00.21811-vivid1
 - Packages: arcconf

**graphene**
 - Version: 1.2.10-1
 - Packages: graphene

**gst-entrans**
 - Version: 1.0.3-1
 - Packages: gst-entrans

**gst-libav1.0**
 - Version: 1.6.1-1
 - Packages: gstreamer1.0-libav

**gst-plugins-bad1.0**
 - Version: 1.6.1-1ubuntu1
 - Packages: gir1.2-gst-plugins-bad-1.0, gstreamer1.0-plugins-bad-dbg, gstreamer1.0-plugins-bad-doc, gstreamer1.0-plugins-bad-faad, gstreamer1.0-plugins-bad-videoparsers, gstreamer1.0-plugins-bad, libgstreamer-plugins-bad1.0-0, libgstreamer-plugins-bad1.0-dev

**gst-plugins-base1.0**
 - Version: 1.6.1-1ubuntu1
 - Packages: gir1.2-gst-plugins-base-1.0, gstreamer1.0-alsa, gstreamer1.0-plugins-base-apps, gstreamer1.0-plugins-base-dbg, gstreamer1.0-plugins-base-doc, gstreamer1.0-plugins-base, gstreamer1.0-x, libgstreamer-plugins-base1.0-0, libgstreamer-plugins-base1.0-dev

**gst-plugins-good1.0**
 - Version: 1.6.1-1ubuntu1
 - Packages: gstreamer1.0-plugins-good-dbg, gstreamer1.0-plugins-good-doc, gstreamer1.0-plugins-good, gstreamer1.0-pulseaudio, libgstreamer-plugins-good1.0-0, libgstreamer-plugins-good1.0-dev

**gst-plugins-ugly1.0**
 - Version: 1.6.1-1ubuntu1
 - Packages: gstreamer1.0-plugins-ugly-amr, gstreamer1.0-plugins-ugly-dbg, gstreamer1.0-plugins-ugly-doc, gstreamer1.0-plugins-ugly

**gstreamer1.0**
 - Version: 1.6.1-1
 - Packages: gir1.2-gstreamer-1.0, gstreamer1.0-doc, gstreamer1.0-tools, libgstreamer1.0-0-dbg, libgstreamer1.0-0, libgstreamer1.0-dev

**hpacucli**
 - Version: 9.40.12.0-vivid1
 - Packages: hpacucli

**janus**
 - Version: 0.0.9-1
 - Packages: janus

**janus-gateway-audioroom**
 - Version: 0.0.2-1
 - Packages: janus-gateway-audioroom

**janus-gateway-rtpbroadcast**
 - Version: 0.0.2-ubuntu1
 - Packages: janus-gateway-rtpbroadcast

**libsrtp**
 - Version: 1.5.3
 - Packages: libsrtp

**libwebsockets**
 - Version: 1.5.0-ubuntu1
 - Packages: libwebsockets-dev, libwebsockets-test-server, libwebsockets3-dbg, libwebsockets3

**orc**
 - Version: 1:0.4.24-1
 - Packages: liborc-0.4-0-dbg, liborc-0.4-0, liborc-0.4-dev, liborc-0.4-doc

**sas2ircu**
 - Version: 20.00.00.00-vivid1
 - Packages: sas2ircu

**storcli**
 - Version: 1.17.08-vivid1
 - Packages: storcli

**usrsctp**
 - Version: 49335e1-git
 - Packages: usrsctp

#### wheezy

**arcconf**
 - Version: 2.00.21811-wheezy1
 - Packages: arcconf

**gearmand**
 - Version: 1.1.12-1
 - Packages: gearman-job-server, gearman-tools, gearman, libgearman-dbg, libgearman-dev, libgearman-doc, libgearman7-dbg, libgearman7

**hpacucli**
 - Version: 9.40.12.0-wheezy1
 - Packages: hpacucli

**janus**
 - Version: 0.0.9-wheezy1
 - Packages: janus

**janus-gateway-audioroom**
 - Version: 0.0.2-1
 - Packages: janus-gateway-audioroom

**janus-gateway-rtpbroadcast**
 - Version: 0.0.2-wheezy1
 - Packages: janus-gateway-rtpbroadcast

**libsrtp**
 - Version: 1.5.3-wheezy1
 - Packages: libsrtp

**libwebsockets**
 - Version: 1.5.0-wheezy1
 - Packages: libwebsockets-dev, libwebsockets-test-server, libwebsockets3-dbg, libwebsockets3

**mysql-proxy**
 - Version: 0.8.4-2
 - Packages: mysql-proxy

**sas2ircu**
 - Version: 20.00.00.00-wheezy1
 - Packages: sas2ircu

**storcli**
 - Version: 1.17.08-wheezy1
 - Packages: storcli

**usrsctp**
 - Version: 49335e1-git-wheezy1
 - Packages: usrsctp




Development
-----------
For signing the repo, the vagrant-provisioner will look for keys in `keys/{private,public}.key`.
Alternatively you might want to create new keys:

#### Creating a signing key
Create key:
```
gpg --gen-key
```

Export private and public key:
```
mkdir -p /vagrant/keys/
gpg --export -a 'Cargo Media' > /vagrant/keys/public.key
gpg --export-secret-key -a 'Cargo Media' > /vagrant/keys/private.key
```

#### Building a package
Start up the box and log in:
```
vagrant up <codename>
vagrant ssh <codename>
```

Build and test a package:
```
/vagrant/build.sh -c <codename> -p <package>
```

Bump version of a package:
```
cd /vagrant/packages/<codename>/<package>
dch -U
```

Build the repo and upload to S3:
```
sudo su
/vagrant/sync.sh
```
