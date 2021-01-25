To build docker:
'''
	make
'''

To run docker(user is your local user):
'''
	docker run -it --privileged -v /home/user/rk-rootfs-build:/home/amarula/rk-rootfs-build rk-rootfs-build
'''

Once into docker launch:
'''
	sudo dpkg -i ubuntu-build-service/packages/*
	sudo apt-get install -f
	RELEASE=buster TARGET=desktop ARCH=armhf ./mk-base-debian.sh
	RELEASE=buster ARCH=armhf ./mk-rootfs.sh
	./mk-image.sh
'''

You now find target image here:
'''
/home/user/rk-rootfs-build/linaro-rootfs.img
'''
