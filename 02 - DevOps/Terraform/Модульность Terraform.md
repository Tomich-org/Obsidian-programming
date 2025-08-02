# Модули
**Модуль** — это просто подкаталог с `.tf`-файлами, содержащими логику, которую можно переиспользовать.

Например:
```css
project-root/
├── main.tf
├── variables.tf
├── modules/
│   ├── nginx/
│   │   ├── main.tf
│   │   ├── variables.tf
│   │   └── outputs.tf
│   └── db/
│       ├── main.tf
│       ├── variables.tf
│       └── outputs.tf
```

Ты выносишь логику контейнеров, баз данных, сетей и т.п. в отдельные папки-модули и подключаешь их из `main.tf`:
```yaml
module "nginx" {
  source = "./modules/nginx"
  image_name = "nginx:latest"
  container_port = 8080
}

module "db" {
  source = "./modules/db"
  db_name = "mydb"
}
```
Модули:
- делают проект **модульным**;    
- помогают избежать **повторений**;    
- позволяют создавать свои собственные **каталоги компонентов**, как в конструкторе.
# Workspace
Terraform поддерживает **рабочие пространства** (workspaces), чтобы ты мог использовать **одну конфигурацию** с разными наборами данных.

Например:
```bash
terraform workspace new dev
terraform workspace new prod
```

Потом в коде можно обращаться к имени окружения:
```yaml
resource "docker_container" "web" {
  name = "nginx-${terraform.workspace}"
  ...
}
```

Однако в реальных проектах часто используют **отдельные каталоги/модули для окружений**, т.к. `workspace` ограничен в возможностях. Лучше:
```css
environments/
├── dev/
│   └── main.tf
├── stage/
│   └── main.tf
├── prod/
│   └── main.tf
```
# Разделение на слои: сеть, БД, сервисы
Например:
- `network/` — создаёт docker network    
- `infra/` — создаёт БД и volume'ы    
- `services/` — деплой приложений    

Ты можешь запускать их отдельно:
```bash
cd network && terraform apply
cd infra && terraform apply
cd services && terraform apply
```
Это удобно, если:
- изменения затрагивают только часть инфраструктуры;    
- разные команды отвечают за разные уровни.
# Как организовать большой проект?
Пример структуры большого проекта на Docker и VM:
```css
terraform/
├── modules/
│   ├── vm/
│   │   └── main.tf
│   ├── docker_app/
│   │   └── main.tf
│   └── network/
│       └── main.tf
├── environments/
│   ├── dev/
│   │   └── main.tf
│   └── prod/
│       └── main.tf
├── terraform.tfvars
└── backend.tf
```
