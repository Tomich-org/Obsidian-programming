Создадим контейнер Nginx на порту `8080`.
# Файлы:
## main.tf
```yaml
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0.2"
    }
  }
}

provider "docker" {
  host = "unix:///var/run/docker.sock"
}

resource "docker_image" "nginx" {
  name = var.image_name
}

resource "docker_container" "web" {
  name  = "nginx_web"
  image = docker_image.nginx.name

  ports {
    internal = 80
    external = 8080
  }
}

```
## variables.tf
```yaml
variable "image_name" {
  type    = string
  default = "nginx:latest"
}
```
## outputs.tf
```yaml
output "nginx_url" {
  value = "http://localhost:8080"
}
```
## команды
```bash
terraform init        # инициализация
terraform plan        # покажет, что будет создано
terraform apply       # создаёт образ и контейнер
```

После выполнения контейнер будет доступен по адресу: `http://localhost:8080`.