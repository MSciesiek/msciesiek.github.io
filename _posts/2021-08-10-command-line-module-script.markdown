---
layout: post
title: "Running a script from inside a module from a command line"
date: 2021-08-10 14:37:17 +0200
categories: python
---
Just for a quick look-up of how to run a script from inside a module in a python project:

```
cd project
source /venv/bin/activate
cd module
PROJECT_ENV_VAR=xyz PYTHONPATH=/path/to/project python script.py
```
Given that inside the script imports look like `from module import xyz` setting the PYTHONPATH like this should deal with errors like "ModuleNotFoundError: No module named 'module'".
