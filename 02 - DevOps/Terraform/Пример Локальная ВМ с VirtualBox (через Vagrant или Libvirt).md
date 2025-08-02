Terraform напрямую не поддерживает VirtualBox, но можно:

1. Использовать **внешние провайдеры**:    
    - [`terraform-provider-vagrant`](https://github.com/bmatcuk/terraform-provider-vagrant)      
    - [`terraform-provider-libvirt`](https://github.com/dmacvicar/terraform-provider-libvirt)        
2. Или проще: вызывать `vagrant` из Terraform через `null_resource` (неоптимально, но возможно):
```yaml
resource "null_resource" "vm" {
  provisioner "local-exec" {
    command = "vagrant up"
  }
}
```
Но это костыль. Лучше:
- использовать `libvirt` на Linux (работает с KVM/QEMU)    
- или работать с облаком, если нужна стабильная виртуализация.