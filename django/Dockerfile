# Use the official Ubuntu base image
FROM ubuntu:latest

# Set the non-interactive frontend for apt to avoid prompts
ENV DEBIAN_FRONTEND=noninteractive

# Update package lists and install required dependencies
RUN apt-get update && apt-get install -y \
    curl \
    software-properties-common \
    python3.10 \
    python3-pip \
    python3-venv \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Create a working directory
WORKDIR /app

# Copy requirements.txt and install dependencies
COPY requirements.txt .
RUN python3 -m venv venv && \
    . venv/bin/activate && \
    pip install --no-cache-dir -r requirements.txt

# Copy the Django project into the container
COPY myproject/ .

# Expose port 8000
EXPOSE 8000

# Command to run the Django development server
CMD ["/bin/bash", "-c", ". venv/bin/activate && python manage.py runserver 127.0.0.1:8000"]
