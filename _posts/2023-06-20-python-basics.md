---
title: Python Basic Setup Concepts
author: gcalvoCR
date: 2023-06-20 12:00:00 -0600
categories: [concepts, python]
tags: [python, basics] # tag names should always be lowercase
---

# Python Basics

## Installation

There are many options to install Python, there are different options out there.

[DOCS](https://www.python.org/downloads/)
[Homebrew](https://docs.brew.sh/Homebrew-and-Python)


## Virtual Environments

A virtual environment in Python is a self-contained space or container that allows you to have separate and isolated Python environments on a single machine.

When you work on different projects or use different libraries in Python, it's possible that those projects or libraries may have conflicting dependencies or versions. A virtual environment helps solve this problem by creating a separate environment for each project, with its own set of dependencies and Python packages.

Type the following commands to create a new virtual environment, activate it and install the dependencies:

```sh
# Create virtual environment
python3 -m venv venv
# Activate it
source venv/bin/activate
# Install dependencies
pip install -r requirements.txt
```

## Dependencies

They are usually stored in a `requirements.txt` file.

In order to create it from the dependencies you have installed, type:
```sh
pip freeze > requirements.txt
```

In order to install them:
```sh
pip install -r requirements.txt
```



