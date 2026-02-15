# Stage 1: Builder
FROM python:3.11-slim as builder

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

# Install build dependencies (if your requirements need C extensions)
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    && rm -rf /var/lib/apt/lists/*

COPY ./mysite/requirements.txt .

# Install dependencies into a local directory
RUN pip install --upgrade pip \
    && pip install --user -r requirements.txt


# Stage 2: Runner
FROM python:3.11-slim as runner

WORKDIR /app

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1
# Ensure the local bin is in the path for the 'python' user
ENV PATH=/root/.local/bin:$PATH

# Copy only the installed packages from the builder stage
COPY --from=builder /root/.local /root/.local
# Copy the application code
COPY ./mysite/ .

EXPOSE 8000

# Use a production-ready server (optional but recommended)
# CMD ["gunicorn", "--bind", "0.0.0.0:8000", "mysite.wsgi:application"]
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]