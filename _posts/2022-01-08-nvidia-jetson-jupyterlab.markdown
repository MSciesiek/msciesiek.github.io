---
layout: post
title: "jupyter lab server"
date: 2022-01-08 20:53:00 +0200
categories: python
---

How to install jupyter lab on a jetson nano or raspberry pi:

```
sudo apt-get update
sudo apt install -y python3-pip python3-dev libffi-dev
sudo python3 -m pip install setuptools cffi
python3 -m pip install jupyterlab
```

To actually run it:

```
jupyter-lab --ip 0.0.0.0 --port 8888 --no-browser
```

To run it as a service:

1. check jupyter-lab executable location to put it in the .service file in the next step

   ```
   which jupyter-lab
   ```

2. create .service file:

   ```
   sudo nano /etc/systemd/system/jupyter.service
   ```

3. paste into the file:

   ```
   [Unit]
   Description=Jupyter Lab
   [Service]
   Type=simple
   PIDFile=/run/jupyter.pid
   ExecStart=/bin/bash -c "/home/maciej/.local/bin/jupyter-lab --ip="0.0.0.0" --no-browser --notebook-dir=/home/maciej/notebooks"
   User=maciej
   Group=maciej
   WorkingDirectory=/home/maciej/notebooks
   Restart=always
   RestartSec=10
   [Install]
   WantedBy=multi-user.target
   ```

4. enable the service
   ```
   sudo systemctl enable jupyter.service
   sudo systemctl daemon-reload
   sudo systemctl start jupyter.service
   sudo systemctl status jupyter.service
   ```

Useful links:

<https://medium.com/analytics-vidhya/jupyter-lab-on-raspberry-pi-22876591b227>
