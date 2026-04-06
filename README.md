<h1 align="center"> Привет! Я <a target="_blank"> Кармеев Артур из группы ЭФМО-01-25 </a> 
<img src="https://github.com/blackcater/blackcater/raw/main/images/Hi.gif" height="32"/></h1>
<h3 align="center"> Данная практика выдалась немного затруднительной :confused: </h3>

Структура работы:

    └── pz4-monitoring/
        ├── go.mod
        ├── go.sum
        ├── monitoring/
        │   └── prometheus.yml
        ├── .idea/
        │   ├── .gitignore
        │   ├── modules.xml
        │   ├── pz4-monitoring.iml
        │   └── workspace.xml
        ├── internal/
        │   ├── student/
        │   │   ├── model.go
        │   │   └── repo.go
        │   ├── metrics/
        │   │   └── metrics.go
        │   └── httpapi/
        │       ├── handler.go
        │       ├── middleware.go
        │       └── response_writer.go
        └── cmd/
            └── server/
                └── main.go


## 1. Начало работы

Почитали вводную часть 4 практики, скопировали код, скачали с Prometheus и Grafana с помощью 3-ёх букв, что нельзя называть :speak_no_evil:

## 2. Запуск приложения

В корне проекта выполните:
`go run ./cmd/server`
Откройте в браузере:
`http://localhost:8080/metrics`
<table cellpadding="10">
  <tr>
    <td><img width="974" height="514" alt="image" src="https://github.com/user-attachments/assets/053822a5-768e-434c-932e-6add1ab45a2b" /></td>
  </tr>
</table>

## 3. Проверка появления метрик

Сделайте несколько запросов:

<table cellpadding="10">
  <tr>
    <td><img width="974" height="612" alt="image" src="https://github.com/user-attachments/assets/f23074cb-aaa7-4b17-9caf-952666099864" /></td>
  </tr>
</table>

<table cellpadding="10">
  <tr>
    <td><img width="974" height="632" alt="image" src="https://github.com/user-attachments/assets/705df876-818f-487c-8f26-165f80092cbe" /></td>
  </tr>
</table>

<table cellpadding="10">
  <tr>
    <td><img width="974" height="622" alt="image" src="https://github.com/user-attachments/assets/30209866-9a8d-4299-8427-aa4e8dd4e18b" /></td>
  </tr>
</table>

<table cellpadding="10">
  <tr>
    <td><img width="974" height="610" alt="image" src="https://github.com/user-attachments/assets/c2042a2a-3efd-42eb-b1d1-e674cd0d193e" /></td>
  </tr>
</table>
  
Затем снова откройте `/metrics` и найдите строки, начинающиеся с:
- app_http_requests_total
- app_http_errors_total
- app_http_request_duration_seconds

<table cellpadding="10">
  <tr>
    <td><img width="974" height="506" alt="image" src="https://github.com/user-attachments/assets/ebbd7a2e-3c85-4175-97e1-a1e9ce8bc86b" /></td>
  </tr>
</table>

<table cellpadding="10">
  <tr>
    <td><img width="974" height="507" alt="image" src="https://github.com/user-attachments/assets/2f8f79d4-4bcd-4ebb-92f1-cdaae96ca5b1" /></td>
  </tr>
</table>

## 4. Запуск Prometheus

<table cellpadding="10">
  <tr>
    <td><img width="974" height="432" alt="image" src="https://github.com/user-attachments/assets/5f8456e2-c7de-4f4a-b263-4ffc70ed206e" /></td>
  </tr>
</table>

<table cellpadding="10">
  <tr>
    <td><img width="974" height="518" alt="image" src="https://github.com/user-attachments/assets/d7f7da42-e173-477b-a28e-1a7386f58130" /></td>
  </tr>
</table>

## 5. Проверка целей сбора в Prometheus

<table cellpadding="10">
  <tr>
    <td><img width="974" height="519" alt="image" src="https://github.com/user-attachments/assets/d1746bd6-2534-46e9-a318-7ce7a27f257e" /></td>
  </tr>
</table>

<table cellpadding="10">
  <tr>
    <td><img width="974" height="519" alt="image" src="https://github.com/user-attachments/assets/fddfad5e-90dd-48bc-b34d-960fa6ae3b9b" /></td>
  </tr>
</table>

<table cellpadding="10">
  <tr>
    <td><img width="974" height="516" alt="image" src="https://github.com/user-attachments/assets/f867945e-2a8c-4c69-b91e-4bbce761f55b" /></td>
  </tr>
</table>

## 6. Подключение Prometheus в Grafana

<table cellpadding="10">
  <tr>
    <td><img width="974" height="516" alt="image" src="https://github.com/user-attachments/assets/162c6d63-7aa2-4d09-863d-f9d3696d2cfb" /></td>
  </tr>
</table>

Во время создания запросов произошли проблемы, при копировании запроса `sum(app_http_requests_total)` Grafana его вопринимал как `{"sum(app_http_requests_total)"}`, из-за чего ничего не работало. 

<table cellpadding="10">
  <tr>
    <td><img width="974" height="517" alt="image" src="https://github.com/user-attachments/assets/e5322db4-0206-4eb9-8365-95e2bb1b3ff0" /></td>
  </tr>
</table>

После долгих разбирательств перешёл в `Code` и сам убрал фигурные скобки с ковычками и всё заработало. Итог, тупое копирование к хорошему не приводит :eyes:

<table cellpadding="10">
  <tr>
    <td><img width="974" height="515" alt="image" src="https://github.com/user-attachments/assets/724c1ff7-f220-4d3f-8b06-c466f39b24a4" /></td>
  </tr>
</table>

<table cellpadding="10">
  <tr>
    <td><img width="974" height="518" alt="image" src="https://github.com/user-attachments/assets/bfdc1822-2fa9-4b99-a342-50883fa37385" /></td>
  </tr>
</table>

## 7. Доп задание, Вариант 1 

Вариант 1. Добавить метрику по студентам
Добавьте счётчик:
`app_student_requests_total`
с лейблом `student_id`.

Добавим новый `CounterVec` в `metrics.go`

<table cellpadding="10">
  <tr>
    <td><img width="974" height="264" alt="image" src="https://github.com/user-attachments/assets/b63bf4fe-04c6-4faf-9d55-22ce0de54522" /></td>
  </tr>
</table>

Добавим счетчик в функции `GetStudentByID` в `handler.go`

<table cellpadding="10">
  <tr>
    <td><img width="974" height="234" alt="image" src="https://github.com/user-attachments/assets/0f4f35fc-ef0c-48d3-a503-3ab3b81ae838" /></td>
  </tr>
</table>

Делаем 3 новых запроса `curl http://localhost:8080/students/1`
И один запрос `curl http://localhost:8080/students/2`
И один запрос `curl http://localhost:8080/students/999`

Проверим метрики на `http://localhost:8080/metrics`

<table cellpadding="10">
  <tr>
    <td><img width="974" height="518" alt="image" src="https://github.com/user-attachments/assets/9fda5a34-41c3-423c-96b0-71ce2f9163ed" /></td>
  </tr>
</table>

Проверяем в Prometheus 

<table cellpadding="10">
  <tr>
    <td><img width="974" height="516" alt="image" src="https://github.com/user-attachments/assets/d6d66c45-be84-4575-811f-d83c1742824e" /></td>
  </tr>
</table>

Проверяем в Grafana

<table cellpadding="10">
  <tr>
    <td><img width="974" height="505" alt="image" src="https://github.com/user-attachments/assets/07e0ef6f-9230-4ec2-996b-cf69302584ad" /></td>
  </tr>
</table>

## 8. Контрольные вопросы :secret:

1. Что такое метрики приложения?
Метрики — это числовые показатели, описывающие состояние приложения и его поведение во времени (например, количество запросов, число ошибок, длительность обработки, нагрузка на процессор).

2. Чем метрики отличаются от логов?
Логи отвечают на вопрос «что именно произошло?» (конкретное событие), а метрики — на вопрос «как система ведёт себя в целом?» (тренды, доли ошибок, динамика нагрузки).

3. Какую роль выполняет Prometheus?
Prometheus — это система мониторинга, которая получает метрики от приложений через регулярный опрос (scraping) HTTP-эндпоинта, сохраняет их как временные ряды и позволяет анализировать с помощью запросов PromQL.

4. Что такое scraping в Prometheus?
Scraping — это процесс, при котором Prometheus периодически опрашивает HTTP-эндпоинты (обычно `/metrics`) целевых приложений, чтобы собрать и сохранить актуальные метрики.

5. Зачем приложению маршрут /metrics?
Маршрут `/metrics` нужен, чтобы приложение публиковало свои метрики в формате, понятном Prometheus. Prometheus обращается к этому эндпоинту для сбора данных.

6. Что делает promhttp.Handler()?
`promhttp.Handler()` создаёт HTTP-обработчик, который экспортирует метрики Prometheus через HTTP, используя стандартный реестр метрик (DefaultGatherer). В коде его вешают на `/metrics`.

7. Для чего нужна Grafana?
Grafana — это инструмент визуализации, который подключается к Prometheus как к источнику данных и строит панели, графики и дашборды для наглядного анализа метрик.

8. Какие три основные метрики реализованы в этой работе?

- `app_http_requests_total` (счётчик общего числа HTTP-запросов);
- `app_http_errors_total` (счётчик ошибочных запросов);
- `app_http_request_duration_seconds` (гистограмма длительности обработки запросов).

9. Что показывает Histogram?
Гистограмма (Histogram) показывает распределение значений измеряемой величины (например, времени обработки запросов) по заданным интервалам («корзинам»). Позволяет оценить процентили и средние значения.

10. Почему мониторинг важен для сопровождения backend-приложений?
Мониторинг позволяет видеть систему в динамике: вовремя заметить рост ошибок, замедление ответов, увеличение нагрузки на отдельные маршруты, а не разбирать каждый инцидент по логам. Это помогает оперативно реагировать на проблемы.
