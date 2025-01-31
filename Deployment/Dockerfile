FROM python:3.11-slim-buster

WORKDIR /app

COPY ./mysite/requirements.txt ./

# Use an explicit pip version for better control
RUN apt-get update
RUN pip install -r requirements.txt

COPY mysite/ .

# Expose the port the app runs on
EXPOSE 8000

# Run the application
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
