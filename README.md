# ESP-MQTT Mosquitto User y Password

Este ejemplo conecta el ESP32 al broker Mosquitto utilizando usuario y contraseña



## Configuracion SSID y PASS WiFi

Este ejemplo usa la funcion "example_connect()" de la platarforma ESP-IDF.

Para configurar el SSID y PASSWORD se debe hacer clic en el icono "engranaje" (configuración)
de la barra inferior del VSCode y allí en la sección de WiFi se podrán configurar los datos
necesarios



## Configurar URI del Broker

Dentro del archivo app_main.c hay que configurar la definición "BROKER_URI" que se encuentra
al inicio del archivo, colocando los datos correctos del broker a utilizar.



## Crear archivo de usuarios y contraseñas para el Mosquitto Broker

Crear un simple archivo de texto ingresando en cada linea los usuarios y sus contraseñas en texto plano.
Que se vea del siguiente mood:

juan:juanPasswd
pepito:pepinPass

guardar el archivo, por ejemplo como "passfile"

luego ejecutar el siguiente comando: mosquitto_passwd -U passfile
(tenemos que tener instalado el mosquitto-client)

una vez ejecutado el comando, si abrimos el archivo "passfile" se verá del siguiente modo:

juan:$7$101$MKELi4uwM9Bytcy2$tfAMpvDhzECPRmazv/sKZ5o2/3lNPUoDb8LttKI1EVsJKhdL0BVzRIcUctFEF34GFAA+SitJ9j46NyZpdICQiA==
pepito:$7$101$tIVbHwY3dhGAfGGS$/IGerQHGTWsQIw2bK0POJYVMNZOwOlMk+Uxl8T6c8uKa5vKJAn5kWJMLFtNRd8YTS5WDe+cJdzsEPsMjNyY9Dw==

En el archivo mosquitto.conf, se incluye el path a este archivo que contiene los usuarios y sus contraseñas
utilizando la opcion "password_file":
(password_file /etc/mosquitto/passfile)



## El siguiente es el contenido del archivo mosquitto.conf que permite correr este ejemplo:

persistence true

persistence_location /var/lib/mosquitto/

log_dest file /var/log/mosquitto/mosquitto.log

include_dir /etc/mosquitto/conf.d

#allow_anonymous true

password_file /etc/mosquitto/passfile

listener 1883

#listener 8883

#cafile /etc/mosquitto/certs/ca.crt

#keyfile /etc/mosquitto/certs/server.key

#certfile /etc/mosquitto/certs/server.crt

#require_certificate true

#use_identity_as_username true




### Ejemplo de la salida por consola al ejecutar la aplicación:

```
I (3714) event: sta ip: 192.168.0.139, mask: 255.255.255.0, gw: 192.168.0.2
I (3714) system_api: Base MAC address is not set, read default base MAC address from BLK0 of EFUSE
I (3964) MQTT_CLIENT: Sending MQTT CONNECT message, type: 1, id: 0000
I (4164) MQTT_EXAMPLE: MQTT_EVENT_CONNECTED
I (4174) MQTT_EXAMPLE: sent publish successful, msg_id=41464
I (4174) MQTT_EXAMPLE: sent subscribe successful, msg_id=17886
I (4174) MQTT_EXAMPLE: sent subscribe successful, msg_id=42970
I (4184) MQTT_EXAMPLE: sent unsubscribe successful, msg_id=50241
I (4314) MQTT_EXAMPLE: MQTT_EVENT_PUBLISHED, msg_id=41464
I (4484) MQTT_EXAMPLE: MQTT_EVENT_SUBSCRIBED, msg_id=17886
I (4484) MQTT_EXAMPLE: sent publish successful, msg_id=0
I (4684) MQTT_EXAMPLE: MQTT_EVENT_SUBSCRIBED, msg_id=42970
I (4684) MQTT_EXAMPLE: sent publish successful, msg_id=0
I (4884) MQTT_CLIENT: deliver_publish, message_length_read=19, message_length=19
I (4884) MQTT_EXAMPLE: MQTT_EVENT_DATA
TOPIC=/topic/qos0
DATA=data
I (5194) MQTT_CLIENT: deliver_publish, message_length_read=19, message_length=19
I (5194) MQTT_EXAMPLE: MQTT_EVENT_DATA
TOPIC=/topic/qos0
DATA=data
```
