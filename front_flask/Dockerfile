# Dockerfile del FRONT — Flask + Jinja2 + Bootstrap (puerto 8059)
FROM python:3.12-slim
WORKDIR /app
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY . .
ENV PUERTO=8059
EXPOSE 8059
CMD ["python", "app.py"]
