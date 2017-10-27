#Seguridad

- Confidencialidad
- Integridad
- Disponibilidad
- Autenticación
	- Password
	- Pluggable Auth Modules
		- Interfaz modular entre apps y metodos de auth
		- Da mayor libertad al admin de elegir metodos
		- Permite integrar aplicaciones clasicas con nuevos esquemas de auth

	- Key Exchange
	- LDAP
		- Lightweight Directory Access Protocol (Basado en un directorio activo). Debe de funcionar en base a objetos (usuarios).
	- Biometrics
	- Physical Devices
- No repudiación

## Encripcion
- Asimetrica
	- Web Server
	- Vpn
	- Ssh
- Simetrica
	- Base de datos o password
	- Blowfish: 64 bits de bloque, key de 32 a 448, default de 128
	- Data Encription Standard (DES), 64 bits de bloque y llave de 56
	- MD5: Hash de 128 bits

# Directorios

- Objects:
	- Todo aquello que se le puede dar seguimiento en una DB (Entidades). 
	- Los objetos tienen atributos.
- Schema: Conjunto de atributos de los objetos. Define los tipos de objetos que se pueden generar.
- Inheritance: Permiso de proveer derechos sobre los contenedores por debajo del objeto.
- Class: Template para la creación de objetos.
	- Class + data = Objeto
- Attribute: Campos de datos dentro de una DB de directorios
- Sintaxis: Usados para especificar el tipo de dato que lleva un campo

## Microsoft Active Directory
- Forest: Conjunto de trusted-linked arboles. Parte más alta de la estructura.
- Tree: Colección de uno o más dominios ligados en un trust-link.
- Domain: Servidor que responde a requisiciones de autenticación dentro de un grupo de servidores con la misma base de datos. Identificados por DNS
- Trust: Permite a usuarios de un dominio acceder a otro domino. 
- Site: Localidad geográfica física que contiene redes de hosts.
- Organizational Unit: Agrupación de objetos dentro de un contenedor para una mejor administración. Se le pueden agregar Group Polocies (GPO)

## Novell eDirectory
- Arbol: (root) Contenedor mas alto en la jerarquia
- Country: Objeto opcional par aconectar con directorios globales. Politicamente es solo un arbol.
- Organization: Segundo objeto en la jerarquia, representa el nombre de la compañía
- Organizational unit: Ayuda a organizar los objetos dentro de un directorio
- Partition: División lógica de un directorio. Permite dividir el directorio en particiones de datos. Bueno para redes lentas.
- Replica: Copia o instancia de una partición que es distribuida a los servidores del árbol.
-  Master réplica: Replica de escritura usada par ainiciar los cambios a un objeto o partición.

## Apple's Open Directory
- Standalone Server: No provee información de directorio o a otrs. El directorio local no puede se rcompartido.
- Open Directory Replica: El server tiene una versión réplica de un directorio. La réplica es constantemente replicada con el master.
- Open Directory master: Servidor que provee info y auth a otros directorios LDAP
- Server contectado a un sistema de directorios: Se puede proveer de servicios que requiere un usuario a través de cuentas que están en otro servidor

# DNS

- Nombre jerárquico al que responden computadoras, servicios o cualquier recurso que está en internet. Hace traducción de nombres.
- Hostname -> IP address.
- Inventado en 1983, despues de TCP/IP
- antes las traducciones se hacian en el archivo _hosts_
- En 1984 en Berkley fue escrito en UNIX. Kevin Dunlap lo reescribió y lo llamó BIND
- TLD -> Top Level Domain: Nivel más alto de la jerarquía, operados por la Internet Corporation For Assigned names and Numbers. 
- En México es nic.mx
- Pueden existir hasta 127 niveles de dominios y subdominios.
- Jerarquía: Root > TLD -> Authoritative Server
- tipos de soluciones: iterativas y recursivas
- DNS Caching: Cacheo de tablas DNS para reducir peticiones. TTL.
- Parametros del DNS: 
	- Name: recurso que pertenece a cierto dominio
	- Type: Tipo de registro
		- A: Address Record
		- CNAME: Canonical name (alias)
		- MX: Mail Exchanger
		- PTR: Pointar
		- SOA: Start of Authority
	- Time to Live: TTL, entero de 32 bits en segundos.
	- Class: De clase Internet
- Comandos chidos:
	- nslookup
	- dig
	- ipconfig /flushdns
	- /etc/rc.d/init.d/nscd restart
	- dscacheutil -flushcache

# DHCP
## BOOTP - Bootstrap Protocol
- Protocolo de red usado para obtener IP de un servidor en el boot
- Se usa para dispositivos cuyo SO o imagen esta en red

## DHCP 
- Protocolo de red usado por los dispositivos par ala asignacion inicial de parametros de tal manera de operar en redes de IP.
- Cuando un cliente es configurado como un cliente de DHCP, el cliente manda un broadcast pidiendo la info necesaria.
- Informacion enviada:
	- Default Gateway
	- Domain name
	- DNS servers
	- IP address
	- Mask
	- Lease time
- Para handlear varias VLANs se utiliza la configuracion de IP HELPER ADDRESS
- Tres formas de asignar IP:
	- Dynamic allocation: Rango de IPs
	- Automatic allocation: Parecido al anterior, pero se guarda una tabla de asignaciones para dar preferencia a la misma.
	- Static Allocation: el servidor reserva ciertas IP para ciertas MAC address
-Proceso de peticion
	1. DHCPDISCOVER Broadcast packet sent by client
	2. DHCPOFFER packet replied by server
	3. DHCPREQUEST by client
	4. DHCPPACK by server
	5. Client requests lease extension
	6. Server sends ACK granting lease extension

## NTP
- Sincroniza los relojes de las compus
- UDP puerto 123
- Utiliza el algoritmo de Marzullo, es viejo.
- Se basa en UTC, no usa timezones o DST.
- Clock stratum: niveles jerarquicos como fuentes de reloj
- 64 bits, los primeros son el tiempo a partir de 1 ene 1900, segundos 32 para la parte fraccional de segundos. En el año 2036 se va a reiniciar el conteo.

## NFS
- Sistema de archivos que puede ser compartido en red
- Los primeros fueron desarrollados en 1976 por Digital Equipment Corportaion mediante el protocol File Access Listener
- Apple File Protocol: AFP - Basado en Appletalk. A partir de la 2.2 usa TCP/IP. Puertos: 548 y 427
- SMB: Server Message Block, usado por windows para compartir archivos y recursos. Interactua con NETBIOS, Puerto 445.
- En el 1996, se propuso renombar SMB en CIFS, sin depender de NETBIOS y abierto a TCP.
- SMB2: Introducido con windows vista
- CIFS: Common Internet File System: acelera la transferencia de archivos
- NCP: Netware Core Protocoll. Por Novell, puerto 524.
	- Funciona a traves de particiones o file systems NSS
- NSS: File System usado por netware y adaptado a Linux
- EVMS: Enterprise Volume management System. Administrador de volumenes de NSS. Alternativa para POSIX: LVM2
