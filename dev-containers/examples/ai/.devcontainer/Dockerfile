FROM mcr.microsoft.com/devcontainers/python:3.13-bullseye

# Install pip for Python 3.13
RUN python -m pip install --upgrade pip

# Install packages
COPY requirements.txt .
RUN pip install -r requirements.txt

ENV ENVIRONMENT=container