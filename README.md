# Практическое  задание №1

Рассмотрим сценарий, в котором финансовое приложение обрабатывает данные фондового рынка в режиме реального времени. Подумайте, как и какой можно использовать брокер очередей сообщений, для эффективной обработки потоковых данных.
1. Опишите потенциальные преимущества и проблемы выбранного брокера.
2. Нарисуйте полную схему сервиса.
3. Дайте подробное описание каждому блоку который вы включили в систему, его назначение и цель.

# Потенциальные преимущества и проблемы Apache Kafka

## Преимущества:
Высокая пропускная способность: Kafka способен обрабатывать огромные объемы данных и обеспечивать высокую пропускную способность.

Устойчивость к сбоям: Распределенная архитектура Kafka обеспечивает отказоустойчивость и сохранность данных.

Гарантированная доставка сообщений: Kafka обеспечивает механизмы гарантированной доставки сообщений, что важно для финансовых данных.

Масштабируемость: Легко масштабируется горизонтально для поддержки роста нагрузки.



## Проблемы:
Сложность настройки: Настройка и поддержка Kafka может потребовать некоторых усилий, особенно при работе с распределенными системами.

Задержка: Несмотря на высокую производительность, существует некоторая задержка в обработке сообщений, что может быть критичным для финансовых данных.

Сложность в администрировании: Необходимость в заботе о темах, партициях и других аспектах может потребовать дополнительного времени и ресурсов.

```text
Финансовое приложение
    |
    |----> Apache Kafka (тема: financial_data)
           |
           |----> Обработчик данных
           |      |
           |      |----> Apache Kafka (тема: processed_data)
           |
           |----> Аналитический модуль
           |      |
           |      |----> Визуализация данных
           |
           |----> Уведомления
```

## Подробное описание каждого блока:

### Финансовое приложение:

Назначение: Получение данных фондового рынка в режиме реального времени.  
Цель: Отправка данных в Apache Kafka тему "financial_data" для асинхронной обработки.

### Apache Kafka (тема: financial_data):

Назначение: Центральная точка передачи сообщений, где поступающие данные о фондовом рынке размещаются в теме "financial_data".  
Цель: Обеспечение надежной и асинхронной передачи данных для обработки.

### Обработчик данных:

Назначение: Обработка данных из темы "financial_data", проведение вычислений и преобразований.  
Цель: Подготовка данных для хранения, анализа и дальнейшей обработки.

### Apache Kafka (тема: processed_data):

Назначение: Тема, куда помещаются обработанные данные.  
Цель: Обеспечение структурированного и гарантированного потока обработанных данных.

### Аналитический модуль:

Назначение: Выполнение сложных аналитических вычислений, моделирование и прогнозирование на основе обработанных данных.  
Цель: Предоставление дополнительной информации для принятия решений.

### Визуализация данных:

Назначение: Построение графиков и диаграмм для визуализации текущего и исторического состояния фондового рынка.  
Цель: Облегчение восприятия данных для конечных пользователей.

### Уведомления:

Назначение: Генерация уведомлений и оповещений на основе изменений в данных фондового рынка.  
Цель: Предоставление оперативной информации пользователям о важных событиях.

Эта схема использует Apache Kafka в качестве брокера сообщений для обеспечения эффективной и надежной передачи данных в финансовом приложении.
