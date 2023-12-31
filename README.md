# Отток клиентов

Из «Бета-Банка» стали уходить клиенты. Каждый месяц. Немного, но заметно. Банковские маркетологи посчитали: сохранять текущих клиентов дешевле, чем привлекать новых.

Нужно спрогнозировать, уйдёт клиент из банка в ближайшее время или нет. Вам предоставлены исторические данные о поведении клиентов и расторжении договоров с банком.

## Описание данных

Данные находятся в файле `./churn.csv`

Признаки:

- `RowNumber` — индекс строки в данных
- `CustomerId` — уникальный идентификатор клиента
- `Surname` — фамилия
- `CreditScore` — кредитный рейтинг
- `Geography` — страна проживания
- `Gender`— пол
- `Age` — возраст
- `Tenure` — сколько лет человек является клиентом банка
- `Balance` — баланс на счёте
- `NumOfProducts` — количество продуктов банка, используемых клиентом
- `HasCrCard` — наличие кредитной карты
- `IsActiveMember` — активность клиента
- `EstimatedSalary` — предполагаемая зарплата

Целевой признак:

- `Exited` — факт ухода клиента

## Используемые модели

Построим модель с предельно большим значением *F1*-меры, не менее 0.59. Затем проверим *F1*-меру на тестовой выборке.

Измерим *AUC-ROC* и сравним её значение с *F1*-мерой.

Для обучения модели выбран популярный алгоритм случайный лес.
Для подбора гиперпараметров и реализации кросс-валидации использован GridSearchCV.

Во время работы над задачей был обнаружен дисбаланс классов.
Метрика F1 на несбалансированных данных почти `0.556`, что ниже целевого `0.59`.

Наилучший результат (на имеющихся данных) мы получили при взвешивании классов. После финального обучения `F1 == 0.613` на кросс-валидации.

На тестовой выборке значение  `F1 == 0.64`.

Значение AUC-ROC: 0.88
