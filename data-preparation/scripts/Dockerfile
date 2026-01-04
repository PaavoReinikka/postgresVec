# python:3.10-slim has security issues, so python:3.13-slim preferred
FROM reinikp2/python-3.13-slim-uv:latest

# Install required system packages (libpq-dev for psycopg2, vim for Q&D edits)
# and gnumeric for Excel file handling in scripts
RUN apt-get update && apt-get install -y \
    curl \
    gnumeric \
    libpq-dev \
    vim \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Install Python dependencies using pip on build, or use uv (see note below)
RUN pip install --no-cache-dir \
    numpy \
    psycopg-binary

# Set the working directory
WORKDIR /scripts

# Copy the scripts into the container
COPY . /scripts

#NOTE: since uv is enabled in the base image, you can also use
# uv to install dependencies from pyproject.toml (assuming it's present in /scripts)
# RUN uv sync

# Default command (can be overridden in docker-compose)
CMD ["bash"]
