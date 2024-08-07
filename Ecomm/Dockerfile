# Use the official Ubuntu base image
FROM ubuntu:22.04

# Set the working directory in the container
WORKDIR /app

# Install necessary packages and clean up
RUN apt-get update && \
    apt-get install -y python3 python3-pip python3-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Copy the requirements file into the container
COPY requirements.txt /app/
COPY .env /app/
COPY . /app/
EXPOSE 8000

# Define environment variable
ENV DJANGO_SETTINGS_MODULE=Ecomm.settings

# Run Django server when the container starts
ENTRYPOINT ["python3"]
CMD ["manage.py", "runserver", "0.0.0.0:8000"]
