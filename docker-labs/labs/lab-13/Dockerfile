# Use Python base image
FROM python:3.10

# Set production environment variables (third method)
ENV APP_MODE=production \
    APP_REGION="canada west"

# Set working directory
WORKDIR /app

# Copy application code
COPY Docker-3/  /app

# Install flask
RUN pip install flask

# Expose port
EXPOSE 9099

# Run the app
CMD ["python", "app.py"]

