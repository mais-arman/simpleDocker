# -------- Stage 1: Build --------

# Base image
FROM python:3.12-slim AS build

# Set working directory
WORKDIR /app

# Copy requirements and install dependencies
COPY requirements.txt ./
RUN pip install -r requirements.txt

# Copy application code
COPY . .

# -------- Stage 2: Runtime --------

FROM python:3.12-slim

WORKDIR /app

# Copy code and libraries from build stage
COPY --from=build /app /app

# Add a non-root user and switch to it
RUN useradd appuser
USER appuser

# Set environment variable
ENV GREETING="Hello from Python Container"

# Expose port
EXPOSE 5000

# Run the application
CMD ["python", "app.py"]

