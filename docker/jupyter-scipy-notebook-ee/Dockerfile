FROM jupyter/scipy-notebook:5811dcb711ba
LABEL base-image="jupyter/scipy-notebook:5811dcb711ba 6/23/2018"

LABEL maintainer="Tyler Erickson <tylere@google.com>"

# ipyleaflet - Leaflet-based interactiving mapping widget
#     docs: https://ipyleaflet.readthedocs.io
#   source: https://github.com/jupyter-widgets/ipyleaflet
#     pkgs: conda search -c conda-forge ipyleaflet
ARG IPYLEAFLET_VERSION=0.9.0

# ipywidgets - Interactive Widgets for the Jupyter Notebook
#     docs: https://ipywidgets.readthedocs.io
#   source: https://github.com/jupyter-widgets/ipywidgets
#     pkgs: conda search -c conda-forge ipywidgets
#ARG IPYWIDGETS_VERSION=7.2.1

# Altair - Declarative visualization in Python
#     docs: https://altair-viz.github.io
#   source: https://github.com/altair-viz/altair
#     pkgs: conda search -c conda-forge altair
ARG ALTAIR_VERSION=2.1.0

# Vega Datasets - Collection of datasets used in Vega and Vega-Lite examples
#     docs: http://vega.github.io/vega-datasets
#   source: https://github.com/vega/vega-datasets
#     pkgs: source: https://github.com/vega/vega-datasets
ARG VEGA_DATASETS_VERSION=0.5.0

# bqplot - Grammar of Graphics-based interactive plotting framework for the Jupyter notebook
#     docs: https://bqplot.readthedocs.io
#   source: https://github.com/bloomberg/bqplot
#     pkgs: conda search -c conda-forge bqplot
ARG BQPLOT_VERSION=0.10.5

# nbdime - Notebook Diff & Merge tool
#     docs: https://nbdime.readthedocs.io
#   source: https://github.com/jupyter/nbdime
#     pkgs: conda search -c conda-forge nbdime
ARG NBDIME_VERSION=1.0.1

# Palettable - color maps
#     docs: https://jiffyclub.github.io/palettable
#   source: https://github.com/jiffyclub/palettable
#     pkgs: conda search -c conda-forge palettable
ARG PALETTABLE_VERSION=3.1.1

# PyDrive - Simplifies many Google Drive API tasks
#     home: https://pypi.org/project/PyDrive
#     docs: https://pythonhosted.org/PyDrive
#   source: https://github.com/gsuitedevs/PyDrive
#     pkgs: conda search -c conda-forge pydrive
ARG PYDRIVE_VERSION=1.3.1

# TensorFlow - Computation using data flow graphs for scalable machine learning
#     home: https://www.tensorflow.org
#     docs: https://www.tensorflow.org/api_docs
#   source: https://github.com/tensorflow/tensorflow
#     pkgs: conda search -c conda-forge tensorflow
ARG TENSORFLOW_VERSION=1.8.0

# Earth Engine Python API 
#     home: https://earthengine.google.com
#     docs: https://developers.google.com/earth-engine
#   source: https://github.com/google/earthengine-api
#     pkgs: conda search -c conda-forge earthengine-api
ARG EARTHENGINE_API_VERSION=0.1.143

# Google API Python Client 
#     home: http://google.github.io/google-api-python-client/
#     docs: https://developers.google.com/api-client-library/python/apis/
#   source: https://github.com/google/google-api-python-client/
#     pkgs: conda search -c conda-forge google-api-python-client
ARG GOOGLE_API_PYTHON_VERSION=1.6.7

#### Other packages
#
# jupyterlab-toc - Table of Contents extension for JupyterLab
#     source: https://github.com/ian-r-rose/jupyterlab-toc
#
# nbgitpuller - Notebook Git Puller
#   source: https://github.com/data-8/nbgitpuller
#
# Sidecar - A sidecar output widget for JupyterLab
#   source: https://github.com/jupyter-widgets/jupyterlab-sidecar
#
# ipythonblocks - colored grids
#    home: http://www.ipythonblocks.org/

RUN conda install --quiet --yes \
        ipyleaflet=${IPYLEAFLET_VERSION} \
        altair=${ALTAIR_VERSION} \
        vega_datasets=${VEGA_DATASETS_VERSION} \
        bqplot=${BQPLOT_VERSION} \
        nbdime=${NBDIME_VERSION} \
        palettable=${PALETTABLE_VERSION} \
        pydrive=${PYDRIVE_VERSION} \
        tensorflow=${TENSORFLOW_VERSION} \
        earthengine-api=${EARTHENGINE_API_VERSION} \
        google-api-python-client=${GOOGLE_API_PYTHON_VERSION} \
      && \
    conda clean -tipsy && \
    jupyter nbextension enable --py widgetsnbextension --sys-prefix && \
    # JupyterLab Extensions
    pip install sidecar && \
    jupyter labextension install --no-build jupyter-leaflet@0.9.0 && \
    jupyter labextension install --no-build @jupyter-widgets/jupyterlab-manager@0.35 && \
    jupyter labextension install --no-build bqplot && \
    jupyter labextension install --no-build jupyterlab-toc && \
    pip install git+https://github.com/data-8/nbgitpuller \
      && jupyter serverextension enable --py nbgitpuller --sys-prefix && \
    pip install ipythonblocks && \
    jupyter lab build && \
    npm cache clean --force && \
    rm -rf $CONDA_DIR/share/jupyter/lab/staging && \
    rm -rf /home/$NB_USER/.cache/yarn && \
    rm -rf /home/$NB_USER/.node-gyp && \
    fix-permissions $CONDA_DIR && \
    fix-permissions /home/$NB_USER
