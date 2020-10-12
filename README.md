# Build & Install FFmpeg with libvmaf on Ubuntu 20.04
[FFmpeg](https://ffmpeg.org/ffmpeg.html) is the leading multimedia framework, able to decode, encode, transcode, mux, demux, stream, filter and play pretty much anything that humans and machines have created. [VMAF](https://github.com/Netflix/vmaf) is a perceptual video quality assessment algorithm developed by Netflix. VMAF Development Kit (VDK) is a software package that contains the VMAF algorithm implementation, as well as a set of tools that allows a user to train and test a custom VMAF model.
## Installation
1. Install [Meson](https://mesonbuild.com/index.html) and [Ninja](https://github.com/ninja-build/ninja) using following commands:
    
    `sudo apt-get install ninja-build meson`
    
2. Get latest VMAF SDK release from [here](https://github.com/Netflix/vmaf/releases).
3. Unzip VMAF SDK zip and install `libvmaf` with following commands:
    
    `cd vmaf-1.5.3/libvmaf`
    
    `meson build --buildtype release`
    
    `ninja -vC build`
    
    `ninja -vC build install`
4. Get latest FFmpeg soruce from [here](https://ffmpeg.org/download.html).
5. Build and install ffmpeg with libvamf using following commands:
    
    `./configure --enable-gpl --enable-libx264 --enable-libx265 --enable-nonfree --enable-libvmaf --enable-version3`
    
    `sudo make`
    
    `sudo make install`
    
    `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib`
6. To build ffmpeg with Nvidia-Cuda support use following command:
    `./configure --enable-gpl --enable-gnutls --enable-demuxer=dash --enable-libxml2 --enable-librsvg --enable-libaom --enable-libass --enable-libfdk-aac --enable-libmp3lame --enable-libfreetype --enable-libvorbis --enable-libopus --enable-libvpx --enable-libx264 --enable-libx265 --enable-nonfree --enable-libvmaf --enable-version3 --enable-cuda-nvcc --enable-cuvid --enable-nvenc --enable-nonfree --enable-libnpp --extra-cflags=-I/usr/local/cuda/include --extra-ldflags=-L/usr/local/cuda/lib64 --nvccflags='-gencode arch=compute_61,code=sm_61'`
