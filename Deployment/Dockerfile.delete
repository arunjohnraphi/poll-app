FROM python:3.11-slim

# Set the working directory
WORKDIR /app

# Set environment variables
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Copy only requirements first to leverage Docker layer caching
COPY ./mysite/requirements.txt ./

# Install required system libraries
RUN pip install --upgrade pip \
    && pip install -r requirements.txt

# Copy the application code
COPY mysite/ .

# Expose the application port
EXPOSE 8000

# Run the application
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
