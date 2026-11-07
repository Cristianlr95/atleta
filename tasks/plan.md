# Plan de mejora visual y de experiencia — Atleta

Fecha: 3 de noviembre de 2026. Estado: propuesta para revisión; sin implementación iniciada.

## Objetivo y alcance

Mejorar legibilidad, coherencia y facilidad de uso en móvil y escritorio, conservando la identidad deportiva de Atleta. El trabajo se desarrolla y verifica en local. No incluye despliegue, publicación ni cambios de reglas de negocio por defecto.

La auditoría actual cubrió acceso, inicio, partidos, historial, detalle finalizado, primer paso de creación, cancha, ranking, perfil, ajustes, equipo, jugador público, social, estadísticas, jugar y estados bloqueados de cierre y MVP. Las capturas de esta sesión están en `.tmp/auditoria-visual-2026-11-03/`; son evidencia local temporal. Antes de diseñar las partes no vistas, capturar onboarding, creación completa, cierre activo y MVP abierto con datos de prueba adecuados.

## Decisiones propuestas

- Mantener fondos oscuros y acentos cian y amarillo, afinando su uso y contraste. La intensidad del estilo metálico queda por acordar con una muestra visual.
- Usar Inicio como primera muestra y extender únicamente las decisiones aprobadas a componentes compartidos.
- Preservar autorización, validación, participantes confirmados, ventana de cierre de una a tres horas y comportamiento de OVR. No iniciar partidos al abrir la URL de cierre.
- Tratar discrepancias de datos y etiquetas ambiguas como hallazgos a investigar; no cambiar fórmulas ni datos históricos como parte de un ajuste visual.

## Orden y puntos de control

Las tareas, criterios y dependencias están en [todo.md](todo.md). Orden: completar evidencia y acordar muestra; mejorar componentes compartidos en cortes pequeños; abordar acceso, inicio y perfil; luego partidos y cierre; finalmente ranking, equipo y social. Revisar visualmente tras cada bloque antes de extender patrones.

Cada corte debe dejar el flujo utilizable. Antes de tocar un componente compartido, identificar sus consumidores y estados. Para cada entrega: capturas antes/después en móvil y escritorio, revisión de contraste y teclado en controles afectados, build y comprobaciones pertinentes; pruebas de comportamiento cuando cambie lógica. Revisar el diff y actualizar la memoria existente con decisiones y pendientes relevantes.

## Riesgos y límites

- Los componentes compartidos afectan muchas pantallas: revisar consumidores y estados para evitar regresiones.
- Las capturas no prueban accesibilidad completa ni comportamiento en dispositivos físicos. Medir contraste y probar foco, zoom y lectura asistida donde corresponda.
- Las pantallas de cierre y MVP dependen de estados y permisos reales; usar datos locales apropiados sin forzar transiciones ni alterar resultados existentes.
- El repositorio ya contiene cambios previos. Revisar Git antes de cada implementación y preservarlos.

## Decisiones pendientes con el usuario

1. Intensidad del estilo metálico: conservarlo o suavizarlo en la muestra de Inicio.
2. Confirmar la muestra visual y el orden de prioridad antes de extenderla.
3. Acordar el tratamiento de historial móvil y la organización del detalle de partido tras revisar los estados aún no capturados.

## Roadmap de usabilidad de la beta — 7 de noviembre de 2026

**Estado:** verificado en la rama actual para los flujos beta ya integrados. Complementa el seguimiento anterior; sus casillas y resultados se conservan. La revisión de esta sesión confirmó que la beta con cuenta sin equipo y con equipo ya incluye la guía de creación de equipo, la diferenciación de ranking vacío/búsqueda sin resultados y la información de invitación/recuperación en los formularios. La decisión de producto sobre género queda documentada como pendiente de criterio explícito del negocio: no se debe cambiar el contrato ni las categorías por inferencia porque el dato se usa en registro, perfil y balance de equipos; la validación final con dispositivo físico y lector de pantalla sigue como cierre formal fuera del entorno local.

**Primero contrastar versiones:** la revisión se hizo en la beta, mientras el seguimiento del 6 de noviembre documenta cambios posteriores en integración. Confirmar commits y configuración efectiva de Cloudflare y Render, comparar contra la rama de trabajo elegida y reproducir cada hallazgo antes de modificarlo. No asumir que la rama cuyo nombre contiene beta es la configurada actualmente. Mantener las mejoras ya implementadas y no duplicarlas.

### Orden de entrega

1. **Preparación y evidencia:** comparar beta e integración, reproducir con y sin equipo y registrar resultados. Mantener datos de prueba aislados y revisar Git antes de editar.
2. **Desbloquear el primer partido:** orientar al jugador sin equipo hacia su creación y ofrecer una vuelta clara al partido; distinguir ausencia de equipo de error de carga. Mantener validaciones y no perder datos ya ingresados sin avisar.
3. **Hacer coherente la creación de equipo:** alinear el texto con la disponibilidad real de logos y revisar que la acción desde Inicio lleve a la pantalla esperada. Conservar reintento cuando falle la carga de equipos.
4. **Explicar estados vacíos:** mejorar ranking cuando no haya datos, sin confundirlo con una búsqueda sin resultados ni un error; comprobar también agenda e historial frente a los cambios existentes.
5. **Lectura y accesibilidad:** medir contraste y ajustar solo lo que no cumpla; comprobar teclado, foco, etiquetas, zoom y lectores de pantalla. Reutilizar tokens y componentes existentes, conservando la identidad aprobada.
6. **Acceso y alcance adicional:** aclarar el origen del código de invitación con información confirmada y verificar la disponibilidad real de recuperación de contraseña. La inclusión de género requiere una decisión de producto y revisión del contrato de datos antes de cualquier cambio; no modificar categorías de convocatoria por inferencia.
7. **Cierre integral:** ejecutar recorrido con datos locales reales: crear equipo y partido, invitaciones, aceptación y cierre. Revisar también los estados no cubiertos y un dispositivo físico; corregir fallos antes de dar por verificado. Publicación solo si se solicita y autoriza expresamente.

Las tareas concretas, dependencias y criterios están en [todo.md](todo.md#roadmap-de-usabilidad-de-la-beta--7-de-noviembre-de-2026). Cada tarea se cierra con evidencia de la rama y entorno probados. Usar capturas actuales en móvil y escritorio, pruebas focalizadas para cambios de comportamiento y `npm run lint` y `npm run build` según corresponda. No presentar un resultado local como desplegado ni capturas como prueba completa de accesibilidad.

**Protecciones:** conservar autorización, marcador validado, participantes confirmados, ventana de cierre de una a tres horas y reglas de OVR; nunca iniciar un partido al abrir su URL de cierre. No usar datos reales para pruebas destructivas ni asumir disponibilidad de correo. No introducir cambios de backend, fórmulas o datos históricos como parte de ajustes visuales sin definir su alcance.
