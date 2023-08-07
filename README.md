# NodeJS-Dev-Test
Mechanism for asynchronous processing of HTTP requests

# Установка и настройка
1. Склонируйте репозиторий проекта: https://github.com/souljee/NodeJS-Dev-Test.git
2. Установите зависимости для каждого микросервиса:  
`npm i express winston amqplib axios`
3. Убедитесь, что у вас установлен и запущен RabbitMQ сервер. Если нет, установите RabbitMQ согласно инструкциям на официальном сайте: https://www.rabbitmq.com/
4. Настройте параметры RabbitMQ в файлах **app.js** и **worker.js**:
    1. В файле **app.js**:

       ~~~~****____
       const queueName = 'task_queue';
       const replyQueueName = 'reply_queue';
       const rabbitmqUrl = 'amqp://localhost';

    2. В файле **worker.js**:
      ~~~~****____
       const queueName = 'task_queue';
       const rabbitmqUrl = 'amqp://localhost';
5. Запустите **index.js**, в терминале будут выводиться сообщения от обеих микросервисов. Или же вы можете по отдельности запускать микросервисы в терминалах.
    1. В первом терминале:
       ~~~~****____
       cd test
       node app.js
   2. Во втором терминале:
       ~~~~****____
      cd test
      node worker.js

6. Отправьте тестовые POST-запросы для проверки работоспособности приложения. Это можно сделать с помощью **Postman** или другого инструмента для отправки HTTP-запросов. Пример отправки запросов с помощью Node.js скрипта представлен в файле **sender.js**.
# Как работает приложение
1. Микросервис М1 (app.js) представляет собой HTTP-сервер, который принимает POST-запросы на порт 3000 и отправляет их в очередь RabbitMQ с помощью библиотеки amqplib.

2. Микросервис М2 (worker.js) слушает очередь RabbitMQ, получает сообщения, обрабатывает их и отправляет результаты обратно в очередь М1.

3. Микросервис М1 принимает ответы от М2 и отправляет их обратно клиенту в качестве ответа на исходный POST-запрос.

# Автор

Автор проекта: **Санжар Ибадуллаев**

Если у вас возникли вопросы или проблемы, пожалуйста свяжитесь со мной по адресу ssoulljee@gmail.com