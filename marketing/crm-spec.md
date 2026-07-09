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

## IDEAS ADICIONALES (para implementar o evaluar)

### Sistema de escalamiento de correos de renovación

No es un solo correo — es una secuencia que sube la presión:

| Día | Correo | Tono | Acción requerida |
|-----|--------|------|------------------|
| **3 días antes** (ej: 5 agosto) | "Recordatorio: renovación pendiente" | Informativo, tranquilo | Contactar proveedor |
| **2 días antes** (si no se confirmó) | "URGENTE: renovación mañana" | Urgente, destacado | Renovar HOY o se pierde |
| **1 día antes** (último aviso) | "ÚLTIMO DÍA: se vence mañana" | Máxima presión, rojo | Renovar AHORA o el cliente pierde acceso |

**Cómo se confirma:** se responde al correo diciendo "Listo" o se marca en el HTML como "Renovado". Si no se marca como renovado, al día siguiente sube la urgencia.

**Lógica:**
```
Día 1 (3 antes): manda correo nivel 1
  → Si se marca "Renovado" en el CRM → se detiene
  → Si NO se marca → al día siguiente...
Día 2 (2 antes): manda correo nivel 2 (URGENTE)
  → Si se marca → se detiene
  → Si NO → al día siguiente...
Día 3 (1 antes): manda correo nivel 3 (ÚLTIMO DÍA)
  → Si NO se renueva → marca como VENCIDO automáticamente
```

---

### Datos adicionales por cliente (campos extra)

| Campo | Para qué |
|-------|----------|
| Correo de la cuenta | El email con el que se activa la pantalla (para renovar) |
| Contraseña | La clave del perfil (para no depender del chat) |
| Perfil asignado | P1, P2, P3... (si aplica) |

Estos datos son CRÍTICOS para la renovación: cuando le pides al proveedor, necesitas decirle la cuenta exacta.

---

### Copys automáticos para el proveedor

El CRM genera un texto listo para copiar y enviar al proveedor:

```
Hola, para el día [FECHA] se me vence la renovación de:
- Plataforma: [PLATAFORMA]
- Cuenta: [CORREO]
- Contraseña: [CLAVE]
- Perfil: [PERFIL]

Necesito renovar por 1 mes más. Confirma cuando esté listo.
```

Ese texto aparece con un botón "Copiar" en el HTML cuando hay renovación pendiente.

---

### Input inteligente (texto en crudo o audio)

**Opción 1 — Campo de texto libre:**
- Un textarea grande donde la persona pega info en crudo
- Ejemplo: "Madelyn vendió Prime a Camilo 3001234567, 3 meses por 30mil, costo 10500, cuenta prime.user@gmail.com clave Prime123 perfil P2"
- El sistema (Apps Script) parsea la información y la organiza automáticamente en las columnas

**Opción 2 — Audio (Web Speech API — CONFIRMADO, gratis, nativo del navegador):**
- Un botón de micrófono en el HTML (touch target grande)
- Usa `webkitSpeechRecognition` con `lang: 'es-CO'`
- Graba voz → convierte a texto → parsea en campos automáticamente
- $0 costo, funciona en Chrome y Safari iOS
- Necesita internet (envía a servidores Google/Apple para procesar)
- Alta precisión para frases cortas tipo "Madelyn vendió Prime a Camilo tres meses treinta mil"

**Código base confirmado:**
```javascript
var recognition = new (window.SpeechRecognition || window.webkitSpeechRecognition)();
recognition.lang = 'es-CO';
recognition.continuous = false;
recognition.interimResults = false;

recognition.onresult = function(event) {
    var texto = event.results[0][0].transcript;
    // Parsear texto → campos del CRM
    parsearVenta(texto);
};

recognition.start(); // Al tocar botón de micrófono
```

**Prioridad:** Se implementa JUNTO con el campo de texto libre (mismo parseo, diferente input).

---

### Orden de construcción (próxima sesión)

| Prioridad | Qué | Complejidad |
|-----------|-----|-------------|
| 1 | Google Sheets (estructura) | Baja |
| 2 | Apps Script (guardar/editar/eliminar) | Media |
| 3 | HTML (formulario + tabla + dashboard) | Alta |
| 4 | Correos nivel 1 (recordatorio simple) | Media |
| 5 | Escalamiento de correos (3 niveles) | Media |
| 6 | Copys para proveedor (botón copiar) | Baja |
| 7 | Campo de texto libre + micrófono (parseo inteligente) | Media |
| 8 | ~~Audio → transcripción → parseo~~ (YA incluido en #7 con Web Speech API) | — |

---

*Última actualización: 8 julio 2026.*
