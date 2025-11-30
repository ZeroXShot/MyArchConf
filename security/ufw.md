# Configuración Intermedia de UFW en Arch Linux

## Instalación

```bash
sudo pacman -S ufw
```

## Configuración Inicial

### 1. Habilitar UFW

```bash
sudo ufw enable
```

### 2. Establecer políticas por defecto

```bash
# Denegar todo lo entrante
sudo ufw default deny incoming

# Permitir todo lo saliente
sudo ufw default allow outgoing

# Rechazar las conexiones denegadas en lugar de ignorarlas
sudo ufw default reject routed
```

## Reglas de Puertos Comunes

### Permitir SSH (importante para acceso remoto)

```bash
#Siendo X tu puerto de SSS
sudo ufw allow X/tcp
# O más específicamente
sudo ufw allow X/tcp comment "SSH"
# Denegar el puerto 22 si se ha cambiado el puerto ssh por defecto
sudo ufw deny 22/tcp

```

## Gestión de Reglas

### Ver estado y reglas

```bash
# Ver estado
sudo ufw status

# Ver estado detallado con números
sudo ufw status numbered

# Ver estado verbose
sudo ufw status verbose
```

### Recargar reglas

```bash
sudo ufw reload
```

### Resetear UFW

```bash
sudo ufw reset
```

## Logging

### Habilitar logging

```bash
sudo ufw logging on

# Configurar nivel de logging (low, medium, high)
sudo ufw logging medium
```

### Ver logs

```bash
# Arch Linux
sudo journalctl -u ufw

# O en syslog
sudo tail -f /var/log/ufw.log
```

## Configuración Avanzada

### Rate limiting

```bash
# Limitar conexiones SSH a 6 intentos cada 30 segundos
sudo ufw limit 22/tcp comment "SSH con límite de tasa"
```

### Verificación de sintaxis

```bash
# Antes de aplicar cambios
sudo ufw show added
```

## Integración con Systemd

### Ver estado del servicio

```bash
sudo systemctl status ufw
```

### Habilitar al iniciar

```bash
sudo systemctl enable ufw
```

### Deshabilitar al iniciar

```bash
sudo systemctl disable ufw
```


## Referencias

- [Documentación oficial de ufw](https://wiki.ubuntu.com/UncomplicatedFirewall)
- [Arch Linux UFW](https://wiki.archlinux.org/title/Uncomplicated_Firewall)
