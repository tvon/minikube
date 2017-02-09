builder_image = minikube-iso-builder
makefile_path := $(dir $(abspath $(lastword $(MAKEFILE_LIST))))
minikube_dir = $(makefile_path)/../..
container_minikube_dir = /usr/local/src

minikube_iso: image
	docker run --rm -it -v $(minikube_dir):/usr/local/src $(builder_image) make minikube_iso

image:
	docker build -t $(builder_image) .

clean:
	$(builder_image) make clean

menuconfig:
	docker run --rm -it \
		-v $(minikube_dir):/usr/local/src \
		$(builder_image) \
		make \
		BR2_EXTERNAL=$(container_minikube_dir)/deploy/iso/minikube-iso \
		-C out/buildroot \
		menuconfig

savedefconfig:
	docker run --rm -it \
		-v $(minikube_dir):/usr/local/src \
		$(builder_image) \
		make \
		BR2_EXTERNAL=$(container_minikube_dir)/deploy/iso/minikube-iso \
		-C out/buildroot \
		savedefconfig

linux-menuconfig:
	docker run --rm -it \
		-v $(minikube_dir):/usr/local/src \
		$(builder_image) \
		make \
		BR2_EXTERNAL=$(container_minikube_dir)/deploy/iso/minikube-iso \
		-C out/buildroot \
		linux-menuconfig
	docker run --rm -it \
		-v $(minikube_dir):/usr/local/src \
		$(builder_image) \
		make \
		BR2_EXTERNAL=$(container_minikube_dir)/deploy/iso/minikube-iso \
		-C out/buildroot

linux-update-defconfig:
	docker run --rm -it \
		-v $(minikube_dir):/usr/local/src \
		$(builder_image)\
		make \
		BR2_EXTERNAL=$(container_minikube_dir)/deploy/iso/minikube-iso \
		-C out/buildroot \
		linux-update-defconfig

linux-savedefconfig:
	docker run --rm -it
	-v $(minikube_dir):/usr/local/src \
		$(builder_image) \
		make \
		BR2_EXTERNAL=$(container_minikube_dir)/deploy/iso/minikube-iso \
		-C out/buildroot \
		linux-savedefconfig
	cp $(minikube_dir)/out/buildroot/output/build/linux-4.7.2/defconfig \
		$(minikube_dir)/deploy/iso/minikube-iso/board/coreos/minikube/linux-4.7_defconfig

smoketest:
	minikube start --iso-url file:///$(minikube_dir)/out/minikube.iso
	minikube ssh

shell:
	docker run --rm -it -v $(minikube_dir):/usr/local/src $(builder_image) /bin/bash
