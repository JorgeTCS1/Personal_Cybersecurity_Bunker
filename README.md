# Personal_Cybersecurity_Bunker
Implementación integral de seguridad en red doméstica, endpoint inmutable y gestión de identidad.

Personal Hardening Project 2026
Secure Infrastructure & Identity Obfuscation

Este proyecto documenta la implementación de una arquitectura de seguridad integral, cubriendo red local, sistema operativo inmutable y gestión de identidad fragmentada.

1. Network Hardening (ISP Gateway Arris Series)

  Se ha transformado el router del ISP en un nodo de baja visibilidad y alta resistencia.
  - Segmentación de radiofrecuencia: 2.4Ghz Red de baja prioridad para dispositivos IoT y terceros. 5.0 Ghz Red privada exclusiva para el endpoint de trabajo.
  - DNS over IPv6: Implementación de Quad9 para filtrado de malware a nivel de router.
  - ACL & Port Filtering: Bloqueo de puertos NetBIOS (135-139) y SMB (445) para mitigar propagación de ransomware.
  - Stealh Mode: Activado bloqueo de ICMP (Ping) y desativos de WPS/ALG innecesarios.
  - Zero-Visibility Discovery: Se eliminó el "ruido" de red desactivando LLMNR y mDNS a nivel de sistema operativo y servicios (systemd-resolved). Esto evita que el endpoint anuncie su presencia o responda a solicitudes de resolución de nombres locales.
  - Active Defense Verification: Se comprobó mediante técnicas de Banner Grabbing y escaneos SYN que el Gateway implementa una postura de Silent Drop en puertos críticos (como el 22/SSH), ignorando paquetes sospechosos en lugar de rechazarlos, lo que dificulta el mapeo de la red por parte de terceros.

2. Endpoint Hardening (Fedora Silverblue)

Implementación de un entorno de escritorio basado en el principio de Inmutabilidad.

  - OS: Fedora Silverblue (Sistema de archivos de solo lectura).
  - Sandboxing: Apliaciones desplegadas exclusivamente vía Flatpak con gestión de permisos mediante Flatseal.
  - Network Layer: Tunel persistente vía Mullvad VPN y navegación endurecida con LibreWolf.
  - Protocol Masking: Uso de systemctl mask para inhabilitar permanentemente servicios de descubrimiento en el sistema inmutable, garantizando que el endurecimiento persista tras actualizaciones del sistema.
  - Local-Onlyu Resolution: Restricción de los servicios de resolución de nombres DNS exclusivamente a la interfaz de loopback eliminando cualquier vector de escucha externa en puertos UDP.

3. Identity & Entity Management

// Modelo de gestión para prevenir el perfilamiento digital (Anti-Doxing) //

------------------------------
 * Identidad: Vault
 * Propósito: Seguridad Crítica
 * Herramienta: Tuta/Proton
------------------------------
 * Identidad: Formal
 * Propósito: Trabajo/Finanzas 
 * Herramienta: Alias Encriptados
------------------------------
 * Identidad: Leisure
 * Propósito: Ocio/Social
 * Herramientas: Cuentas desechables
------------------------------
 * Identidad: Gov
 * Propósito: Trámites legales
 * Herramientas: Identidad real controlada
------------------------------
Tecnologías utilizadas

 - Sistemas: Linux (Fedora Silverblue), y Arris Firmware.
 - Protocolos: WPA2-AES, IPv6, SMB/CIFS (Blocked), ICMP (Blocked)
 - Seguridad: Quad9 DNS, MFA (TOTP), VPN (WireGuard/OpenVPN)

Fundamentación cientifica

Todas las configuraciones aplicadas se basan en el modelo de Defensa en Profundidad y los estándares de la NIST para la protección de redes domésticas y endpoints críticos.

Resumen

Se ha logrado una transición de una red doméstica estándar a un entorno de Alta Resistencia y Baja Observavilidad. El sistema fedora silverblue actúa como un endpoint 'mudo' que no emite telemetría de descubrimiento, mientras que el Gateway ha sido validado para operar en modo sigilo, filtrando activamente intentos de escaneo y segmentando el tráfico de baja confianza del tráfico de alta integridad. 
