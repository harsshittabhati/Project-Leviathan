# Start from Python slim base
FROM python:3.12-slim

# Set a non-root user (required by Kyverno)
RUN useradd -u 1000 -m appuser

# Set working directory
WORKDIR /app

# Copy app code (will come from ConfigMap in Kubernetes, but we need requirements for image)
COPY canary-app/requirements.txt requirements.txt

# Install dependencies
RUN pip install --no-cache-dir -r requirements.txt

# Switch to non-root user
USER appuser

# Expose port
EXPOSE 8080

# Run Flask app (actual app.py will be mounted from ConfigMap)
CMD ["flask", "run", "--host=0.0.0.0", "--port=8080"]
