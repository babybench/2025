---
title: Installation
layout: default
nav_order: 2
---

# Installation
{: .no_toc }

To install BabyBench, head over to the [Github repository](https://github.com/babybench/babybench2025_starter_kit) and follow the instructions below. We provide two options for installation: a local installation and a Singularity container. Both options are equivalent and will install all the necessary dependencies to participate in the competition.

## Table of Contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Option 1: Local installation

The first option is to install BabyBench locally on your machine. This is the recommended option if you are new to Python or if you want to use BabyBench for your own research.

Pre-requisites: [Python](https://www.python.org/), [Git](https://git-scm.com/), and [Conda](https://www.anaconda.com/products/individual). All software has been tested on Ubuntu 18.04 and 24.04, MS Windows 10, and MacOS 11.

### Create a conda environment
{: .no_toc }

```
conda create --name babybench python=3.12
conda activate babybench
```

### Clone the BabyBench2025 repository
{: .no_toc }

```
git clone https://github.com/babybench/BabyBench2025_Starter_Kit.git
cd BabyBench2025_Starter_Kit
```

### Install requirements
{: .no_toc }

```
pip install -r requirements.txt
```

### Install MIMo
{: .no_toc }

```
pip install -e MIMo
```

All done! You are ready to start using BabyBench.

### Launch the installation test
{: .no_toc }

```
python test_installation.py
```

This will run a test to check that the everything is correctly installed. If the installation is successful, you should find a new folder called `test_installation` in the `results` directory with a rendered video of the test.  

## Option 2: Singularity container

Alternatively, you can use a Singularity container to install BabyBench. This allows you to use BabyBench without installing the software on your machine. It is also the recommended option if you are using a HPC cluster.

Pre-requisites: [Singularity](https://neuro.debian.net/install_pkg.html?p=singularity-container). All software has been tested on Ubuntu 24.04.

### Create the singularity container
{: .no_toc }

```
singularity build -F babybench.sif babybench.def
```

This will create a singularity container called `babybench.sif` in the current directory.

### Launch the installation test
{: .no_toc }

```
singularity run -c -H /home --bind "$PWD/:/home" babybench.sif
```

This will run a test to check that the everything is correctly installed. If the installation is successful, you should find a new folder called `test_installation` in the `results` directory with a rendered video of the test.

## Troubleshooting

If you encounter any issues during the installation, please refer to the [troubleshooting page](https://babybench.github.io/2025/troubleshooting)

---

### [Next page: Getting started](../start)
{: .no_toc }