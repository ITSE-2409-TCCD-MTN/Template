FROM mcr.microsoft.com/devcontainers/base:ubuntu

ENV PYTHONUNBUFFERED 1

RUN apt-get -y install --no-install-recommends postgresql postgresql-contrib \
    && apt-get clean -y && rm -rf /var/lib/apt/lists/*

RUN echo "alias cd='cd_workspace() { if [-z \"\$1\" ]; then builtin cd /workspaces/${localWorkspaceFolderBasename}; else builtin cd \"\$1\"; fi; }; cd_workspace'" >> /home/vscode/.bashrc

# [Optional] If your requirements rarely change, uncomment this section to add them to the image.
# COPY requirements.txt /tmp/pip-tmp/
# RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
#    && rm -rf /tmp/pip-tmp

# [Optional] Uncomment this section to install additional OS packages.
# RUN apt-get update && export DEBIAN_FRONTEND=noninteractive \
#     && apt-get -y install --no-install-recommends <your-package-list-here>
