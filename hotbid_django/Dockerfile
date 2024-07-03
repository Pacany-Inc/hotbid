# hotbid_django/Dockerfile
FROM python:3.9-slim

# Устанавливаем зависимости
COPY ./requirements.txt /app/requirements.txt
WORKDIR /app
RUN pip install --no-cache-dir -r requirements.txt

# Копируем код проекта
COPY . /app

# Открываем порт
EXPOSE 8000

# Запускаем сервер
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]