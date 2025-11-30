# Configuración SSH

## Cambio de Puerto

Cambiar el puerto SSH del puerto predeterminado 22 a **[X]**, siendo **[X]** un puerto a tu elección. 

### Pasos:

1. Editar el archivo de configuración SSH:
```bash
sudo nano /etc/ssh/sshd_config
```

2. Buscar la línea `#Port 22` y cambiarla a:
```
Port [X]
```

3. Guardar y salir (Ctrl+O, Enter, Ctrl+X)

4. Reiniciar el servicio SSH:
```bash
sudo systemctl restart sshd
```

5. Verificar el nuevo puerto:
```bash
sudo ss -tulpn | grep ssh
```

### Importante:
- Asegúrate de permitir el puerto **[X]**  en tu firewall antes de reiniciar SSH
- Prueba la conexión con: `ssh -p X usuario@hostname`


## Ajustes y recomendaciones adicionales

A continuación se muestran directivas recomendadas que puedes añadir en `/etc/ssh/sshd_config`. Reemplaza `tuusuario` por tu nombre de usuario real.    

```


# Limitar intentos de login
MaxAuthTries 3

# Evitar resolución inversa de IP para acelerar login
UseDNS no
```

Reemplaza `tuusuario` por tu nombre de usuario real en Arch.

3️⃣ Verifica sintaxis

Antes de reiniciar, comprueba que no haya errores:

```bash
sudo sshd -t
```

Si no devuelve nada → sintaxis correcta

Si muestra errores → corrige la línea indicada

4️⃣ Reinicia SSH

```bash
sudo systemctl restart sshd
sudo systemctl status sshd
```

Verifica que el servicio esté activo y sin errores

5️⃣ Verifica que tu usuario puede conectarse

Desde otra terminal o equipo:

```bash
ssh -p X tuusuario@IP_DEL_SERVIDOR
```