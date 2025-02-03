# Use the official lightweight Python image
FROM python:3.11-slim

# Set the working directory
WORKDIR /app

# Create a non-root user and group
RUN groupadd -g 1001 appgroup && useradd -m -u 1001 -g appgroup appuser

# Copy dependency file and install dependencies first for better caching
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application
COPY . .

# Ensure correct ownership and permissions
RUN chown -R appuser:appgroup /app && chmod -R 755 /app

# Explicitly create and set permissions for the token file
RUN touch /app/current_token.txt && chown appuser:appgroup /app/current_token.txt && chmod 666 /app/current_token.txt

# Switch to non-root user
USER appuser

# Expose port
EXPOSE 8080

# Start the application
CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8080"]
