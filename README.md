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


### 1. Начало работы

Почитали вводную часть 4 практики, скопировали код, скачали с Prometheus и Grafana с помощью 3-ёх букв, что нельзя называть :speak_no_evil:

### 2. Запуск приложения

В корне проекта выполните:
`go run ./cmd/server`
Откройте в браузере:
`http://localhost:8080/metrics`
<table cellpadding="10">
  <tr>
    <td><img width="974" height="514" alt="image" src="https://github.com/user-attachments/assets/053822a5-768e-434c-932e-6add1ab45a2b" /></td>
  </tr>
</table>

### 3. Проверка появления метрик

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

<tr>
    <td><img width="974" height="610" alt="image" src="https://github.com/user-attachments/assets/c2042a2a-3efd-42eb-b1d1-e674cd0d193e" /></td>
  </tr>
  
Затем снова откройте `/metrics` и найдите строки, начинающиеся с:
- app_http_requests_total
- app_http_errors_total
- app_http_request_duration_seconds

<img width="974" height="506" alt="image" src="https://github.com/user-attachments/assets/ebbd7a2e-3c85-4175-97e1-a1e9ce8bc86b" />

<img width="974" height="507" alt="image" src="https://github.com/user-attachments/assets/2f8f79d4-4bcd-4ebb-92f1-cdaae96ca5b1" />

### 4. Запуск Prometheus

<img width="974" height="432" alt="image" src="https://github.com/user-attachments/assets/5f8456e2-c7de-4f4a-b263-4ffc70ed206e" />

<img width="974" height="518" alt="image" src="https://github.com/user-attachments/assets/d7f7da42-e173-477b-a28e-1a7386f58130" />

### 5. Проверка целей сбора в Prometheus

<img width="974" height="519" alt="image" src="https://github.com/user-attachments/assets/d1746bd6-2534-46e9-a318-7ce7a27f257e" />

<img width="974" height="519" alt="image" src="https://github.com/user-attachments/assets/fddfad5e-90dd-48bc-b34d-960fa6ae3b9b" />

<img width="974" height="516" alt="image" src="https://github.com/user-attachments/assets/f867945e-2a8c-4c69-b91e-4bbce761f55b" />

### 6. Подключение Prometheus в Grafana

<img width="974" height="516" alt="image" src="https://github.com/user-attachments/assets/162c6d63-7aa2-4d09-863d-f9d3696d2cfb" />

Во время создания запросов произошли проблемы, при копировании запроса `sum(app_http_requests_total)` Grafana его вопринимал как `{"sum(app_http_requests_total)"}`, из-за чего ничего не работало. 

<img width="974" height="517" alt="image" src="https://github.com/user-attachments/assets/e5322db4-0206-4eb9-8365-95e2bb1b3ff0" />

После долгих разбирательств перешёл в `Code` и сам убрал фигурные скобки с ковычками и всё заработало. Итог, тупое копирование к хорошему не приводит :eyes:

<img width="974" height="515" alt="image" src="https://github.com/user-attachments/assets/724c1ff7-f220-4d3f-8b06-c466f39b24a4" />

<img width="974" height="518" alt="image" src="https://github.com/user-attachments/assets/bfdc1822-2fa9-4b99-a342-50883fa37385" />

### 7. Доп задание, Вариант 1 

Вариант 1. Добавить метрику по студентам
Добавьте счётчик:
`app_student_requests_total`
с лейблом `student_id`.

Добавим новый `CounterVec` в `metrics.go`

<img width="974" height="264" alt="image" src="https://github.com/user-attachments/assets/b63bf4fe-04c6-4faf-9d55-22ce0de54522" />

Добавим счетчик в функции `GetStudentByID` в `handler.go`

<img width="974" height="234" alt="image" src="https://github.com/user-attachments/assets/0f4f35fc-ef0c-48d3-a503-3ab3b81ae838" />

Делаем 3 новых запроса `curl http://localhost:8080/students/1`
И один запрос `curl http://localhost:8080/students/2`
И один запрос `curl http://localhost:8080/students/999`

Проверим метрики на `http://localhost:8080/metrics`

<img width="974" height="518" alt="image" src="https://github.com/user-attachments/assets/9fda5a34-41c3-423c-96b0-71ce2f9163ed" />

Проверяем в Prometheus 

<img width="974" height="516" alt="image" src="https://github.com/user-attachments/assets/d6d66c45-be84-4575-811f-d83c1742824e" />

Проверяем в Grafana

<img width="974" height="505" alt="image" src="https://github.com/user-attachments/assets/07e0ef6f-9230-4ec2-996b-cf69302584ad" />

