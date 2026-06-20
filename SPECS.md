# Especificación del Panel de Administración - AgentHub

## 1) Descripción breve del producto

AgentHub es una plataforma para administrar el alquiler de agentes de IA y las skills asociadas a esos agentes. El panel de administración permite a un usuario administrador supervisar métricas de negocio, gestionar usuarios y agentes, mantener el catálogo de skills, revisar contrataciones y monitorear errores operativos.

### Usuario administrador

- Es una persona del equipo interno (operaciones, soporte o producto) con acceso completo al panel.
- Necesita ver estado global de la plataforma en un vistazo y ejecutar acciones rápidas por registro.
- Debe poder consultar detalles completos mediante modales sin salir de la vista actual.

## 2) Stack tecnológico y restricciones

- Frontend estático en HTML5.
- El entregable puede resolverse en un único archivo index.html o en varios archivos HTML enlazados por sección.
- Estilos con Tailwind CSS cargado vía CDN.
- No se permiten archivos CSS personalizados.
- No se permiten atributos style inline.
- Interactividad implementada únicamente con JavaScript vanilla.
- No se permite uso de frameworks frontend (React, Vue, Angular, etc.).
- No existe backend: todos los datos para el prototipo son hardcodeados en el cliente.
- El modo oscuro se implementa con utilidades dark: de Tailwind, con un toggle global en la barra superior.

## 3) Estructura general de la interfaz

- Navegación lateral persistente con acceso a seis secciones: Dashboard, Gestión de usuarios, Gestión de agentes, Skills, Contrataciones de agentes y Log de errores.
- La barra lateral debe incluir enlaces de navegación a todas las secciones y un indicador visual claro de sección activa.
- Barra superior persistente con título de sección activa y toggle de modo claro/oscuro.
- Área principal que renderiza una sección a la vez, manteniendo consistencia visual y de espaciado.

## 3.1) Interacciones globales

- El toggle de modo oscuro/claro de la barra superior cambia todo el panel usando utilidades dark: de Tailwind.
- El modo elegido debe conservarse al navegar entre secciones.
- Todos los dropdowns del panel deben cerrarse al hacer clic fuera de su área.
- Todos los modales del panel deben cerrarse al hacer clic sobre el backdrop.

## 4) Especificaciones por sección

### 4.1 Dashboard

1. Componente: cuadrícula de métricas.
   - Contenido: exactamente 4 tarjetas con icono, etiqueta y valor hardcodeado para: ingresos del mes, pérdida del mes (descuentos/cupones), agentes activos en clientes y agentes marcados como fallando.
   - Comportamiento: la cuadrícula debe ser responsive; en desktop 2x2 y en móvil 1 columna.

2. Componente: tarjeta de métrica individual.
   - Contenido: cada tarjeta muestra un color de acento distinto según tipo de métrica.
   - Comportamiento: cada tarjeta aplica sombra sutil y mantiene contraste adecuado en modo claro y oscuro.

3. Componente: marcador de gráfico semanal.
   - Contenido: debajo de la cuadrícula, un contenedor de ancho completo con borde discontinuo y etiqueta centrada para representar la actividad semanal.
   - Comportamiento: se adapta al ancho disponible y conserva proporciones visuales consistentes entre breakpoints.

### 4.2 Gestión de usuarios

1. Componente: tabla de usuarios.
   - Contenido: al menos 5 filas de usuarios hardcodeados, con columnas de nombre, email, plan y badge de estado.
   - Comportamiento: filas con separación visual clara y legibilidad en ambos modos de color.

2. Componente: dropdown de acciones por fila.
   - Contenido: botón de acciones con icono y menú que incluye Ver detalle y Eliminar.
   - Comportamiento: el menú se abre/cierra al hacer clic, y solo puede haber un dropdown abierto por vez.

3. Componente: modal de detalle de usuario.
   - Contenido: muestra el registro completo del usuario seleccionado.
   - Comportamiento: se abre al elegir Ver detalle y se cierra con botón de cerrar o clic sobre el backdrop.

### 4.3 Gestión de agentes

1. Componente: listado de agentes.
   - Contenido: al menos 4 agentes hardcodeados; cada ítem muestra nombre del agente, propietario, estado (activo, inactivo o fallando) y una lista de skills asociadas.
   - Comportamiento: badges de estado codificados por color para lectura rápida.

2. Componente: lista de skills colapsable por agente.
   - Contenido: skills asociadas ocultas por defecto.
   - Comportamiento: un control expandible revela/oculta la lista con transición suave.

3. Componente: dropdown de acciones + modal de configuración.
   - Contenido: menú con Configurar y Eliminar.
   - Comportamiento: al elegir Configurar se abre un modal con el prompt de sistema del agente dentro de un textarea editable; Eliminar requiere confirmación explícita.

### 4.4 Skills

1. Componente: catálogo de skills.
   - Contenido: al menos 4 skills hardcodeadas; cada skill incluye nombre, descripción breve e indicador de cuántos agentes la tienen habilitada.
   - Comportamiento: diseño en tarjetas o filas uniformes con jerarquía tipográfica clara.

2. Componente: bloque explicativo contextual.
   - Contenido: texto breve que explique qué significa una skill en AgentHub.
   - Comportamiento: se muestra fijo al inicio de la sección y mantiene legibilidad en claro/oscuro.

3. Componente: dropdown de acciones por skill.
   - Contenido: opciones Ver detalle y Eliminar.
   - Comportamiento: Ver detalle abre modal informativo y Eliminar solicita confirmación en la misma interacción.

### 4.5 Contrataciones de agentes

1. Componente: tabla de contratos.
   - Contenido: al menos 4 contratos hardcodeados con cliente, agente alquilado, skills contratadas, fecha de inicio, fecha de fin e importe total pagado.
   - Comportamiento: estructura tabular consistente con encabezados visibles y alineación estable.

2. Componente: dropdown de acciones por contrato.
   - Contenido: acción Ver detalle por cada fila.
   - Comportamiento: despliega menú contextual y cierra al hacer clic fuera.

3. Componente: modal de detalle de contrato.
   - Contenido: desglose completo del contrato con listado de skills y precios individuales.
   - Comportamiento: modal centrado, con scroll interno si excede altura y cierre por botón/backdrop.

### 4.6 Log de errores

1. Componente: registro de errores.
   - Contenido: al menos 6 errores hardcodeados con timestamp, nombre del agente, badge de tipo de error con código de color y descripción breve por entrada.
   - Comportamiento: ordenado de más reciente a más antiguo.

2. Componente: badges de severidad/tipo.
   - Contenido: cada error incluye badge visual con código de color según gravedad o categoría.
   - Comportamiento: colores consistentes y distinguibles en modo claro y oscuro.

3. Componente: dropdown de acciones + modal de traza.
   - Contenido: menú con Ver detalle y Marcar como resuelto.
   - Comportamiento: Ver detalle abre modal con la traza completa; Marcar como resuelto actualiza el estado visual del registro.

## 5) Inventario de componentes reutilizables

- Sidebar de navegación persistente.
- Barra superior con título y toggle de modo oscuro.
- Tarjeta de métrica.
- Tabla base reutilizable (encabezado, fila, celda).
- Dropdown de acciones.
- Modal base (header, body, footer, backdrop).
- Badge de estado/severidad.
- Botón primario/secundario/peligro.
- Item colapsable para lista de skills.
- Contenedor placeholder de gráfico semanal.

## 6) Criterios de aceptación

1. Deben existir exactamente seis secciones accesibles desde la navegación lateral persistente.
2. La solución debe implementarse en un único index.html o en varios archivos HTML enlazados por sección, sin backend.
3. Tailwind CSS debe cargarse exclusivamente vía CDN, sin archivos CSS personalizados ni atributos style inline.
4. La barra lateral persistente debe mostrar un indicador claro de la sección activa.
5. El toggle global de modo claro/oscuro debe alternar toda la interfaz usando clases dark: de Tailwind y conservar el modo elegido al navegar entre secciones.
6. Todos los dropdowns deben cerrarse al hacer clic fuera y todos los modales al hacer clic en el backdrop.
7. El dashboard debe mostrar 4 tarjetas de métricas con valores hardcodeados y distribución responsive 2x2 en desktop.
8. Debajo de las métricas del dashboard debe aparecer un marcador de gráfico semanal de ancho completo con borde discontinuo y etiqueta centrada.
9. La sección de usuarios debe mostrar al menos 5 usuarios hardcodeados con nombre, email, plan y badge de estado.
10. El dropdown de acciones en usuarios debe abrirse y cerrarse correctamente, permitiendo Ver detalle y Eliminar.
11. El modal de detalle de usuario debe abrirse desde el dropdown y cerrarse por botón y por clic en backdrop.
12. La sección de agentes debe mostrar al menos 4 agentes hardcodeados con nombre, propietario, badge de estado y skills colapsadas por defecto.
13. La lista de skills en gestión de agentes debe expandirse/contraerse con transición al interactuar.
14. El flujo de configuración de agente debe abrir un modal con el prompt de sistema dentro de un textarea editable.
15. La sección Skills debe mostrar al menos 4 skills hardcodeadas, una explicación contextual y dropdown funcional con Ver detalle y Eliminar.
16. La sección de contrataciones debe mostrar al menos 4 contratos hardcodeados con fechas de inicio/fin y el modal de detalle debe incluir desglose de skills y precios individuales.
17. El log de errores debe mostrar al menos 6 entradas hardcodeadas con badge de tipo de error, permitir Ver detalle en modal y ofrecer la acción Marcar como resuelto.
18. La acción Marcar como resuelto en el log de errores debe cambiar el estado visual del registro afectado.
19. El prototipo debe funcionar sin frameworks, únicamente con HTML, Tailwind CDN y JavaScript vanilla.
