# Auto Config MikroTik

Interfaz en español para preparar una configuración inicial de DHCP/LAN, Hotspot, servidor PPPoE y balanceo PCC multi-WAN. Abre `index.html` en un navegador; no necesita dependencias ni un servidor web.

## Estado de esta versión

Esta versión **no se conecta al router ni aplica cambios**. Genera un script `.rsc` en el navegador para revisión e importación manual. No solicita ni guarda credenciales. La conexión directa desde el navegador a RouterOS expondría credenciales y suele fallar por CORS/TLS; para aplicar cambios desde una aplicación hace falta un backend autenticado como intermediario.

## Uso

1. Abre `index.html` y completa los nombres reales de las interfaces y las direcciones de tu red.
2. Activa los servicios necesarios y pulsa **Generar configuración**.
3. Revisa el script y descarga el `.rsc`.
4. Haz un backup del router y prueba primero en un equipo de laboratorio. Comprueba que la sintaxis sea compatible con tu versión exacta de RouterOS antes de importar.

## Alcance y notas

- La plantilla está orientada a RouterOS v7 y supone gateways estáticos en cada WAN.
- Hotspot configura el perfil y el servidor, no crea cuentas de usuario ni personaliza el portal cautivo.
- PPPoE crea el pool, perfil y servidor; los usuarios/secretos PPP se administran aparte.
- PCC distribuye conexiones entre enlaces; no combina el ancho de banda de una sesión individual. La política de rutas, NAT y excepciones para redes locales debe revisarse con la topología real.
- El script no es idempotente: volver a importarlo puede crear entradas duplicadas.

## Siguiente paso para integración API

Para conectar y aplicar configuraciones, confirmar primero: versión exacta de RouterOS, método de acceso (REST de RouterOS v7 o API), interfaces LAN/WAN, tipo de gateway de cada ISP (estático, DHCP o PPPoE), subredes requeridas y si el servidor será local o remoto. La integración debe usar un backend con TLS, autenticación, permisos mínimos, validación de entradas y confirmación explícita antes de aplicar cambios; nunca se deben poner credenciales del router en el HTML.
