# Auto Config MikroTik

Herramienta en español para preparar una configuración inicial de DHCP/LAN, Hotspot, servidor PPPoE y balanceo PCC multi-WAN. Abre `index.html` en un navegador; no necesita dependencias ni un servidor.

## Estado y uso

La herramienta genera scripts `.rsc` localmente para revisar e importar manualmente. **No se conecta al router ni aplica cambios directamente, y no solicita ni guarda credenciales.**

1. Abre `index.html`, completa las interfaces y direcciones según tu topología.
2. Activa los servicios necesarios y pulsa **Generar configuración**.
3. Revisa el script, haz un backup y prueba primero en un equipo de laboratorio.
4. Confirma la compatibilidad con tu versión exacta de RouterOS antes de importar.

## Aviso de corte por falta de pago (sin Hotspot)

Abre `suspension-clientes.html` para generar un script separado para la función Web Proxy integrada de MikroTik, agregar IPs a una address-list y generar una página HTML de aviso. No usa Hotspot ni aplica cambios automáticamente.

- El aviso personalizado se limita a tráfico HTTP. No redirijas HTTPS: el navegador no puede mostrar una página HTTP de aviso dentro de una conexión HTTPS sin interceptación TLS.
- Revisa las reglas existentes: el script agrega reglas al inicio de las cadenas `input` y `forward`; una política de firewall mal ordenada puede dejar clientes bloqueados o exponer servicios.
- La función requiere que Web Proxy esté disponible y habilitado en el equipo. La ubicación de `error.html` depende del modelo y almacenamiento; verifica la ruta en el propio RouterOS antes de reemplazar archivos.
- Los cambios de NAT/firewall pueden cortar el acceso de clientes. Mantén acceso local/gestión de emergencia, haz backup y prueba con una IP de prueba.
- Este generador usa el proxy integrado del MikroTik; no configura un servidor Squid externo en CentOS.

## Alcance y notas

- La plantilla principal está orientada a RouterOS v7 y supone gateways estáticos para PCC.
- Hotspot configura el perfil y servidor, pero no crea cuentas ni personaliza el portal cautivo.
- PPPoE crea el pool, perfil y servidor; los usuarios/secretos PPP se administran aparte.
- PCC distribuye conexiones entre enlaces; no combina el ancho de banda de una sesión individual.
- Los scripts no son idempotentes: importar varias veces puede crear entradas duplicadas.
- La conexión para leer la configuración existente desde la API todavía no está implementada.
