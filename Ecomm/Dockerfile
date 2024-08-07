# Stage 1: Build Stage
FROM python:3.10-slim AS builder

# Set the working directory in the container
WORKDIR /app

# Install build dependencies
RUN apt-get update && \
    apt-get install -y \
    postgresql-client \
    libpq-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Copy the requirements file into the container
COPY requirements.txt /app/

# Install Python dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application code into the container
COPY . /app/

# Stage 2: Runtime Stage
FROM python:3.10-slim

# Set the working directory in the container
WORKDIR /app

# Copy only the necessary files from the build stage
COPY --from=builder /app /app

# Copy the .env file into the container
COPY .env /app/

# Expose the port the app runs on
EXPOSE 8000

# Define environment variable
ENV DJANGO_SETTINGS_MODULE=Ecomm.settings

# Run Django server when the container starts
ENTRYPOINT ["python"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]
