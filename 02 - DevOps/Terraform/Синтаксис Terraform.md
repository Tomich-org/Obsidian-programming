Terraform использует **HCL (HashiCorp Configuration Language)** — простой язык с блоковой структурой. Пример базового синтаксиса:
```yaml
provider "docker" {
  host = "unix:///var/run/docker.sock"
}

resource "docker_container" "nginx" {
  name  = "nginx_server"
  image = docker_image.nginx.latest
  ports {
    internal = 80
    external = 8080
  }
}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}
```

Что тут происходит:
- `provider "docker"` — указывает, что мы работаем с Docker.
- `resource "docker_image"` — говорит, что нужно скачать образ `nginx:latest`.
- `resource "docker_container"` — создаёт контейнер на основе этого образа и проксирует порт.