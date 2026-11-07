# Beta: Cloudflare Pages + Render + Neon

> **Estado verificado el 2 de noviembre de 2026:** Cloudflare Pages publica https://atleta-beta.pages.dev/ y Render sirve https://atleta-beta-api.onrender.com con perfil beta y Neon. Flyway aplicó V001–V027; salud, CORS, rechazo de registro sin código o con código incorrecto, registro con código, sesión y configuración de perfil se comprobaron. El código compartido está en la variable `BETA_INVITE_CODE` del entorno de Render; no publicarlo en el repositorio. Google está bloqueado en beta. La cuenta sintética `beta-smoke-20261102@atleta.test` se anonimizó y el acceso posterior respondió 401. En una prueba posterior se crearon e invalidaron un partido sin equipo y dos cuentas sintéticas anonimizadas; aceptar su invitación respondió 500. Se repitió con equipo asociado: creación e invitación aceptada por API, con arquero rotativo conservado; partido invalidado, equipo archivado y cuentas anonimizadas con autorización. La vista previa de cierre respondió 200, sin probar el cierre real. La prueba posterior se detuvo por solicitud del usuario antes de crear el partido; se anonimizaron siete cuentas sintéticas y Neon reportó cero cuentas activas con dominio .test o «smoke» en el correo. Se corrigió la respuesta no autorizada: el backend desplegado devolvió 403 y conservó la invitación pendiente; al aceptar sin equipo se responde 409, se conserva la invitación pendiente y se informa al usuario; la aceptación requiere que el organizador configure un equipo. El arranque en frío tardó unos dos minutos. Se publicó un aviso de conexión que se muestra mientras se inicializa la sesión; se verificó localmente con una demora simulada y en el HTML servido por Pages. Faltan pruebas desplegadas del cierre completo, más variantes de partidos e invitaciones y correo real. El texto inferior conserva la evidencia y planificación anteriores.

## Comprobación local actualizada (2 de noviembre de 2026)

El backend empaquetado con el perfil `beta` arrancó en Windows contra PostgreSQL 18.1 temporal; Flyway aplicó las migraciones hasta V027. El smoke de `atleta-server/scripts/smoke-beta.mjs` terminó correctamente con 420 solicitudes y cuatro trabajadores, usando una cuenta sintética. Se detuvieron los servicios y se retiró la base temporal.

Docker Desktop no arrancó durante esta comprobación. Los resultados del contenedor PostgreSQL 16 y de los límites de 512 MiB y 0,1 CPU indicados abajo son los del 24 de octubre; no se repitieron con los cambios recientes. Flyway advierte que PostgreSQL 18 supera su versión de soporte probado. No se verificaron TLS hacia Neon, proveedores reales ni un despliegue externo.

## Evaluacion del backend (24 de octubre de 2026)

**Validado localmente para una beta pequena con limites reales de 512 MiB y 0,1 CPU.**
Falta desplegar en Render y probar la conexion a Neon por TLS.
Render Free ofrece 512 MB y 0,1 CPU. La configuracion prod actual no es apropiada
para comenzar: Hikari mantiene 20 conexiones y permite 50. El nuevo perfil
independiente `beta` usa 0 conexiones ociosas, maximo 4 y 20 hilos HTTP.

### Resultado del contenedor Linux

Se construyo el Dockerfile real y se probo contra PostgreSQL 16 en una base vacia.
Los limites efectivos fueron 536870912 bytes, sin swap y cuota CPU `10000 100000`.
Java del contenedor: Eclipse Temurin 21.0.12.1. Se midio el pico del cgroup completo,
no solamente el heap Java.

| Medicion | Configuracion inicial | Configuracion final |
| --- | --- | --- |
| RAM maxima permitida | 512 MiB | 512 MiB |
| CPU | 0,1 | 0,1 |
| Arranque Spring | 189,189 s | 110,997 s |
| Pico de memoria del contenedor | 352,6 MiB | 300,5 MiB |
| Smoke | 420 solicitudes, PASS | 420 solicitudes, PASS |
| Concurrencia de lecturas de perfil | 4 | 4 |
| p95 del smoke | 1800 ms | 899 ms |
| Solicitud mas lenta del smoke | 3194 ms | 3992 ms |
| Reinicios / OOM | 0 / 0 | 0 / 0 |
| Migraciones aplicadas | 25 | 25 |

Se conserva `-XX:TieredStopAtLevel=1` en Render y en el compose de comprobacion.
En estos ensayos redujo el arranque aproximadamente 41 % y el pico de memoria.
Limita la optimizacion del compilador JIT; antes de aumentar CPU o la carga de
produccion debe volver a evaluarse. El maximo de latencia aumento en el segundo
ensayo, por lo que no se afirma que todas las operaciones sean mas rapidas.

El resultado respalda usar Free para una beta cerrada de carga baja. No representa
una prueba de capacidad para un numero fijo de usuarios, datos grandes, partidos
completos, correo o TLS hacia Neon. Render puede tener otros tiempos de arranque:
la pantalla de login debe tolerar que el backend tarde cerca de dos minutos en
despertar. No usar sondeos artificiales para mantenerlo activo.

### Pruebas preliminares en Windows

Prueba ejecutada en Windows, Java 21.0.8, PostgreSQL 18 temporal y base vacia:

| Medicion | Resultado |
| --- | --- |
| Heap maximo | 224 MiB |
| Arranque de Spring | 13,135 s |
| Migraciones Flyway | 25 aplicadas correctamente |
| Memoria residente al iniciar | 313,5 MiB |
| Pico residente tras las pruebas | 365,3 MiB |
| Memoria privada tras las pruebas | 391,9 MiB |
| Smoke final | 410 solicitudes, PASS |
| Carga principal | 400 lecturas autenticadas de perfil, 4 trabajadores concurrentes |
| p95 / maximo del smoke final | 9 ms / 155 ms |

Tambien se probaron registro, login, creacion de perfil, CORS permitido y rechazado,
salud/readiness y rechazo de las dos rutas de carga de imagenes. Se ejecuto una
primera tanda adicional de 400 lecturas antes de la tanda final. No se probaron
partidos completos, consultas con grandes volumenes ni picos prolongados.

Estas cifras NO reproducen la cuota de 0,1 CPU ni un limite total de proceso.
`ActiveProcessorCount=1` solo ajusta la JVM; no limita CPU al 10 %. La memoria
reservada virtual tampoco equivale a RAM consumida. Docker Desktop no pudo
levantar el motor Linux en esta sesion. No se midio contra Neon ni con TLS remoto.
El margen observado justifica intentar el plan Free, pero no garantiza capacidad
para un numero de usuarios ni los tiempos de respuesta de Render.

Validacion de preparacion: compilacion Maven del JAR correcta; build de produccion
Angular correcto; 5 pruebas Maven seleccionadas correctas (filtro beta y configuracion
de seguridad). No se ejecuto la suite completa. Angular mantiene avisos existentes
de Stencil y presupuesto CSS, sin errores de compilacion.

Continuacion de la validacion local (mismo dia): el smoke ampliado completo
420 solicitudes, incluyendo creacion/consulta de equipo y partido, lectura de
miembros, renovacion de refresh token y rechazo del access token tras logout.
Resultado PASS, cuatro trabajadores concurrentes, p95 80 ms, maximo 464 ms;
pico residente 359,2 MiB. Estos tiempos siguen siendo locales, sin cuota de CPU.
El frontend compilo con `ATLETA_UPLOADS_ENABLED=false` y genero esa bandera en
app-config.json. `docker compose config --quiet` valido la configuracion de prueba.

Docker quedo operativo tras la reparacion autorizada de sockets temporales.
Windows impedia borrar los sockets; se apartaron sus carpetas con comprobacion
previa de que solo contuvieran los sockets identificados y vacios. Los respaldos
quedaron en `AppData/Local/Docker/run.beta-socket-backup-20261024` y su variante
`-2`, y en `AppData/Local/docker-secrets-engine.beta-socket-backup-20261024` y su
variante `-2`. No se borraron imagenes, volumenes ni contenedores preexistentes.

## Reproducir la verificacion con limites reales

Desde el repositorio **atleta-server**, con Docker funcionando:

```powershell
docker compose -p atleta-beta-check -f docker-compose.beta-check.yml up --build -d
docker compose -p atleta-beta-check -f docker-compose.beta-check.yml logs -f backend
node scripts/check-beta-resources.mjs
docker stats --no-stream
docker compose -p atleta-beta-check -f docker-compose.beta-check.yml down
```

La base de esta prueba es desechable y vive en tmpfs. El puerto 18080 debe estar
libre. El script solo acepta localhost y crea una cuenta sintetica por ejecucion.
El comprobador espera hasta diez minutos por readiness, verifica los limites,
ejecuta el smoke y reporta pico de RAM, eventos OOM y reinicios. Requiere cgroups v2.
Comprobar que no haya OOM/reinicios y que el consumo mantenga margen bajo 512 MiB.
Repetir con datos representativos y flujos de partidos antes de ampliar la beta.

## Repositorios

La carpeta Atleta registra atleta-app y atleta-server como gitlinks y no tiene
`.gitmodules`. Para evitar desplegar carpetas ausentes al clonar, conectar cada
proveedor directamente al repositorio correspondiente: Pages a **atleta-app** y
Render a **atleta-server**. Versionar los cambios dentro de cada repositorio.

## 1. Neon

Crear un proyecto gratuito y una base exclusiva de beta. Elegir una region cercana
a la region del backend. Copiar host, usuario y password desde Connect.

En Render guardar por separado (no incluir credenciales en las URLs):

| Variable | Valor de ejemplo |
| --- | --- |
| DB_JDBC_URL | `jdbc:postgresql://ep-REEMPLAZAR-pooler.REGION.aws.neon.tech:5432/neondb?sslmode=require&connectTimeout=30&socketTimeout=60&tcpKeepAlive=true&prepareThreshold=0` |
| DB_MIGRATION_JDBC_URL | `jdbc:postgresql://ep-REEMPLAZAR.REGION.aws.neon.tech:5432/neondb?sslmode=require&connectTimeout=30&socketTimeout=60` |
| DB_USERNAME | Usuario de Neon |
| DB_PASSWORD | Password de Neon |

Usar los hosts exactos del panel, no construirlos a partir del ejemplo. La primera
URL usa el pooler para la app; Flyway usa una conexion directa a la misma base.
`prepareThreshold=0` evita depender de prepared statements de sesion en el pooler.
No pegar una URL `postgresql://usuario:password@host/db` en DB_JDBC_URL: Java requiere
el prefijo `jdbc:postgresql://`. No importar las cuentas ni los datos locales de dev.

## 2. Render

Crear un Blueprint desde atleta-server y usar `render.yaml` en su raiz.
El Blueprint selecciona Free, Docker y el perfil beta; genera JWT_SECRET.
Completar las variables de Neon y `FRONTEND_URL`, por ejemplo
`https://atleta-beta.pages.dev` (origen exacto, sin barra final).

El servicio acepta el PORT asignado por Render en 0.0.0.0. La comprobacion de salud
usa `/actuator/health/readiness`, sin consultar la base en cada sondeo. Para validar
la conexion real a Neon consultar manualmente `/actuator/health` y los logs Flyway.
Nunca activar dev ni combinar beta con prod. No modificar JWT_SECRET en cada deploy:
invalidaria sesiones. La API publica tendra una URL asignada por Render; copiarla.

## 3. Cloudflare Pages

Conectar atleta-app por Git y configurar:

| Campo | Valor |
| --- | --- |
| Directorio raiz | Raiz del repositorio atleta-app |
| Comando de build | `npm ci && npm run build` |
| Directorio de salida | `www` |
| Node | 22 (archivo .node-version) |
| ATLETA_API_BASE_URL | `https://NOMBRE-REAL.onrender.com/api/v1` |
| ATLETA_ENV_NAME | `beta` |
| ATLETA_STORAGE_PREFIX | `atleta.beta` |
| ATLETA_UPLOADS_ENABLED | `false` |

Configurar las variables para el entorno Production de Pages y volver a compilar
si cambia la URL. Son valores publicos; ningun password, secreto JWT ni credencial
de Neon debe estar en Pages. Las variables del proveedor prevalecen sobre archivos
env locales. No agregar 404.html: Pages resuelve las rutas Angular como SPA.
El archivo `_headers` evita cache de app-config.json y solicita no indexar la beta.
Esto no restringe el acceso: una beta privada requiere un control adicional.

Se desactivo solo la descarga de fuentes durante el build de Angular para que la
compilacion no dependa de Google Fonts. El navegador sigue solicitando esas fuentes
y usa los fallbacks CSS si no estan disponibles.

Actualizar FRONTEND_URL de Render si Pages asigna otro nombre. No permitir
comodines de todos los previews de Pages en CORS.

## Limites funcionales deliberados

- **Fotos y logos:** cargas deshabilitadas con 503 en beta para no perder archivos
  en el disco efimero de Render. Pages oculta los controles con
  `ATLETA_UPLOADS_ENABLED=false`; la API tambien rechaza las cargas.
  Habilitarlas requiere implementar almacenamiento persistente externo.
- **Scheduler:** deshabilitado; Render duerme y no ofrece ejecucion puntual de jobs.
  Los recordatorios y transiciones que dependan del job no son garantizados. Los
  flujos de lectura existentes siguen aplicando sus propias transiciones.
- **Correo:** no hay proveedor de correo configurado. La recuperacion de contrasena
  por email requiere configurarlo y probarlo (considerar restricciones SMTP de Render).
- **Google:** usar registro/login local hasta configurar y verificar el cliente OAuth.
- **IA:** permanece deshabilitada por defecto para evitar dependencias/costos externos.
- **Arranque en frio:** advertir a los probadores que la primera solicitud puede tardar.

## Comprobacion publica antes de invitar usuarios

Verificar salud con DB, registro/login, onboarding, crear equipo y partido,
convocatorias, cierre y consulta de historial. Recargar una ruta interna de Pages;
confirmar HTTPS, URL API y CORS. Revisar RAM/reinicios y tiempos tras una suspension.
Vigilar cuotas de Neon y Render y preparar exportaciones de la base de beta.
No se crearon recursos remotos ni se publicaron cambios desde esta sesion.

Fuentes oficiales:
- https://render.com/docs/compute-plans
- https://render.com/docs/free
- https://render.com/docs/blueprint-spec
- https://neon.com/pricing
- https://developers.cloudflare.com/pages/configuration/serving-pages/
