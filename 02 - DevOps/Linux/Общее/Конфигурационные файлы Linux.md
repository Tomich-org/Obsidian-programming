Конфигурационные файлы в Linux хранятся в `/etc`, но так же могут храниться в `/usr/local/etc`, `/opt`, `/var/lib` (для некоторых сервисов)
# Системные конфигурационные файлы
 - `/etc/passwd` - информация о пользователях (имя, UID, GID, домашняя директория , shell)
 - `/etc/shadow` - хешированные пароли пользователей
 - `/etc/group` - список групп и их участников
 - `/etc/hostname` - имя хоста системы
 - `/etc/hosts` - сопоставление IP-адресов и имен хостов (локальный DNS)
 - `/etc/resolf.conf` - DNS-серверы для системы
 - `/etc/fstab` - точки монтирования файловых систем
 - `/etc/mtab` - список текущих смонтированных файловых систем
# Конфигурация сетевых сервисов
- `/etc/network/system/` - кастомные юниты `systemd`
- `/etc/sysconfig/network-scripts/ifcfg-eth0` - конфигурация сетевых интерфейсов
- `/etc/ssh/sshd_config` - конфигурация SSH-сервера
- `/etc/nginx/nginx.conf` - конфигурация Apache
- `/etc/hosts.allow` и `/etc/hosts.deny` - настройка доступа через TCP  Wrappers
# Системные службы и их конфигурация
- `/etc/systemd/system` - кастомные юниты `systemd`
- `/etc/init.d/` - скрипты запуска (в старых системах)
- `/etc/contrab` - планировщик заданий (cron)
- `/etc/logrotate.conf` - конфигурация системных логов
# Безопасность и доступ
- `/etc/sudoers` - правила доступа для sudo
- `/etc/security/limits.conf` - лимиты ресурсов для пользователей
- `/etc/pam.d` - конфигурация аутентификации PAM
- `/etc/selinux/config` - настройки SELinux (RHEL)