# Image Concepts

## Image Layer

![Image Kernel Architecture](/Users/ruan/workspace/hello-docker/figures/image-kernel.png)

- bootfs: the kernel on the host to be shared by all the containers
  - `uname -r` on the host and in the container: the same kernel info
- rootfs: each container's userspace filesystem, it includes /dev, /proc, /bin
  ![Multiple Containers upon the same kernel](/Users/ruan/workspace/hello-docker/figures/image-multi-containers.png) 
- image contains multiple layers which are mutable
- container layer: only the top layer is a writable layer corresponds to a container 
  ![Image Multiple Layer](/Users/ruan/workspace/hello-docker/figures/image-multiple-layers.png)