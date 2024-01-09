# Linux-Docker
Задача:
1) создать сервис, состоящий из 2 различных контейнеров: 1 - веб, 2 - БД (compose)

Решение:

version: '3.1'
services:
  el-mysql:
    # Используемый Docker образ
    image: mysql:8.0.31
    # Переменные окружения для MySQL
    environment:
      MYSQL_ROOT_PASSWORD: el-pass1
    # Монтируем том для сохранения данных MySQL
    volumes:
      - mysql_data:/var/lib/mysql

  el-php:
    # Используемый Docker образ
    image: phpmyadmin/phpmyadmin
    ports:
      - 8081:80
    depends_on:
      - el-mysql
    # Переменные окружения для phpMyAdmin
    environment:
      PMA_HOST: el-mysql
volumes:
  mysql_data:
