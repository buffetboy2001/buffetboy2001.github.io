# Jupyter Lab Installation Notes

Official Reference: https://plotly.com/python/getting-started/

Jupyter < 3 (3+ does not have full plotly support)
Make sure to install:
* `jupyter labextensions install @jupyter-widgets/jupyterlab-manager`
* `juptyer labextensions install jupterlab-plotly`

Do _not_ install other plotly extensions. At least one is deprecated & causes confusion when trying to resolve the problem.