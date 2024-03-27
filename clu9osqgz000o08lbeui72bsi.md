---
title: "Jupyter Installation"
datePublished: Wed Jun 29 2022 18:30:00 GMT+0000 (Coordinated Universal Time)
cuid: clu9osqgz000o08lbeui72bsi
slug: jupyter
tags: jupyter, jupyter-notebook

---

## Jupyter

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

## Jupyter hub

* [https://towardsdatascience.com/how-to-connect-to-jupyterlab-remotely-9180b57c45bb](https://towardsdatascience.com/how-to-connect-to-jupyterlab-remotely-9180b57c45bb)