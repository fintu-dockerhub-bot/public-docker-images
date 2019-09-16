FROM python:3.6-slim-buster

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential git \ 
    libsnappy-dev # for python-snappy \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Support German locale
RUN apt install -y locales
RUN echo "de_DE.utf-8 UTF-8" >> /etc/locale.gen
RUN locale-gen

# Set up non-root user
RUN mkdir -p /home/app \
    && groupadd -r app && useradd -r -g app -d /home/app app \
    && chown -R app:app /home/app
USER app
WORKDIR /home/app

# Set up Poetry et al.
ENV PATH=~/.local/bin:$PATH
RUN python3.6 -m pip install --no-cache-dir --user poetry mypy codecov tox

ENTRYPOINT ["/bin/bash"]