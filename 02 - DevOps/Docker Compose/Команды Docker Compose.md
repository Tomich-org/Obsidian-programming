Docker Compose предлагает множество команд для управления многоконтейнерными приложениями. Вот наиболее значимые команды, их ключевые опции и примеры использования:
### **1. `docker-compose up`**
Запускает все сервисы, определенные в файле `docker-compose.yml`.
- **Флаги:**    
    - `-d`: Запускает сервисы в фоновом режиме (detached mode).
    - `--build`: Пересобирает образы перед запуском.
    - `--force-recreate`: Пересоздает контейнеры даже без изменений.
    - `--scale <service>=<count>`: Масштабирует указанный сервис (например, `web=3` создаст три контейнера для сервиса `web`).
```bash
docker-compose up -d --build
```
### **2. `docker-compose down`**
Останавливает сервисы и удаляет контейнеры, сети и тома, созданные `up`.
- **Флаги:**    
    - `--volumes`: Удаляет созданные тома.
    - `--remove-orphans`: Удаляет контейнеры, не указанные в текущем `docker-compose.yml`.
```bash
docker-compose down --volumes
```
### **3. `docker-compose ps`**
Показывает статус контейнеров, запущенных через Docker Compose.
```bash
docker-compose ps
```
### **4. `docker-compose logs`**
Выводит логи запущенных сервисов.
- **Флаги:**    
    - `-f`: Включает потоковое обновление логов (аналогично `tail -f`).
    - `--tail <lines>`: Показывает последние строки логов (например, `--tail 100`).
    - `<service>`: Вывод логов только указанного сервиса.
```bash
docker-compose logs -f web
```
### **5. `docker-compose build`**
Собирает образы для сервисов, указанных в `docker-compose.yml`.
- **Флаги:**    
    - `--no-cache`: Не использует кэш для сборки.
    - `--pull`: Обновляет образы из реестра перед сборкой.
    - `<service>`: Собирает образ только для указанного сервиса.
```bash
docker-compose build --no-cache
```
### **6. `docker-compose exec`**
Запускает команду внутри запущенного контейнера.
```bash
docker-compose exec web bash
```
В данном случае вы попадете в терминал контейнера `web`.
### **7. `docker-compose run`**
Запускает временный контейнер для выполнения команды.
```bash
docker-compose run web python manage.py migrate
```
Выполняет миграции в Django-приложении.
### **8. `docker-compose stop`**
Останавливает все запущенные контейнеры, но не удаляет их.
```bash
docker-compose stop
```
### **9. `docker-compose start`**
Запускает остановленные контейнеры.
```bash
docker-compose start
```
### **10. `docker-compose restart`**
Перезапускает контейнеры.
```bash
docker-compose restart web
```
### **11. `docker-compose pull`**
Загружает актуальные версии образов из реестра.
- **Флаги:**    
    - `<service>`: Обновляет образ только для указанного сервиса.
```bash
docker-compose pull
```
### **12. `docker-compose config`**
Проверяет файл `docker-compose.yml` на синтаксические ошибки.
- **Флаги:**    
    - `--services`: Показывает список всех сервисов.
    - `--volumes`: Показывает список всех томов.
```bash
docker-compose config --services
```
### **13. `docker-compose rm`**
Удаляет остановленные контейнеры.
- **Флаги:**    
    - `-f`: Удаляет контейнеры без подтверждения.
    - `-v`: Удаляет тома, связанные с контейнерами.
```bash
docker-compose rm -f
```
### **14. `docker-compose kill`**
Прерывает работу всех запущенных контейнеров.
```bash
docker-compose kill
```
### **15. `docker-compose top`**
Показывает процессы, запущенные в контейнерах.
```bash
docker-compose top
```
### **16. `docker-compose version`**
Показывает установленную версию Docker Compose.
```bash
docker-compose version
```
### Полезные сценарии:
- **Запуск с обновлением образов и пересборкой:**
```bash
docker-compose pull && docker-compose up -d --build
```
- **Остановка и удаление всех ресурсов:**
```bash
docker-compose down --volumes --remove-orphans
```
- **Мониторинг работы:**
```bash
docker-compose logs -f
```