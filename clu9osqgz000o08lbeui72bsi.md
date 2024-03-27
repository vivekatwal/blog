---
title: "Jupyter"
datePublished: Wed Jun 29 2022 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: clu9osqgz000o08lbeui72bsi
slug: jupyter
tags: jupyter, jupyter-notebook

---

Jupyter notebook make life easier for

* **Begineer** to learn and understand step by step
    
* **Experts** to explore data,visualiations.
    
* **Mentors** to create course
    
* **Speakers** for demonstration
    

## How to enable virtualenv on jupyter notebook

Installation

```plaintext
sudo apt install jupyter-core
```

Activate the env and the install `ipykernel`

```plaintext
pip install ipykernel
```

Inorder to differentiate different environemnt, you have to name them, Name them with along with packgae version

```plaintext
ipython kernel install --user --name=envname_pkg_v1
```

To view all the environment

```plaintext
jupyter kernelspec list
```

Remove environment from jupyter

```plaintext
jupyter kernelspec uninstall envname
```

## Themes

```plaintext
pip install jupyterthemes
```

## How to install extension

```plaintext
pip install jupyter_contrib_nbextensions
jupyter contrib nbextension install
```

* [plotly extension](https://community.plotly.com/t/jupyterlab-extension-install-for-plotly-4-9-0-fails/44520/4)
    

## Jupyter hub

* [https://towardsdatascience.com/how-to-connect-to-jupyterlab-remotely-9180b57c45bb](https://towardsdatascience.com/how-to-connect-to-jupyterlab-remotely-9180b57c45bb)