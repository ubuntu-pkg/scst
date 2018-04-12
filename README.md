# Building scst Ubuntu package

Tested on Ubuntu 18.04. Prebuilt packages available on [releases](https://github.com/ubuntu-pkg/scst/releases) page.

* Create an empty working directory
 ```
rm -rf ~/scst-build
mkdir ~/scst-build
cd ~/scst-build
 ```

* Install dependencies
 ```
sudo apt install git devscripts equivs gdebi-core
git clone -b ubuntu-3.4.x https://github.com/ubuntu-pkg/scst.git
cd scst
sudo mk-build-deps -i -r
 ```

* Build
 ```
dpkg-buildpackage -b -uc -ui
 ```

# Installing scst Ubuntu package

* Install built package
 ```
sudo gdebi ../scst-dkms_*deb
sudo gdebi ../iscsi-scst_*.deb
sudo gdebi ../scstadmin_*deb
 ```
 
* Create `scst.conf`. You can use included sample to start
 ```
sudo cp /etc/scst.sample.conf /etc/scst.conf
 ```

* If you use sample conf, prepare zram block device
 ```
sudo modprobe zram
echo $((64*1024*1024)) | tee sudo /sys/block/zram0/disksize
 ```

* Restart scst service
 ```
sudo systemctl restart scst
sudo systemctl status scst
 ```

