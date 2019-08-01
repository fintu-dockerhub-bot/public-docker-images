FROM python:3.6-slim-buster

# Install system dependencies
RUN apt-get update && apt-get install -y \
    build-essential \ 
    libsnappy-dev # for python-snappy \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Set up non-root user
RUN mkdir -p /home/app \
    && groupadd -r app && useradd -r -g app -d /home/app app \
    && chown -R app:app /home/app
USER app
WORKDIR /home/app

# Set up Poetry et al.
RUN python3.6 -m pip install --no-cache-dir --user poetry mypy codecov tox
ENV PATH=~/.local/bin:$PATH
