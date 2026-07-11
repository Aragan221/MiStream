# Changelog — MiStream

> Registro de cambios del cerebro de MiStream, con fecha. Si se pierde el chat o se abre una sesión nueva, este documento muestra el estado actual y lo último que se hizo.

---

## 10 julio 2026 — CRM operativo + actualización precios + bot Telegram

### CRM MiStream — OPERATIVO
- ✅ URL: https://mistream-crm.netlify.app/
- ✅ Backend: Google Apps Script v3 (CRUD + correos renovación + remarketing)
- ✅ Dashboard: ventas, facturación, costo, ganancia, renovaciones próximas
- ✅ Registrar, editar, eliminar ventas desde celular
- ✅ Correos automáticos 3 niveles (3 días, 2 días, último día) a crecio.co@gmail.com
- ✅ Remarketing automático para vencidos (correo diario 9AM)
- ✅ Tab "Renovar" con botón copiar mensaje proveedor + marcar renovado
- ✅ 5 ventas reales registradas: $85K facturación, $44K ganancia

### Bot de Telegram — OPERATIVO
- ✅ Bot: @crecio_transcriptor_bot
- ✅ Transcribe videos de YouTube al instante
- ✅ Multi-idioma (es/en/pt/fr/de)
- ✅ Cola de videos + playlists (max 10)
- ✅ Historial (/historial)
- ✅ Modo silencioso (+200 palabras = solo archivos)
- ✅ Título real del video
- ✅ Deduplicación automática
- ✅ Archivo .txt descargable
- ✅ Código en: crecio-cerebro/tools/bot_telegram.py

### Actualización de precios
- ✅ YouTube Premium: costo proveedor $5.500 → **$6.000** (margen baja de $8.500 a $8.000)
- ✅ Combo Música + Video (Spotify + YouTube): costo $11.000 → $11.500, margen $9.000 → $8.500
- ✅ Nuevo combo: 2× YouTube para misma persona → $22.000 (ganancia $10.000)

### Publicidad semana 1
- ✅ 9 piezas generadas con estética casino VIP
- ✅ Prompts completos en `contenido/prompts-publicidad.md`
- ✅ Calendario de publicación definido
- ✅ Prompt "Robar como un artista" (regla 50/50)
- ✅ Prompt incrustar personaje

### Plan operativo
- ✅ `plan-mistream.html` actualizado con copys + flujo de venta + frases rápidas
- ✅ Equipo (Lorena, Melisa, Madelyn) con acceso al CRM y copys

*Última actualización: 10 julio 2026.*

---

## 8 julio 2026 — Sesión completa: V3 reescrito + identidad casino + prompts publicidad

### Cambios mayores
- ✅ `v3-sistema-completo.md` — REESCRITO desde cero con identidad visual casino de lujo, plan actualizado desde 3 julio, 15 secciones completas
- ✅ `marketing/plan-30-dias.md` — REESCRITO completo (4 semanas con acciones por persona, KPIs, checklist)
- ✅ `negocio/combos.md` — Actualizado con 7 combos oficiales que respetan margen $8K+, lista de combos prohibidos
- ✅ `negocio/referidos.md` — PAUSADO hasta validar ventas reales. Todos al mismo precio.
- ✅ `copys/whatsapp.md` — Actualizado: quitados referidos del cierre, agregada referencia a entrega-cuenta.md
- ✅ `copys/entrega-cuenta.md` — NUEVO: 4 plantillas de entrega de cuenta (estándar, combo, minimalista, Spotify/YouTube)
- ✅ `contenido/prompts-publicidad.md` — NUEVO: prompt base cinematográfico + prompt "Robar como un artista" (regla 50/50) + prompt incrustar personaje + 14 variaciones por día + calendario + nombres de archivos
- ✅ `marca/publicidad/` — NUEVA carpeta con imagen god tier de referencia
- ✅ `contenido/semana-1/` — NUEVA carpeta con 9 piezas publicitarias generadas (renombradas con nombres descriptivos)
- ✅ `assets/` — Carpeta creada para HTMLs visuales

### Decisiones tomadas
- Identidad visual: temática **casino de lujo** SOLO para diseño de contenido, NO para lenguaje
- Lenguaje de venta: natural colombiano, humano, desde perfiles personales
- Referidos: PAUSADOS hasta tener ventas reales
- Todos los clientes al mismo precio regular (sin escalones primera vez)
- Formato por defecto de imágenes: 1:1 (cuadrado)
- Logo MiStream: solo texto, nunca inventar símbolo gráfico
- Prompts de publicidad: regla 50/50 al robar de otros (conservar esencia original)

### Prompts de publicidad creados
1. **Prompt base cinematográfico** — estilo Unreal Engine 5, casino VIP, tipografía con degradado
2. **Robar como un artista** — modelar publicidad de otros con regla 50/50
3. **Incrustar personaje** — recrear pieza existente con personaje nuevo integrado
4. **Catálogo limpio** — versión minimalista para enviar en chat
5. **14 variaciones diarias** — semana 1 completa con horarios

*Última actualización: 8 julio 2026.*

---

## 26 junio 2026 — Consolidación V3 (sistema completo)

> Se migró todo lo bueno del documento `v3-sistema-completo.md` (que vivía en `crecio-cerebro`) a este repo, corrigiendo precios, combos y lenguaje legal. **MiStream queda como única fuente de verdad.**

### Nuevo contenido
- ✅ `marca/identidad.md` + `marca/brand-kit.md` — posicionamiento, tono, eslogan, paleta (azul #1E3A5F + ámbar #F59E0B + oscuro #0F172A), tipografía
- ✅ `equipo/roles.md` — **4 integrantes:** Juan Manuel (técnico), Lorena, Melisa, Madelyn (ventas). Corregidas las "dos Madelyn" del V3
- ✅ `cliente/icp-avatares.md` — ICP vs seguidor ideal + 4 sub-avatares
- ✅ `copys/objeciones.md` — respuestas a objeciones con **lenguaje legal cuidado**
- ✅ `contenido/estrategia.md` — niveles de awareness, formatos, batching, calentamiento de cuentas
- ✅ `contenido/guiones.md` — **6 guiones listos para grabar** + banco de hooks
- ✅ `contenido/whatsapp-estados.md` — estrategia de estados para los 4, calendario semanal, 6 plantillas y flujo de saludo
- ✅ `marketing/metas.md` — metas **realistas** (mes 1 ~$300K) + puente numérico hacia los millones (retención 70% + referidos 30%)
- ✅ `marketing/telegram.md`, `marketing/remarketing-crm.md`, `marketing/plan-30-dias.md`, `marketing/riesgos.md`
- ✅ Actualizados `CLAUDE.md`, `README.md` y `marketing/adquisicion.md` (embudo completo + estados WA)

### Correcciones aplicadas (lo que estaba mal en el V3)
- 🔧 **Precios:** Spotify y YouTube a **$14.000** en todos los guiones (antes $12.000; gancho vs competencia $22.000/$24.000)
- 🔧 **Combos:** reemplazados los combos del competidor con margen $0–$2.500 por combos con **piso de margen $8.000** (`negocio/combos.md`)
- 🔧 **Legal:** eliminado "100% legal / autorizado / hackeado". Ahora: "perfiles privados de cuentas compartidas" con soporte y reposición
- 🔧 **Equipo:** definidas 4 personas reales (Lorena, Melisa, Madelyn, Juan Manuel)
- 🔧 **Metas:** añadido el "puente" numérico que faltaba entre el mes 1 realista y la meta grande

### Próximo (mañana)
- Arrancar publicidad por **estados de WhatsApp** de los 4 · luego crear cuentas TikTok/IG · Telegram · CRM

---

## 26 junio 2026 — Creación del repo

### Montaje inicial del cerebro MiStream
- ✅ Creado el repo `MiStream` (privado, push directo a main)
- ✅ `CLAUDE.md` — router del proyecto + regla clave: marketing/embudos/landing se consultan en el repo hermano `crecio-cerebro`
- ✅ `README.md` — puerta de entrada visual (mapa Mermaid, navegación, gancho de valor, pendientes)
- ✅ `negocio/modelo.md` — modelo de arbitraje, roles, datos operativos, visión por fases
- ✅ `negocio/precios.md` — **única fuente de verdad de precios**: costo proveedor + venta regular + primera vez + reglas de pricing
- ✅ `negocio/combos.md` — combos rediseñados con piso de margen $8.000
- ✅ `negocio/referidos.md` — sistema de referidos (modelo actual + modelo a futuro con topes)
- ✅ `propuesta-valor/por-que-mistream.md` — 6 pilares para competir por valor, no por precio
- ✅ `copys/whatsapp.md` — 5 mensajes dinámicos reestructurados para margen
- ✅ `copys/indrive.md` — script de venta a pasajeros de inDrive
- ✅ `marketing/adquisicion.md` — orgánico (inDrive, TikTok/IG, referidos) → pauta
- ✅ `marketing/web-landing.md` — visión de la futura landing (vitrina → WhatsApp)
- ✅ `competencia/vendedora-referencia.md` — precios del competidor + lectura estratégica

### Decisiones de precios tomadas
- **Streaming:** igualamos a la competencia (competir por valor). Netflix $15.000, la mayoría $10.000, Paramount $12.000, Disney+ Premium $14.000.
- **Gancho:** Spotify y YouTube a **$14.000** (competencia cobra $22.000 y $24.000). Margen $8.500 y somos mucho más baratos.
- **Primera vez (inDrive):** margen = costo (ej. servicios de $3.500 → $7.000). Netflix y Disney+ Premium no bajan.
- **Regla de oro:** nunca vender por debajo de 2× el costo. Margen regular objetivo $6.000+, combos $8.000+.

### Pendientes abiertos
- [ ] Confirmar costo proveedor de: Universal+, Flujo TV, Apple TV, DirectTV GO, Viki Rakuten, Telelatino
- [ ] Primera venta consolidada (validar MVP)
- [ ] Crear + calentar TikTok/IG, estructurar Telegram, plan de contenido
- [ ] Landing web cuando el flujo por WhatsApp esté validado

**Contexto:** MiStream nace como proyecto de arbitraje de pantallas de streaming. Comparte conocimiento con `crecio-cerebro` (marketing, embudos, ventas). Precios basados en la lista real del proveedor y comparados con una vendedora competidora.
