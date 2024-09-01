# Configuración de Windows

## Restaurar el clic derecho en Windows 11
### Pasos:
1. Abrir CMD introducir siguiente comando:
    ```bash
    reg.exe add "HKCU\Software\Classes\CLSID\{86calaa0-34aa-4e8b-a509-50c905bae2a2}\InprocServer32"/f/ve
    ```

2. luego reiniciar el explorador de archivos

## Corregir Alert Warning de XAMPP
### Pasos:
1. Editor de Registro:
    ```bash
    Equipo\HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
    ```

2. Cambiar valor de 1 a 0 en:
    ```bash
    EnableLUA
    ```

## Configurar la conexion de WiFi movil sin limites (DefaultTTL)
### Pasos:
1. windows+R:
        ```bash
    regedit
    ```

2. Dirigir a esta direccion:
    ```bash
    Equipo\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters
    ```

3. Crear archivo DWORD (32 bits):
    ```bash
    valor de DWORD (32 bits)
    ```

4. Cambiar nombre al archivo poner:
    ```bash
    DefaultTTL
    ```

5. Modificar
- Base:
    ```bash
    Decimal
    ```
- Información del valor: 
    ```bash
    65
    ```

6. "REINICIAR MAQUINA"

## Cambiar el DefaultTTL en Linux

### Pasos para cambiar el `DefaultTTL` en Linux Mint 22

1. **Abre una Terminal**:
   - Puedes hacerlo presionando `Ctrl + Alt + T` o buscando "Terminal" en el menú de inicio.

2. **Edita el archivo de configuración de sysctl**:
   - Ejecuta el siguiente comando para abrir el archivo de configuración de `sysctl` en un editor de texto (usaremos `nano` en este ejemplo):
   ```bash
   sudo nano /etc/sysctl.conf
   ```

3. **Añade o Modifica la Configuración de `TTL`**:
   - Desplázate hacia abajo en el archivo abierto hasta el final.
   - Añade la siguiente línea para establecer el valor de `DefaultTTL` en 65 (este es un número comúnmente utilizado para evitar limitaciones):
   ```bash
   net.ipv4.ip_default_ttl=65
   ```
   - Si esta línea ya existe en tu archivo, simplemente cambia el número a 65 o al valor que prefieras.

4. **Guarda y Cierra el Editor de Texto**:
   - Guarda los cambios presionando `Ctrl + O` y luego `Enter`.
   - Sal del editor presionando `Ctrl + X`.

5. **Aplica los Cambios**:
   - Para aplicar los cambios realizados en el archivo de configuración de `sysctl`, ejecuta el siguiente comando en la terminal:
   ```bash
   sudo sysctl -p
   ```

6. **Verifica que el Cambio se haya Aplicado**:
   - Puedes verificar que el valor de TTL se ha establecido correctamente ejecutando:
   ```bash
   cat /proc/sys/net/ipv4/ip_default_ttl
   ```
   - Debería mostrar el valor `65` si los cambios se aplicaron correctamente.

7. **Reinicia tu Conexión de Red**:
   - Reinicia tu conexión de red o simplemente reinicia tu computadora para asegurarte de que los cambios se apliquen completamente.

### Configuración Adicional para Conexiones de Hotspot

Algunos operadores de red pueden requerir configuraciones adicionales para que el cambio de TTL tenga efecto:

- **Configura el mismo TTL en el dispositivo móvil**:
  - Algunos routers móviles permiten cambiar el valor de TTL de manera similar, asegúrate de que ambos dispositivos (Linux Mint y tu Samsung A30S) estén configurados de manera compatible.

Siguiendo estos pasos, tu Linux Mint debería configurarse para usar un TTL sin restricciones al conectarse a un hotspot móvil, lo que debería permitirte compartir internet sin limitaciones de tu operador móvil.