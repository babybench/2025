---
title: Installation
layout: default
nav_order: 2
---

# Installation

{: .no_toc }

## Table of Contents
{: .no_toc .text-delta }

- TOC
  {:toc}

## Option 1: Local installation

Pre-requisites: [Python](https://www.python.org/), [Git](https://git-scm.com/), and [Conda](https://www.anaconda.com/products/individual). All software has been tested on Ubuntu 18.04 and 24.04.

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
cd BabyBench
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

This will run a test to check that the everything is correctly installed.

## Option 2: Singularity container

Pre-requisites: [Singularity](https://docs.sylabs.io/guides/latest/user-guide/). All software has been tested on Ubuntu 18.04 and 24.04.

### Create a singularity container
{: .no_toc }

```
singularity build --fakeroot --sandbox babybench.sif docker://babybench/babybench:latest
```

This will create a singularity container called `babybench.sif` in the current directory.

### Launch the installation test
{: .no_toc }

```
singularity exec --bind /home/lopez/Code/babybench.github.io/babybench2025:/babybench2025 babybench.sif python test_installation.py
```

This will run a test to check that the everything is correctly installed.

## Troubleshooting


If you encounter any issues, visit the [troubleshooting page](https://babybench.github.io/babybench2025/wiki/troubleshooting)
