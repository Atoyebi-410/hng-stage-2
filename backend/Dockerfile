# Use an official Python runtime as a parent image
FROM python:3.10-slim

# install bash to run the script
# RUN sudo apt-get install bash

# Set the working directory to /app
WORKDIR /app

# Install system dependencies and Poetry
RUN apt-get update && apt-get install -y \
    curl \
    gcc \
    libpq-dev \
    python3-dev \
    && curl -sSL https://install.python-poetry.org | python3 - \
    && apt-get clean

# Add Poetry to PATH
ENV PATH="/root/.local/bin:$PATH"

# Copy pyproject.toml and poetry.lock to leverage Docker cache
COPY pyproject.toml poetry.lock* ./

# Install Python dependencies using Poetry
RUN poetry install --no-root --no-dev

# Copy the rest of the application code to the working directory
COPY . .

# Expose port 8000 for FastAPI
EXPOSE 8000

# Command to run the FastAPI server
CMD ["poetry", "run", "uvicorn", "app.main:app", "--host", "0.0.0.0", "--port", "8000"]

