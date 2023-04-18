FROM mcr.microsoft.com/devcontainers/miniconda:0-3

# Create a temporary directory with the correct permissions and set the PIP_NO_CACHE_DIR environment variable
RUN mkdir -p /tmp/conda-tmp && chmod 755 /tmp/conda-tmp
ENV PIP_NO_CACHE_DIR=true

# Copy environment.yml (if found) to the temporary location so we update the environment. Also
# copy "noop.txt" so the COPY instruction does not fail if no environment.yml exists.
COPY environment.yml* .devcontainer/noop.txt /tmp/conda-tmp/
RUN if [ -f "/tmp/conda-tmp/environment.yml" ]; then umask 0002 && conda install -y -c conda-forge mamba && /opt/conda/bin/mamba env update -n base -f /tmp/conda-tmp/environment.yml; fi \
    && echo "OK"

# [Optional] Uncomment to install a different version of Python than the default
# RUN conda install -y python=3.6 \
#     && pip install --no-cache-dir pipx \
#     && pipx reinstall-all

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
