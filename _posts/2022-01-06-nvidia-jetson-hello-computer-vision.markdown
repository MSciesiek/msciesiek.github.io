---
layout: post
title: "nvidia jetson hello world"
date: 2022-01-06 22:53:00 +0200
categories: python
---

I got nvidia jetson nano 2gb for Xmax this year. This is a quick overview of the setup and testing of a Raspberry pi camera v2 that I attached using CSI interface.

1. Etch an image on a SD card. 
    I was using Balena Etcher and installed a dedicated image from the nvidia website: <https://developer.nvidia.com/jetson-nano-2gb-sd-card-image> . The image includes 'JetPack', a set of preinstalled libraries.

2. Setup:
    it's a bit easier in the graphical mode. When doing that in the headless mode via USB and setting internet connection over wifi: if you have any special characters in your wifi password, you have to remember to escape them in the console with `\`.

3. Not really needed right away, but eventually:

    ```
    sudo apt get update
    sudo apt get install python3-pip
    ```

    ---
    **NOTE**

    `python3 -m pip list` does not show opencv (which is included in JetPack), but
    `python3`, `import cv2` works...
    What's important, the version of opencv included in JetPack supports GStreamer. The version installed via `pip` does not. You can check if GStreamer is supported by
    ```
    import cv2
    print(cv2.getBuildInformation())
    ```
    It's in the `Video I/O` section.

    ---

4. Clone official jetson repository with a few demos:

    ```
    git clone https://github.com/JetsonHacksNano/CSI-Camera.git
    ```

5. Run demo with a CSI camera

    ```
    cd CSI-Camera
    python3 simple_camera.py
    ```

    A new window should appear with the image from camera. When using opencv installed via pip there is an error (`Unable to open camera`) due to GStreamer not being enabled (as described in step 3).

6. Access resource usage statistics
   installing `jtop` - like `htop` but much more useful during development on Jetson:

    ```
    sudo -H python3 -m pip install -U jetson-stats
    sudo reboot
    jtop
    ```


Some useful links:
- <https://github.com/jetsonHacksNano/CSI-Camera>
- <https://galaktyk.medium.com/how-to-build-opencv-with-gstreamer-b11668fa09c>
- <https://medium.com/axinc-ai/install-jetpack-and-tensorflow-on-jetson-176ddc0a5a3c>
- <https://docs.nvidia.com/jetson/jetpack/install-jetpack/index.html#how-to-install-jetpack>
- <https://qengineering.eu/install-opencv-4.5-on-jetson-nano.html>
