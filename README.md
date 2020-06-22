# I) Churn_predict (предсказание пользователей склонных к оттоку)

Численные признаки - 190
Категориальные - 40

1) Обработка числовых признаков:
   1.1) Удаление пустых признаков
   1.2) Заполнение пропущенных значений средним/медианой
   1.3) Создание признаков пропущено ли значение в признаке: 1 - пропущено, 0 - не пропущено
   1.4) Масштабирование

2) Обработка категориальных признаков:
    2.1) Удаление пустых признаков
    2.2) Замена пропущенных значений на собственное уникальное значение 'fakenan'
    2.3) Отбор категориальных признаков с числом уникальных значений меньше 250 и one-hot кодирование
    2.4) Убираем дубликаты получившихся признаков

3) Отбор признаков:
    3.1) с помощью sklearn.feature_selection.SelectKBest
    3.2) с помощью модели с l1 регуляризацией

4) Балансировка классов:
   3.1) Задание словаря весов классов в class_weight модели логистической регрессии
   3.2) Undersampling  - удаление некоторого числа случайных объектов превосходящего класса

5) Модели:
    5.1) XGB
    5.2) Логистическая регрессия
    5.3) Нейронная сеть
    
# II) Predict_future_sales (Предсказание будущих продаж)

1) Осознание имеющихся данных 
   1.1) объем данных, колличество пропущенных значений
   1.2) численные и категориальные признаки, число уникальных значений признаков
   1.3) выбросы
   1.4) выводы по каждому файлу

2) Обработка выбросов
 
3) Создание признаков:
   2.1) создание мета категорий (город магазина, категория товара)
   2.2) создание временных признаков (год, месяц)
   2.3) создание признаков (месяц начала работы магазина, месяц окончания, длительность работы магазина в месяцах, новый товар или нет, новый ли в конкретном магазине ...)

4) Агрегирование данных и слияние данных из разных datafram-ов

5) Добавление данных о продажах в прошлом месяце

6) Модель - реккурентная нейронная сеть для задачи регрессии

# III) Идентификация пользователя по последовательности посещенных сайтов

Временные признаки + Категориальные

1) Создание новых прзнаков
   1.1) Колличество открытых вкладок
   1.2) Преобразование даных к  виду: [session_id] [site_id1....site_idn...site_id1_2....site_idn_k] и подсчитаем, сколько раз был открыт тот или иной сайт во время сессии
   1.3) Создадим признаки начала сессии (выходной или будний день, утро или вечер)

2) Модель - линейная регрессия (time-split кросс валидация т.к. данные отсортированы по времени)