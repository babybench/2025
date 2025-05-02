---
title: Troubleshooting
layout: default
nav_order: 98
---

# Troubleshooting
{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}


## Installation problems

### Conda installation failed

If you are unable to use Conda to install the required packages, you can try to create a virtual environment using Python's [builtin venv module](https://docs.python.org/3/library/venv.html). You can create a virtual environment with `python -m venv babybench` and activate it with `babybench\Scripts\activate`. You can then continue with the installation of the required packages as described in the [installation page](../installation).

python -m venv [name] and activate it with <venv-name>\Scripts\activate. Then, you can install all the required packages similar to Conda

### I can't install Singularity

If you are using a Windows/MAC/Ubuntu machine and have root privileges, we recommend installing Singularity using [NeuroDebian](https://neuro.debian.net/install_pkg.html?p=singularity-container). Otherwise, you can follow the [official installation guide](https://sylabs.io/guides/3.0/user-guide/installation.html). You can follow Singularity's [admin guide](https://docs.sylabs.io/guides/latest/admin-guide/installation.html) to install it without root provileges. 

## Errors

### X11: The DISPLAY environment variable is missing

This error can occur when trying to render in a headless machine or a remote server. You can still use BabyBench without rendering, e.g. by passing the --render=False flag when running the evaluation code. However, take into account that the visual modality will not be available without rendering.

---

### [Next page: FAQ](../faq)
{: .no_toc }