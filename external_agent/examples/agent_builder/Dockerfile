FROM python:3.11-slim

WORKDIR /app
RUN useradd -m appuser

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .
RUN chown -R appuser:appuser /app
RUN touch /app/current_token.txt && chmod 666 /app/current_token.txt
USER appuser
EXPOSE 8080

CMD ["uvicorn", "app:app", "--host", "0.0.0.0", "--port", "8080"]
