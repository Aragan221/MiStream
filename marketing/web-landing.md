# Visión Web / Landing — MiStream

> Futuro cercano: una página que muestre catálogo, precios, políticas y combos, y que **redirija a WhatsApp para pagar y activar**. Reemplaza el "mandar la lista por chat" una y otra vez.

---

## Objetivo
Que el cliente vea todo (precios, combos, garantía, cómo funciona) en un solo link y llegue al WhatsApp **ya decidido**, listo para pagar. Menos preguntas repetidas, más cierres.

## Qué debe tener la landing (v1, simple)
1. **Hero:** "MiStream — Tus pantallas de streaming, privadas y con respaldo" + botón "Pedir por WhatsApp".
2. **Catálogo con precios** (traído de `negocio/precios.md`): streaming + música, resaltando el gancho Spotify/YouTube.
3. **Combos** (de `negocio/combos.md`).
4. **Por qué MiStream** (los 6 pilares de `propuesta-valor/por-que-mistream.md`): reposición, activación < 1h, trato humano, precio justo, referidos.
5. **Cómo funciona:** pagas → mandas comprobante → activamos en < 1h.
6. **Políticas claras:** qué cubre la reposición, que el soporte es del proveedor, perfiles privados.
7. **CTA repetido a WhatsApp** con mensaje pre-cargado (`wa.me/57XXXXXXXXXX?text=...`).
8. **Sistema de referidos** explicado.

## Flujo
```
Landing (precios + valor + políticas)  →  botón WhatsApp (mensaje pre-cargado)
    →  cierre + pago (Nequi/Bancolombia)  →  activación < 1h
```

## Notas técnicas (a futuro)
- Puede ser una página estática simple (HTML/CSS) en GitHub Pages o Netlify — mismo stack gratuito que usa Creció.
- No necesita carrito ni pasarela al inicio: el pago sigue por WhatsApp. La web es **vitrina + redirección**.
- Para diseño visual, CRO de landing y referencias, ver `crecio-cerebro/skills/marketing/skills-alto-valor-integrados.md` y `skills/contenido/diseno-visual-aplicado.md`.

## Estado
💭 Idea / planeado. Se construye cuando el flujo por WhatsApp esté validado y haya volumen que justifique la vitrina.

*Última actualización: 26 junio 2026.*
