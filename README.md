# Практическое задание №3
1. Напишите определение паттерна “таймаут и повтор” и для чего он нужен
2. Перерисуйте схему внедрив в нее RabbitMQ. (Схема системы будет в чате Telegram)
3. Опишите какие сервисы на схеме стоит связывать через очереди, а какие нет. И почему
4. Опишите тип exchange, который стоит использовать
5. Опишите возможности дальнейшей масштабируемости, благодаря внедрению брокера
6. Напишите есть ли в RabbitMq возможность реализовать Топологию очередей “Репликация”? Как она может быть реализована?


# Определение паттерна "таймаут и повтор":
   Паттерн "таймаут и повтор" (Retry Pattern) представляет собой стратегию обработки ошибок в распределенных системах. При возникновении ошибки при выполнении операции система ожидает некоторый промежуток времени (таймаут) и затем повторяет операцию. Этот процесс может повторяться несколько раз, прежде чем будет принято решение о сбое операции.

# Схема с RabbitMQ:
   К сожалению, я не могу визуализировать схему, предоставленную вами в формате XML. Однако, я готов ответить на вопросы и предоставить советы на основе предоставленного описания.

# Связывание сервисов через очереди:
   На схеме следует связывать сервисы, которые имеют асинхронные взаимодействия и могут работать независимо друг от друга через очереди. Например, сервисы доставки, статистики и предсказания ML могут быть асинхронно связаны через RabbitMQ, чтобы снизить взаимосвязанность и улучшить отказоустойчивость. Сервисы, которые имеют синхронное взаимодействие и требуют мгновенного ответа, могут быть связаны напрямую без использования очередей. Например, клиент может взаимодействовать напрямую с сервисами Nginx, заказов и монолитного сервиса.

# Тип Exchange для RabbitMQ:
   В зависимости от требований можно использовать различные типы Exchange в RabbitMQ.  
   Например:  
   Direct Exchange: Используется, когда необходима прямая маршрутизация сообщений между определенными очередями и обменником.  
   Fanout Exchange: Рассылает сообщения всем подключенным очередям. Полезен, если необходимо доставить сообщение каждой подписанной очереди.  
   Topic Exchange: Позволяет маршрутизировать сообщения на основе шаблонов маршрутов, что обеспечивает более гибкую маршрутизацию.  

# Возможности масштабируемости с брокером:
   Внедрение брокера сообщений, такого как RabbitMQ, обеспечивает гибкость и масштабируемость системы. Возможности масштабирования включают:  
   Горизонтальное масштабирование: Добавление новых узлов брокера для увеличения пропускной способности и обработки сообщений.  
   Разделение обязанностей: Каждый сервис может обрабатывать только те сообщения, которые ему необходимы, улучшая производительность и отказоустойчивость.  
# Репликация очередей в RabbitMQ:
   В RabbitMQ есть возможность репликации очередей для обеспечения отказоустойчивости. Это можно достичь с использованием Mirrored Queues, где сообщения копируются на несколько узлов брокера. Это обеспечивает сохранность сообщений в случае сбоя одного из узлов. Также, стоит отметить, что RabbitMQ предоставляет другие механизмы для обеспечения отказоустойчивости, такие как кластеризация и политики зеркальности для обменников.
