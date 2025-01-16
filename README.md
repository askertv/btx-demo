# Развёртывание Битрикс в Docker

## Скачиваем архив Битрикса с официального сайта

https://www.1c-bitrix.ru/download/cms.php

Дистрибутивы для PHP

Стандарт zip


Технические требования
Продукт «1С-Битрикс: Управление сайтом» разработан на языке программирования PHP и может эффективно работать на любой UNIX или Windows-платформе.
Минимальные технические требования

PHP 8.1

Apache 2.0 и выше

MySQL 8.0 и выше 

## Распаковываем внутри данного проекта так, чтобы папки bitrix и upload были в корне

## Запускаем сборку docker-контейнеров
docker-compose up -d

## Разбираемся с некторыми возможными проблемами, которые решаются не сложно (адрес mysql, указание нужного пользователя и прочее)
