FROM python:3.10-slim

# Set an environment variable to prevent Python from buffering output
ENV PYTHONUNBUFFERED=1

# Install system dependencies needed for building mysqlclient
RUN apt-get update && \
    apt-get install -y \
    pkg-config \
    libmariadb-dev \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

# Set the working directory inside the container
WORKDIR /django

# Copy the requirements file first to leverage Docker caching
COPY requirements.txt requirements.txt

# Upgrade pip to the latest version
RUN pip install --upgrade pip

# Install dependencies from the requirements file
RUN pip install -r requirements.txt

# Copy the rest of the application files
COPY . .

# Expose port 8000 for the Django development server
EXPOSE 8000

# Command to run the Django development server
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
