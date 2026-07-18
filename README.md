# IMPLEMENTACIÓN DE RDP REMOTEAPP, RD WEB ACCESS, IIS Y NPS/RADIUS CON AAA

---

## Información del proyecto

| Información | Detalle |
|---|---|
| **Institución** | Instituto Tecnológico de las Américas (ITLA) |
| **Asignatura** | Seguridad de Redes |
| **Estudiante** | Álvaro Smilk Báez Tavera |
| **Matrícula** | 20211150 |
| **Profesor** | Jonathan Esteban Rondón Corniel |
| **Fecha** | 17 de julio de 2026 |

---

# Entregables

## Video demostrativo

El siguiente video presenta la demostración del correcto funcionamiento de la infraestructura implementada, incluyendo RDP RemoteApp, RD Web Access, IIS, NPS/RADIUS, AAA y autenticación mediante SSH.

**Duración aproximada:** 4 minutos.

**Enlace del video:**  
https://youtu.be/C0146iTGkFA

## Repositorio de GitHub

El repositorio contiene las evidencias y la documentación técnica correspondiente a la implementación de la práctica.

**Enlace del repositorio:**  
https://github.com/smilkxxx/debug-aaa-authentication-debug-aaa-authorization-debug-radius.git

---

# 1. Descripción del proyecto

Este proyecto presenta la implementación de una infraestructura de red orientada a la administración remota, publicación de aplicaciones y autenticación centralizada utilizando Windows Server y routers Cisco.

La práctica integra diferentes tecnologías y servicios, entre ellos Remote Desktop Services (RDS), RDP RemoteApp, RD Web Access, Internet Information Services (IIS), Active Directory Domain Services (AD DS), DNS y Network Policy Server (NPS).

Además, se implementó NPS como servidor RADIUS para centralizar la autenticación de los usuarios que acceden administrativamente a los routers Cisco mediante SSH. Los routers utilizan el modelo AAA (Authentication, Authorization and Accounting) para gestionar el acceso de los usuarios.

La infraestructura permite demostrar el acceso a aplicaciones publicadas mediante RemoteApp, el acceso a una página web personalizada alojada en IIS y la autenticación de usuarios en dispositivos Cisco utilizando RADIUS.

---

# 2. Objetivo general

Implementar una infraestructura que integre servicios de acceso remoto, publicación de aplicaciones, alojamiento web y autenticación centralizada mediante Windows Server, NPS/RADIUS y dispositivos Cisco.

---

# 3. Objetivos específicos

- Configurar Remote Desktop Services en Windows Server.
- Configurar y publicar aplicaciones mediante RDP RemoteApp.
- Implementar RD Web Access para acceder a las aplicaciones publicadas.
- Instalar y configurar Internet Information Services (IIS).
- Crear una página web personalizada.
- Permitir la consulta de la página IIS mediante los servicios implementados.
- Configurar Active Directory Domain Services.
- Configurar DNS para la resolución de nombres dentro del dominio.
- Integrar el equipo cliente Windows al dominio.
- Instalar y configurar Network Policy Server (NPS).
- Configurar NPS como servidor RADIUS.
- Registrar los routers Cisco como clientes RADIUS.
- Configurar un grupo para nivel de acceso 15.
- Configurar un grupo para nivel de acceso 1.
- Implementar AAA en los routers Cisco.
- Crear un usuario local en el router como método alternativo de autenticación.
- Configurar una contraseña para acceder al modo privilegiado.
- Configurar acceso remoto mediante SSH.
- Autenticar usuarios mediante el servidor RADIUS.
- Verificar los procesos de autenticación y autorización AAA.
- Comprobar la comunicación entre los routers Cisco y el servidor NPS/RADIUS.

---

# 4. Tecnologías utilizadas

Durante el desarrollo de la práctica se utilizaron las siguientes tecnologías y servicios:

- Windows Server.
- Windows 10.
- Active Directory Domain Services (AD DS).
- DNS Server.
- Internet Information Services (IIS).
- Remote Desktop Services (RDS).
- RDP RemoteApp.
- RD Web Access.
- Network Policy Server (NPS).
- RADIUS.
- AAA.
- SSH.
- Cisco IOS.
- GNS3.

---

# 5. Topología de red y direccionamiento

La infraestructura fue implementada utilizando GNS3 para la virtualización de los dispositivos de red.

La topología está compuesta principalmente por routers Cisco, un servidor Windows Server y un equipo cliente Windows.

El Windows Server funciona como servidor central de la infraestructura y proporciona los servicios de Active Directory, DNS, IIS, Remote Desktop Services y NPS/RADIUS.

El equipo Windows funciona como cliente y es utilizado para realizar las pruebas de acceso a los servicios publicados, así como las conexiones SSH hacia los routers Cisco.

El servidor Windows utiliza la dirección IP:

`20.21.11.50`

El dominio utilizado en la infraestructura es:

`itla.local`

La red fue configurada para permitir la comunicación entre el servidor, el cliente y los dispositivos Cisco necesarios para completar las pruebas de la práctica.

![Topología y direccionamiento](capturas/01-topologia-y-direccionamiento.png)

*Figura 1. Topología general y direccionamiento de la infraestructura implementada.*

---

# 6. Active Directory y DNS

Se configuró Active Directory Domain Services en Windows Server para proporcionar servicios de dominio dentro de la infraestructura.

El dominio configurado durante la práctica es:

`itla.local`

El servicio DNS se encuentra integrado con la infraestructura de Active Directory y permite realizar la resolución de nombres correspondiente a los equipos y servicios del dominio.

El cliente Windows fue configurado para utilizar la dirección IP `20.21.11.50` como servidor DNS.

Posteriormente, el equipo cliente fue unido correctamente al dominio `itla.local`.

Para verificar el correcto funcionamiento del servicio DNS se realizaron consultas mediante comandos como:

```text
nslookup itla.local
```

y:

```text
nslookup win-j18pujum42n.itla.local
```

Estas pruebas permitieron comprobar que el equipo cliente podía localizar correctamente el controlador de dominio mediante el servicio DNS.

---

# 7. Remote Desktop Services, RemoteApp y RD Web Access

Se configuró Remote Desktop Services en Windows Server con el objetivo de proporcionar acceso remoto a las aplicaciones disponibles en el servidor.

Mediante RDP RemoteApp se publicaron diferentes aplicaciones para que los usuarios autorizados pudieran ejecutarlas remotamente desde el equipo cliente.

Esta tecnología permite proporcionar acceso a una aplicación específica sin necesidad de entregar al usuario una sesión completa del escritorio del servidor.

También se configuró RD Web Access para proporcionar una interfaz web desde la cual los usuarios pueden consultar las aplicaciones publicadas mediante RemoteApp.

Desde el equipo cliente Windows es posible acceder al portal correspondiente, autenticarse utilizando las credenciales autorizadas y visualizar las aplicaciones disponibles.

Posteriormente, se realizaron pruebas de ejecución para comprobar el correcto funcionamiento de las aplicaciones publicadas.

![RemoteApp y RD Web Access](capturas/02-remoteapp-y-rd-web-access.png)

*Figura 2. Acceso a las aplicaciones publicadas mediante RemoteApp y RD Web Access.*

---

# 8. Internet Information Services (IIS)

Se instaló y configuró Internet Information Services (IIS) en Windows Server para proporcionar servicios web dentro de la infraestructura.

Como parte de la práctica se creó una página web personalizada alojada directamente en el servidor.

El funcionamiento del servicio IIS fue comprobado accediendo a la página desde el equipo cliente.

La página personalizada también fue utilizada como parte de las pruebas realizadas mediante los servicios de RemoteApp implementados en Windows Server.

Esta configuración permite demostrar la integración entre los servicios web proporcionados por IIS y la infraestructura de acceso remoto implementada durante la práctica.

![Página personalizada IIS](capturas/03-pagina-personalizada-iis.png)

*Figura 3. Página web personalizada alojada mediante Internet Information Services (IIS).*

---

# 9. Network Policy Server (NPS) y RADIUS

Network Policy Server (NPS) fue instalado y configurado en Windows Server para funcionar como servidor RADIUS.

El objetivo de esta implementación es centralizar las solicitudes de autenticación provenientes de los dispositivos Cisco.

Los routers Cisco fueron registrados como clientes RADIUS dentro de NPS.

Para establecer la comunicación entre los routers y el servidor se configuró un secreto compartido, el cual debe coincidir tanto en la configuración del dispositivo Cisco como en la configuración del cliente RADIUS dentro de NPS.

Cuando un usuario intenta acceder administrativamente al router, el dispositivo envía una solicitud de autenticación hacia el servidor NPS/RADIUS.

NPS procesa la solicitud utilizando las políticas y los usuarios configurados dentro de la infraestructura.

![NPS RADIUS y grupos de privilegios](capturas/04-nps-radius-y-grupos-privilegios.png)

*Figura 4. Configuración del servidor NPS/RADIUS y grupos utilizados para los niveles de acceso.*

---

# 10. Grupos y niveles de acceso

Como parte de la configuración de autenticación y autorización se crearon grupos de usuarios para establecer diferentes niveles de acceso a los dispositivos Cisco.

Se configuraron dos niveles principales.

## Nivel de acceso 15

Este nivel está destinado a usuarios con privilegios administrativos sobre los dispositivos Cisco.

Los usuarios pertenecientes a este grupo pueden recibir un nivel de privilegio elevado de acuerdo con las políticas configuradas en el servidor NPS/RADIUS.

## Nivel de acceso 1

Este nivel está destinado a usuarios con permisos limitados.

Su objetivo es proporcionar acceso al dispositivo sin entregar directamente privilegios administrativos completos.

La utilización de diferentes niveles de acceso permite aplicar una separación de privilegios y proporcionar a cada usuario únicamente los permisos necesarios para realizar sus funciones.

---

# 11. Configuración AAA en los routers Cisco

Los routers Cisco fueron configurados utilizando AAA para gestionar los procesos de autenticación y autorización.

AAA representa tres funciones principales:

**Authentication:** permite verificar la identidad del usuario que intenta acceder al dispositivo.

**Authorization:** permite determinar los permisos y privilegios correspondientes al usuario autenticado.

**Accounting:** permite registrar información relacionada con las sesiones y actividades realizadas por los usuarios.

En esta práctica, RADIUS funciona como mecanismo principal de autenticación.

También se configuró un usuario local en el router como método alternativo de acceso en caso de que el servidor RADIUS no se encuentre disponible.

Adicionalmente, se configuró una contraseña para acceder al modo privilegiado del router.

Esta configuración proporciona un mecanismo adicional de administración y recuperación del dispositivo.

![Configuración AAA y RADIUS](capturas/05-configuracion-aaa-radius-router.png)

*Figura 5. Configuración de AAA y comunicación RADIUS implementada en el router Cisco.*

---

# 12. Autenticación mediante RADIUS

Los routers Cisco fueron configurados para comunicarse con el servidor NPS/RADIUS alojado en Windows Server.

Durante el proceso de autenticación, el usuario inicia una conexión SSH hacia la dirección IP del router.

El proceso general de autenticación funciona de la siguiente manera:

`Cliente Windows → Router Cisco → AAA → RADIUS → NPS / Windows Server`

El router recibe las credenciales del usuario y genera una solicitud RADIUS hacia el servidor NPS.

NPS valida las credenciales y las políticas correspondientes al usuario.

Cuando la autenticación es aceptada, el servidor RADIUS envía una respuesta al router y el dispositivo procesa el acceso de acuerdo con la configuración AAA establecida.

Este mecanismo permite centralizar la administración de las credenciales utilizadas para acceder a los dispositivos de red.

---

# 13. Acceso mediante SSH

Se configuró SSH en los routers Cisco para proporcionar acceso administrativo remoto.

Desde el equipo cliente Windows se realizaron conexiones SSH hacia los routers utilizando usuarios procesados mediante el servidor NPS/RADIUS.

La prueba de autenticación SSH permite comprobar la integración entre el cliente Windows, el router Cisco y el servidor NPS.

El usuario introduce sus credenciales durante la conexión SSH y el router utiliza AAA para enviar la solicitud correspondiente al servidor RADIUS.

La comunicación entre los diferentes componentes permite verificar el funcionamiento de la autenticación centralizada implementada durante la práctica.

![Prueba SSH mediante RADIUS](capturas/06-prueba-ssh-autenticacion-radius.png)

*Figura 6. Prueba de acceso SSH utilizando autenticación mediante NPS/RADIUS.*

---

# 14. Verificación de AAA y RADIUS

Para comprobar el funcionamiento de los procesos de autenticación, autorización y comunicación entre el router y el servidor RADIUS se utilizaron diferentes comandos disponibles en Cisco IOS.

## Debug de autenticación AAA

El siguiente comando permite visualizar información relacionada con el proceso de autenticación de los usuarios:

```text
debug aaa authentication
```

Durante una conexión SSH, este comando permite observar los eventos relacionados con el proceso de autenticación AAA.

## Debug de autorización AAA

El siguiente comando permite visualizar información relacionada con el proceso de autorización:

```text
debug aaa authorization
```

Este proceso permite verificar cómo el router determina los permisos correspondientes al usuario autenticado.

## Debug de RADIUS

Para observar la comunicación entre el router Cisco y el servidor NPS/RADIUS se utilizó:

```text
debug radius
```

Este comando permite visualizar información relacionada con las solicitudes y respuestas RADIUS procesadas durante una autenticación.

## Estado de los servidores AAA

Para verificar el estado del servidor RADIUS configurado se utilizó:

```text
show aaa servers
```

Este comando permite visualizar información sobre el estado del servidor y estadísticas relacionadas con las solicitudes de autenticación.

Durante las pruebas realizadas fue posible observar solicitudes de acceso y respuestas de aceptación generadas por el servidor RADIUS.

## Sesiones AAA

Para consultar información relacionada con las sesiones AAA se utilizó:

```text
show aaa sessions
```

La información disponible puede variar dependiendo de la versión de Cisco IOS utilizada y de las sesiones activas en el dispositivo.

Después de finalizar las pruebas de depuración se utiliza:

```text
undebug all
```

para detener todos los procesos de debug activos en el router.

![Verificación AAA y RADIUS](capturas/07-verificacion-debug-aaa-radius.png)

*Figura 7. Verificación de los procesos de autenticación, autorización y comunicación RADIUS mediante comandos de Cisco IOS.*

---

# 15. Pruebas realizadas

Durante la implementación de la infraestructura se realizaron diferentes pruebas para comprobar el correcto funcionamiento de los servicios configurados.

Entre las principales pruebas realizadas se encuentran:

1. Verificación de conectividad entre los dispositivos de la topología.
2. Resolución DNS del dominio `itla.local`.
3. Resolución DNS del controlador de dominio.
4. Integración del equipo cliente Windows al dominio.
5. Acceso al servicio RD Web Access.
6. Visualización de las aplicaciones publicadas mediante RemoteApp.
7. Ejecución de aplicaciones remotas.
8. Acceso a la página personalizada alojada mediante IIS.
9. Verificación de los grupos de nivel de acceso 15 y nivel de acceso 1.
10. Comunicación entre los routers Cisco y el servidor NPS/RADIUS.
11. Pruebas de autenticación mediante SSH.
12. Verificación del estado del servidor RADIUS mediante `show aaa servers`.
13. Verificación de las sesiones AAA mediante `show aaa sessions`.
14. Depuración del proceso de autenticación AAA.
15. Depuración del proceso de autorización AAA.
16. Depuración de la comunicación RADIUS.

Las pruebas realizadas permitieron comprobar la comunicación entre los diferentes componentes de la infraestructura y verificar el funcionamiento de los servicios implementados.

---

# 16. Evidencias

Las principales evidencias utilizadas para documentar la implementación fueron organizadas utilizando los siguientes nombres:

```text
capturas/
├── 01-topologia-y-direccionamiento.png
├── 02-remoteapp-y-rd-web-access.png
├── 03-pagina-personalizada-iis.png
├── 04-nps-radius-y-grupos-privilegios.png
├── 05-configuracion-aaa-radius-router.png
├── 06-prueba-ssh-autenticacion-radius.png
└── 07-verificacion-debug-aaa-radius.png
```

Cada evidencia fue incluida en la sección correspondiente de esta documentación para facilitar la comprensión del proceso de implementación y demostrar el correcto funcionamiento de los servicios configurados.

---

# 17. Resultados

La implementación permitió integrar correctamente diferentes servicios de Windows Server con mecanismos de administración y autenticación utilizados en dispositivos Cisco.

El cliente Windows pudo comunicarse con el servidor, utilizar los servicios DNS e integrarse al dominio `itla.local`.

Los servicios Remote Desktop Services, RemoteApp y RD Web Access permitieron proporcionar acceso remoto a las aplicaciones publicadas en el servidor.

Internet Information Services permitió alojar y consultar una página web personalizada dentro de la infraestructura.

Por otra parte, NPS fue configurado como servidor RADIUS para procesar las solicitudes de autenticación provenientes de los routers Cisco.

La configuración AAA permitió integrar los mecanismos de autenticación y autorización de los dispositivos Cisco con el servidor RADIUS.

Finalmente, mediante los comandos de monitoreo y depuración fue posible comprobar el estado del servidor RADIUS y analizar los procesos relacionados con la autenticación y autorización.

---

# 18. Conclusión

La realización de esta práctica permitió implementar una infraestructura que integra servicios de acceso remoto, publicación de aplicaciones, alojamiento web y autenticación centralizada.

Mediante Remote Desktop Services, RemoteApp y RD Web Access fue posible proporcionar acceso remoto a las aplicaciones publicadas en Windows Server. La implementación de IIS permitió alojar una página web personalizada y comprobar su funcionamiento dentro de la infraestructura.

La configuración de Active Directory y DNS proporcionó los servicios necesarios para administrar el dominio y permitir la resolución de nombres entre los equipos.

Por otra parte, Network Policy Server fue utilizado como servidor RADIUS para centralizar las solicitudes de autenticación provenientes de los routers Cisco. La implementación de AAA permitió integrar los procesos de autenticación y autorización con el servidor RADIUS y proporcionar acceso administrativo mediante SSH.

Finalmente, los comandos de monitoreo y depuración permitieron verificar la comunicación entre los routers y el servidor NPS/RADIUS, así como analizar el comportamiento de los procesos de autenticación y autorización.

Esta práctica permitió demostrar la integración entre servicios de Windows Server y tecnologías de administración de dispositivos Cisco, proporcionando una infraestructura funcional para el acceso remoto y la autenticación centralizada.
