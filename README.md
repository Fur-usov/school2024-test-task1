# Тестовое задание для отбора на Летнюю ИТ-школу КРОК по разработке

## Условие задания
Один развивающийся и перспективный маркетплейс активно растет в настоящее время. Текущая команда разработки вовсю занята тем, что развивает ядро системы. Помимо этого, перед CTO маркетплейса стоит задача — разработать подсистему аналитики, которая на основе накопленных данных формировала бы разнообразные отчеты и статистику.

Вы — компания подрядчик, с которой маркетплейс заключил рамочный договор на выполнение работ по разработке этой подсистемы. В рамках первого этапа вы условились провести работы по прототипированию и определению целевого технологического стека и общих подходов к разработке.

На одном из совещаний с Заказчиком вы определили задачу, на которой будете выполнять работы по прототипированию. В качестве такой задачи была выбрана разработка отчета о периодах наибольших трат со стороны пользователей.

Аналитики со стороны маркетплейса предоставили небольшой срез массива данных (файл format.json) о покупках пользователей, на примере которого вы смогли бы ознакомиться с форматом входных данных. Каждая запись данного среза содержит следующую информацию:
- Идентификатор пользователя;
- Дата и время оформления заказа;
- Статус заказа;
- Сумма заказа.

В пояснительной записке к массиву данных была уточняющая информация относительно статусов заказов:
- COMPLETED (Завершенный заказ);
- CANCELED (Отмененный заказ);
- CREATED (Созданный заказ, еще не оплаченный);
- DELIVERY (Созданный и оплаченный заказ, который доставляется).

Необходимо разработать отчет, вычисляющий по полученному массиву данных месяц, когда пользователи тратили больше всего. Если максимальная сумма пользовательских трат была в более, чем одном месяце, отчет должен показывать все такие месяцы. В отчете должны учитываться только завершенные заказы.

Требования к реализации:
1. Реализация должна содержать, как минимум, одну процедуру (функцию/метод), отвечающую за формирование отчета, и должна быть описана в readme.md в соответствии с чек-листом;
2. В качестве входных данных программа использует json-файл (input.json), соответствующий структуре, описанной в условиях задания;
3. Процедура (функция/метод) формирования отчета должна возвращать строку в формате json следующего формата:
   - {«months»: [«march»]} 
   - {«months»: [«march», «december»]}
4. Найденный в соответствии с условием задачи месяц должен выводиться на английском языке в нижнем регистре. Если месяцев несколько, то на вывод они все подаются на английском языке в нижнем регистре в порядке их следования в течение года.

## Автор решения
Урусов Фёдор Сергеевич

## Описание реализации
В моем решении есть 2 функции:  

* **get_data()**  
Создание словаря, содержащего сумарные траты по месяцам.  

Создаем пустой словарь months_total. Проходимся по входным данным (JSON, то есть список из словарей в Python), и в каждом словаре проверяем, равно ли поле 'status' строке "COMPLETED". 

Если да, то выделяем время заказа из поля 'ordered_at', форматируем в вид "год-месяц-день время", далее выделяем только месяц и сохраняем его название в переменную month.

Если ячейка словаря существует, то просто прибавляем к ней значение из поля 'total', если не существует, инициализируем со значением 0 и делаем то же самое. (при помощи функции get) 

В конце функция возвращает созданный словарь.   

- **create_report()**  
Cоздания отчета в формате JSON.

Выбираем максимальное значение среди всех значений входного словаря, то есть среди всех месячных сумм.

Далее при помощи генератора словаря создаем словарь, где ключ - строка 'months', а значение - список из тех месяцев, чья сумма равна максимальной (используем генератор списка) 

Возвращаем результат.

### Основная часть (main)
1) Сначала открывается файл format.json при помощи контекстного менеджера и данные записываются в переменную data
2) При помощи функции get_data на основе переменной data формируется словарь и записывается в переменную m_total
3) На основе m_total формируется отчет при помощи функции create_report и выводится в стандартный вывод



## Инструкция по сборке и запуску решения
1) проверьте, что у вас установлен Python 3.11. Для этого в консоли введите python --version. Если появилась ошибка, скачайте Python с официального сайта: https://www.python.org/
2) скачайте решение командой `git clone https://github.com/Fur-usov/school2024-test-task1` или через GitHub Desktop. 
3) Откройте папку с проектом в любой IDE или в консоли. 
4) Убедитесь, что в папке присутствуют файлы main.py и format.json
5) Введите `python main.py` в консоли или нажмите кнопку пуск в IDE
6) После успешного выполнения программы в консоли появится отчет о максимальных тратах
6) Если возникнут ошибки, попробуйте установить библоитеку json вручную командой `pip install json`
