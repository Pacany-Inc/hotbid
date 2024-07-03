# hotbid_front/Dockerfile
FROM node:16

# Устанавливаем зависимости
WORKDIR /app
COPY package*.json ./
RUN npm install

# Копируем код проекта
COPY . .

# Собираем проект
RUN npm run build

# Открываем порт
EXPOSE 8080

# Запускаем сервер
CMD ["npm", "run", "serve"]
