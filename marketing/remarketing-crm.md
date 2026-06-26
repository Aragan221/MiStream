# Remarketing y CRM — MiStream

> **La recompra ES el negocio.** Un cliente que renueva 12 meses vale 12× una venta suelta. Sin sistema de renovación, MiStream vive de vender a desconocidos cada mes (agotador e inestable).

## Sistema de renovación (mensual)
1. **Día 25 del mes:** mensaje recordatorio.
   ```
   ¡Hola [nombre]! 👋 Se acerca la renovación de tu [plataforma].
   ¿La dejamos un mes más? Mismo precio, mismo perfil. ⚡
   ```
2. **Si no responde / no renueva:** seguimiento suave.
   ```
   ¿Todo bien con el servicio? ¿Necesitas algo diferente este mes?
   ```
3. **Cliente fiel (3+ meses):** upsell.
   ```
   Por ser cliente fiel: súmale otra plataforma con precio especial.
   ¿Le agregamos [X]? 🙌
   ```

## CRM simple (Google Sheets compartido entre los 4)
| Columna | Dato |
|---------|------|
| Nombre | Cliente |
| WhatsApp/Telegram | Contacto |
| Plataforma(s) | Qué compró |
| Fecha compra | Cuándo |
| Fecha renovación | Cuándo toca recordarle |
| Precio pagado | Cuánto |
| Estado | Activo / No renovó / Referido |
| Referido por | Quién lo trajo |
| Atendido por | Juan Manuel / Lorena / Melisa / Madelyn |
| Notas | Observaciones |

## Reglas del CRM
- **Todo cliente se registra** apenas paga. Sin registro = se pierde la recompra.
- Revisar la columna "Fecha renovación" **a diario** para enviar recordatorios el día 25.
- Marcar quién atendió (para turnos y comisiones justas).
- Tablero compartido para que los 4 vean el estado en tiempo real.

## Meta
- **Retención mensual: 70%** (de cada 10 clientes, 7 renuevan).
- **30% de clientes** traen al menos 1 referido (ver `negocio/referidos.md`).

*Última actualización: 26 junio 2026.*
