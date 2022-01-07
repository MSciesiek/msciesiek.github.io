---
layout: post
title: "raspberry pi and airflow"
date: 2021-09-09 14:37:17 +0200
categories: python
---
I wanted to experiment a bit with airflow in home setting. I came up with an idea to install it on a raspberry pi and periodically call a esp8266 board hosting a webserver showing temperature.

1. Set up the termometer:
For this I followed the tutorial from: XXX
I had a different board so I checked the pinout to make sure things were wired correctly

2. Install airflow on raspberry

```
mkdir airflow
cd airflow
sudo apt-get install python3 python3-dev gcc
python3 -m venv venv
source venv/bin/activate
pip install -U pip
pip install wheel
pip install apache-airflow
```

3. Put a script in ~/airflow/dags/

4. Init airflow and create admin user
```
airflow db init
FLASK_APP=airflow.www.app flask fab create-admin
```

5. unpause the dag
```
airflow dags unpause temperature
```

6. start scheduler in screen
```
screen
source venv/bin/activate
airflow scheduler
```
to deatach do ctrl+A and then d


