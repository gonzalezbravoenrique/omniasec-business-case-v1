## Análisis  

Tras analizar el reto propuesto, sospecho que detrás del incidente **se ha podido ver comprometido anteriormente un host de un/a empleado/a**, ya que la IP atacante (192.168.1.45) corresponde a la red de OMNIASEC.  

El origen del compromiso podría deberse a una técnica de **phishing** o a la instalación de **malware** en el host que permite al atacante controlar remotamente el equipo comprometido. Desde este host, el atacante estaría intentando realizar **movimiento lateral dentro de la red interna para acceder al servidor principal de la BBDD**.

El uso del **puerto 3389** indica además que el intento de acceso se está realizando mediante **RDP** (Remote Desktop Protocol y Escritorio Remoto), por lo que el objetivo no parece ser atacar directamente la base de datos, sino **comprometer primero el servidor que la aloja para posteriormente acceder a la información**, robar credenciales, seguir moviéndose lateralmente o incluso desplegar ransomware.

También me llama la atención la existencia de 2 alertas prácticamente similares, aunque una de ellas aparece parcialmente ofuscada eliminando vocales. Creo que el sistema está enviando la alerta por dos canales distintos, posiblemente mediante notificación estándar y SMS (debido a la longitud de caracteres del segundo mensaje) o algún sistema adicional de monitorización. Aun así, detecto un pequeño error sin mayor importancia en la abreviación “flr”, ya que “favor” sin vocales debería aparecer como “fvr”.

## Medidas inmediatas  

1. **Aislaría** temporalmente mediante firewall el host 192.168.1.45 para evitar comunicaciones entrantes y salientes.  
2. **Bloquearía temporalmente** el acceso RDP al servidor de BBDD.  
3. **Revisaría los logs del servidor** para comprobar si ha existido algún acceso exitoso a la BBDD, desde qué hosts y qué acciones se han llevado a cabo.  
4. **Identificaría a qué empleado/a pertenece el equipo afectado** y, hablaría directamente con él/ella para intentar localizar posibles correos o accesos sospechosos, o cualquier otra pista que me ayude a determinar cómo pudo producirse el compromiso inicial.  
5. Comprobaría el estado de las **actualizaciones del sistema operativo y antivirus del host**, además de realizar un análisis exhaustivo del equipo en busca de malware o actividad sospechosa.  
6. **Reforzaría el acceso al servidor de BBDD** permitiendo únicamente conexiones mediante VPN (Red Privada Virtual) con MFA (Autenticación Multifactor) y desde IPs autorizadas. Además, ubicaría el servidor en una subred separada del resto de equipos, en caso de que actualmente no estuviera segmentado.  
7. En caso de confirmarse acceso a datos sensibles o personales, **informaría a los responsables correspondientes**, y si fuese necesario, a las autoridades competentes.  
8. Finalmente, **documentaría** todo lo sucedido, las acciones realizadas y los hallazgos obtenidos, además de **reforzar la formación** en phishing y buenas prácticas de ciberseguridad para todos los empleados.  


No obstante, y pese al escenario planteado, **tampoco descartaría inicialmente la posibilidad de un falso positivo**, en el que el/la empleado/a estuviese intentando acceder repetidamente porque hubiera olvidado sus credenciales.
