# busybox-glibc-rpi
Busybox container with glibc for raspeberry pi board (all in just 4,5MB).

>Note that this image is not production ready and the suggestion is to use it for develop and test purposes.

This image has been created using [Buildroot](https://buildroot.org/) tool. You can find the buildroot config file in the buildroot folder together with the configuration used for busybox.

This source repo is linked to automated build feature actived in Docker Hub so refert to [antvale/busybox-glibc-rpi] (https://hub.docker.com/r/antvale/busybox-glibc-rpi/) image name if you want to pull the latest tag from Docker Hub public reposiroty.
 
To test the image you can run this simple docker command line from raspberry board:
`docker run antvale/busybox-glibc-rpi ls -l /lib/`
that will automatically pull the latest image from official Docker Hub.



Versions of tools and libreries used to build the image:
* Ubuntu 16.04.1 LTS (Xenial Xerus)
* Buildroot (default cross-compiler, kerner headers 4.4.x):  buildroot-2016.05 
* Busybox 1.24.2
* Glibc 2.22 
