# GEO optimized pyspark container

FROM jupyter/pyspark-notebook

USER root

# Here are some informations how-to change the 'conda' environment
# https://hub.docker.com/r/pdonorio/py3dataconda/~/dockerfile

# Force bash always 
RUN rm /bin/sh && ln -s /bin/bash /bin/sh

# Setup python 2.7 as default environment
ENV CONDA_ENV_PATH /opt/conda/envs/python2
ENV CONDA_DEFAULT_ENV python2
ENV CONDA_DIR /opt/conda
ENV CONDA_ACTIVATE "source $CONDA_ENV_PATH/bin/activate python2"
ENV PATH $CONDA_ENV_PATH/bin:$PATH

RUN apt-get -y update && \
    apt-get install -y --no-install-recommends --force-yes curl && \
    apt-get install -y --no-install-recommends --force-yes git-core && \
    apt-get install -y --no-install-recommends --force-yes build-essential && \
    apt-get install -y --no-install-recommends --force-yes cpio && \
    apt-get install -y --no-install-recommends --force-yes python-pip && \
    apt-get install -y --no-install-recommends --force-yes libpython-dev && \
    apt-get install -y --no-install-recommends --force-yes libgeos-dev && \
    apt-get install -y --no-install-recommends --force-yes libproj-dev && \
    apt-get install -y --no-install-recommends --force-yes libgdal-dev && \
	apt-get install -y --no-install-recommends --force-yes libspatialite-dev && \
    apt-get clean

# Install / upgrade python libs
RUN $CONDA_ACTIVATE && pip install overpy --upgrade
RUN $CONDA_ACTIVATE && pip install retrying --upgrade
RUN $CONDA_ACTIVATE && pip install geopandas --upgrade
# add folim and related python libs for geovisualization
RUN $CONDA_ACTIVATE && pip install vincent --upgrade
RUN $CONDA_ACTIVATE && pip install branca --upgrade
RUN $CONDA_ACTIVATE && pip install folium --upgrade

# Install conda packages
RUN conda install libgfortran -y
RUN conda install fiona -y
RUN conda install gdal -y


# Separate 'pip' for updating correct kernal version 
#RUN curl -O https://bootstrap.pypa.io/get-pip.py
#RUN python2.7 get-pip.py

RUN curl -k -o /usr/local/lib/spatial-spark_2.10-1.1.1-beta-SNAPSHOT.jar https://dl.dropboxusercontent.com/u/96303065/spark-workshop/spatial-spark_2.10-1.1.1-beta-SNAPSHOT.jar
RUN curl -o /usr/local/lib/jts-1.13.jar http://central.maven.org/maven2/com/vividsolutions/jts/1.13/jts-1.13.jar

# GEO libs
ENV SPARK_CLASSPATH="/usr/local/lib/jts-1.13.jar:/usr/local/lib/spatial-spark_2.10-1.1.1-beta-SNAPSHOT.jar"
