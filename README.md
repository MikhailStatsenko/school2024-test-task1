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
Стаценко Михаил Александрович

## Описание реализации
Для выполнения поставленной задачи разработано консольное Spring Boot приложение.  

Первым аргументом командной строки передается путь к файлу с исходными данными. `ReportService` в методе `generateReport` при помощи вспомогательных методов читает json файл по указанному пути, затем считает сумму, потраченную пользователями для каждого месяца, после чего находит месяц(-ы) с максимальной суммой и возвращает строку в формате json в соответствии с заданием.  

Поскольку речь идет об анализе заказов на маркетплейсе, отчет, вероятно, будет создаваться на основании миллионов заказов, поэтому для подсчета суммы, потраченной пользователями по месяцам используется параллельная обработка, а файл с исходными данными читается при помощи `BufferedReader`.

## Инструкция по сборке и запуску решения
На тестовом стенде должны быть установлены Maven и Java 21+ версии

Сначала необходимо клонировать репозиторий на локальную машину:  
`git clone https://github.com/MikhailStatsenko/school2024-test-task1.git`

Затем нужно перейти в склонированную директорию и последовательно выполнить команды:  
`mvn clean package`  
`java -jar target/analytics-1.0.jar [путь к файлу с исходными данными]`