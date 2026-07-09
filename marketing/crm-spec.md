# Especificación CRM MiStream

> Documento de diseño para el sistema CRM completo. Se construye en la próxima sesión.

---

## Arquitectura

```
HTML (Netlify)  →  Google Apps Script (doGet/doPost)  →  Google Sheets (base de datos)
                                                      →  Gmail (correos de renovación a crecio.co@gmail.com)
```

---

## Componentes

| # | Componente | Dónde vive | Qué hace |
|---|-----------|-----------|----------|
| 1 | Google Sheets | Google Drive (compartido con los 4) | Base de datos de todas las ventas |
| 2 | Google Apps Script | Dentro del Sheets | Backend: recibe datos, guarda, edita, elimina, envía correos |
| 3 | HTML | Netlify (URL pública tipo mistream-crm.netlify.app) | Interfaz gráfica para el equipo |
| 4 | Trigger diario | Apps Script (programado) | Revisa renovaciones pendientes y manda correo |

---

## Datos por venta (columnas del Sheets)

| Columna | Campo | Tipo | Ejemplo | Nota |
|---------|-------|------|---------|------|
| A | ID | Auto | 001 | Consecutivo |
| B | Fecha venta | Fecha | 8/07/2026 | Auto (fecha de registro) |
| C | Vendedor | Selector | Madelyn | Juan Manuel / Lorena / Melisa / Madelyn |
| D | Cliente | Texto | Camilo Pérez | Nombre del comprador |
| E | WhatsApp | Número | 3001234567 | Para contactar después |
| F | Plataforma | Selector | Prime Video | Netflix / Disney+ / Max / Prime / Spotify / YouTube / etc. |
| G | Meses pagados | Número | 3 | Cuántos meses pagó de una vez |
| H | Precio cobrado | Número | $30.000 | Lo que pagó el cliente |
| I | Costo proveedor | Número | $10.500 | Lo que se pagó al proveedor (total) |
| J | Ganancia | Fórmula | $19.500 | =H-I (auto) |
| K | Fecha activación | Fecha | 8/07/2026 | Cuándo se activó la pantalla |
| L | Próxima renovación proveedor | Fecha | 5/08/2026 | 3 días antes del vencimiento mensual |
| M | Renovaciones restantes | Número | 2 | Se descuenta cada vez que se renueva |
| N | Estado | Selector | Activo | Activo / Vencido / Renovado / Cancelado |
| O | Notas | Texto | "Primo de Lorena" | Libre |

---

## Lógica de renovaciones

```
Cliente paga X meses:
  → Mes 1: se activa inmediatamente (se paga al proveedor)
  → Mes 2 en adelante: se programa recordatorio 3 días antes del vencimiento
  
Ejemplo: Prime Video, 3 meses, activado 8 julio:
  → Julio: activo (ya pagado)
  → 5 agosto: correo "Renovar Prime de Camilo con proveedor"
  → 5 septiembre: correo "Renovar Prime de Camilo con proveedor"
  → 2 octubre: correo "Contactar Camilo — se vence su plan. ¿Renueva?"
```

---

## HTML — Secciones

### 1. Dashboard (arriba, siempre visible)
- Ventas totales (este mes)
- Facturación total (lo cobrado)
- Costo total (lo pagado al proveedor)
- Ganancia neta
- Renovaciones próximas (3 días)
- Clientes activos

### 2. Formulario de registro (nueva venta)
- Vendedor (dropdown: 4 opciones)
- Nombre cliente
- WhatsApp
- Plataforma (dropdown con todas las opciones)
- Meses pagados (1, 2, 3, 6, 12)
- Precio cobrado (auto-sugerido según plataforma/meses, editable)
- Costo proveedor (auto-sugerido, editable)
- Notas (opcional)
- Botón: REGISTRAR

### 3. Tabla de ventas (todas las ventas)
- Todas las columnas visibles
- Filtros: por vendedor, por estado, por plataforma
- Acciones por fila: EDITAR / ELIMINAR
- Renovaciones próximas destacadas en amarillo/rojo
- Ordenar por fecha (más reciente primero)

### 4. Editar/Eliminar
- Click en EDITAR → abre formulario con datos precargados → guardar cambios
- Click en ELIMINAR → confirma "¿Seguro?" → borra del Sheets

---

## Correos de recordatorio

**Destinatario:** crecio.co@gmail.com
**Frecuencia:** diario (trigger a las 8:00 AM)
**Condición:** si hay renovaciones cuya fecha sea HOY o en los próximos 3 días

**Formato del correo:**

```
Asunto: 🔔 MiStream — Renovaciones pendientes (3)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━
RENOVACIONES PENDIENTES
━━━━━━━━━━━━━━━━━━━━━━━━━━━━

1. Camilo Pérez — Prime Video
   WhatsApp: 3001234567
   Vendedor: Madelyn
   Renovar antes de: 8 agosto 2026
   Acción: Pagar al proveedor

2. Laura García — Netflix
   WhatsApp: 3109876543
   Vendedor: Lorena
   Renovar antes de: 9 agosto 2026
   Acción: Pagar al proveedor

━━━━━━━━━━━━━━━━━━━━━━━━━━━━
MiStream CRM · Automático
━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Pruebas a realizar

| # | Prueba | Datos | Qué validar |
|---|--------|-------|-------------|
| 1 | Venta simple sin renovación | Netflix, 1 mes, $15.000, costo $9.000 | Se guarda en Sheets, aparece en tabla, ganancia = $6.000 |
| 2 | Venta con renovaciones | Prime, 3 meses, $30.000, costo $10.500 | Se crean fechas de renovación automáticas (mes 2 y 3) |
| 3 | Editar registro | Cambiar precio de $30.000 a $28.000 | Se actualiza en Sheets, ganancia recalcula |
| 4 | Eliminar registro | Borrar la venta de prueba | Desaparece de Sheets y de la tabla |
| 5 | Correo de renovación | Poner fecha de renovación = mañana | Llega correo a crecio.co@gmail.com con formato correcto |
| 6 | Dashboard | Después de registrar 3 ventas | Muestra totales correctos (ventas, facturación, ganancia) |

---

## Estilo visual del HTML

- Modo oscuro (igual que el analizador de Creció)
- Paleta MiStream: azul noche + dorado como acento
- Mobile-first (se usa desde celular)
- Botones grandes (touch-friendly)
- Tabla responsive (horizontal scroll en móvil si es necesario)

---

## Hosting

- URL: `mistream-crm.netlify.app` (o similar)
- Un solo archivo HTML con CSS + JS inline
- Se conecta con Google Sheets vía fetch a la URL del Apps Script

---

## Próximos pasos (siguiente sesión)

1. Crear el Google Sheets con las columnas
2. Escribir el Google Apps Script (doGet + doPost + trigger correos)
3. Generar el HTML completo
4. Subir a Netlify
5. Pruebas con los 5 casos

---

*Última actualización: 8 julio 2026.*
