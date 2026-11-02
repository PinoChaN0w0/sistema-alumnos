# Jenkins + las herramientas que necesita el pipeline de esta actividad.
# Base oficial de Jenkins (Debian) con Python, Doxygen y Graphviz añadidos.
FROM jenkins/jenkins:lts-jdk21

USER root

# Herramientas del sistema: Python 3, Doxygen (+ Graphviz para los diagramas), curl
RUN apt-get update \
 && apt-get install -y --no-install-recommends \
        python3 python3-venv python3-pip \
        doxygen graphviz curl \
 && rm -rf /var/lib/apt/lists/*

# Herramientas de Python en un entorno aislado (/opt/herramientas) para no tocar el Python del sistema
RUN python3 -m venv /opt/herramientas \
 && /opt/herramientas/bin/pip install --no-cache-dir \
        pipenv pip-audit bandit flake8 pytest

ENV PATH="/opt/herramientas/bin:${PATH}"

USER jenkins

# Plugins que usa el Jenkinsfile (el asistente inicial instalará además los sugeridos)
RUN jenkins-plugin-cli --plugins workflow-aggregator git junit credentials-binding timestamper
