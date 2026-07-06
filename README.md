# Seguimiento de pedidos — Nefusac

Aplicación web para el seguimiento de pedidos de un negocio de fabricación e instalación de ventanas: desde la solicitud del cliente hasta la entrega final, con fotos, reportes y calendario.

Es un **único archivo HTML autocontenido** (`index.html`) que se conecta a una **base de datos en la nube (Supabase)**: todos los usuarios ven los mismos pedidos desde cualquier celular o computadora, en tiempo casi real. No necesita instalación; solo un navegador moderno y conexión a internet.

## Flujo de trabajo (5 etapas)

1. **Solicitud de visita o solicitud de pedido** — Vendedor
2. **Programación de visita** — Técnico
3. **Visita técnica** — Técnico (tipo de ventana, fotos, días de fabricación)
4. **Confirmación de pago** — Logística
5. **Pedido finalizado** — Técnico (entrega, foto de ventana y foto de conformidad)

## Usuarios y permisos

| Usuario | Clave | Puede registrar | Puede modificar |
|---|---|---|---|
| Vendedor | `vendedor123` | Solicitud | No |
| Técnico | `tecnico123` | Programación, Visita, Finalizado | No |
| Logística | `logistica123` | Pago | No |
| Administrador | `admin123` | Todas las etapas | Sí (y puede eliminar pedidos) |

Todos los usuarios pueden **visualizar** todos los pedidos y generar reportes.

> ⚠️ **Nota importante:** este login organiza los roles del día a día, pero no es seguridad real, ya que todo vive en el navegador sin servidor. Las claves están en el código. Para cuentas realmente protegidas se necesitaría un backend.

## Funciones principales

- Tarjetas de pedido con barra de progreso y color según etapa
- Búsqueda por cliente y filtros por etapa (finalizados se ordenan al final)
- Fotos múltiples por campo, con compresión automática, descarga individual y eliminación
- Reporte imprimible por pedido con todas las etapas, fotos y cronología de días
- Calendario mensual con visitas técnicas y entregas (toca un evento para abrir el pedido)
- Exportación a CSV de todos los pedidos
- Los datos se guardan en una base de datos en la nube (Supabase): **todos los dispositivos ven los mismos pedidos**, con sincronización automática cada 20 segundos y reintento de guardado si se pierde la conexión
- Migración automática: si un navegador tenía pedidos guardados de la versión anterior (localStorage), se suben solos a la nube la primera vez que se abre esta versión

## Cómo usarla

**Opción 1 — Local:** descarga `index.html` y ábrelo con doble clic en cualquier navegador.

**Opción 2 — GitHub Pages (gratis):** en este repositorio, ve a *Settings → Pages*, en "Branch" elige `main` y carpeta `/ (root)`, guarda, y en unos minutos la app quedará publicada en `https://TU-USUARIO.github.io/NOMBRE-DEL-REPO/`.

**Opción 3 — Netlify Drop:** arrastra la carpeta con `index.html` a [netlify.com/drop](https://app.netlify.com/drop).

## Tecnología

- HTML + CSS + JavaScript puro (vanilla), sin frameworks ni librerías
- Base de datos: Supabase (PostgreSQL) mediante su API REST, con clave publicable
- Requiere conexión a internet para sincronizar; si se corta, los cambios pendientes se reintentan automáticamente
