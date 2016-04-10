# GEO optimized pyspark container

FROM jupyter/pyspark-notebook

USER root

RUN apt-get -y update && \
    apt-get install -y --no-install-recommends curl && \
        apt-get clean 

RUN curl -o /usr/local/lib/jts2geojson-0.7.0.jar http://central.maven.org/maven2/org/wololo/jts2geojson/0.7.0/jts2geojson-0.7.0.jar

RUN curl -o /usr/local/lib/jts-1.13.jar http://central.maven.org/maven2/com/vividsolutions/jts/1.13/jts-1.13.jar

# GEO libs
ENV LD_LIBRARY_PATH /usr/local/lib

