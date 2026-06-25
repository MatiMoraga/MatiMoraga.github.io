---
title: "Destilación multicomponente ideal"
date: 2026-06-18
summary: "Modelamiento"
tags: 
  - Python
  - Modelamiento
  - Procesos
  - Oil & Gas
featured: true
status: "Completado"
role: "Lead Developer"
duration: "1 semana"
team_size: 1
highlights:
  - "Handles 10k+ concurrent users"
  - "99.9% uptime SLA"
  - "Processing $50k+ monthly transactions"
  - "60% faster page load vs competitors"
---

Se elige el siguiente problema para resolver en Python

## Problema

Una corriente de líquido y vapor saturados (q = 0.30) a una presión de 405.4 KPa se alimenta a una torre de destilación en un flujo de 1000 mol/h. La composición global de la alimentación es n-butano ($z_{but}$ = 0.35), n-pentano ($z_{pent}$ = 0.30), n-hexano ($z_{hex}$ = 0.20) y n-heptano ($z_{hept}$ = 0.15). La corriente es destilada de manera de recuperar el 97% del n-pentano en el destilado y el 85% del n-hexano en el producto de cola. Calcule lo siguiente:

+ Flujo y composición de los productos y temperaturas del tope y la base de la columna.
+ Número de etapas a reflujo total y distribución de otros componentes en los productos.
+ Razón mínima de reflujo, número de etapas a 1.2 $R_{mín}$ y localización del plato de alimentación.

## Resolución

### Método _short cut_ (aproximación de diseño)
- **Elección de componentes claves** - Resolución de balances de masa e imposición de recuperaciones respecto a clave liviana (n- pentano) y pesada (n- heptano).
- **Temperaturas del tope y cola** - Estimación mediante punto de burbuja utilizando librería _chemicals_ y _scipy_.
- **Método FUG** - Cálculo de etapas mínimas por método Fenske, reflujo mínimo por Underwood y número de etapas reales por Gilliland, resolviendo iterativamente con _fsolve_.
- **PLato de alimentación** - Resolución de ecuación empírica de Kirkbride.

### Método riguroso MESH
- **Definición de variables** - Cálculo de flujos y razón de _boil up_ según McCabe-Thiele.
- **Balance por etapas** - Definición de problema lineal $Ax= b$ con matriz tridiagonal con coeficientes variables en función de la temperatura por etapa.
- **Resolución de balances** - Resolución con interación de punto fijo sobre el vector de temperatras para encontrar fracciones de molares en los flujos de líquido.
- **Problema de optimización** - Minimización de función objetivo definida por la suma de los errores cuadráticos entre las recuperaciones deseadas y reales, variando flujo de destilado y razón de reflujo.

## Architecture

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│  React SPA  │────▶│   REST API   │────▶│ PostgreSQL  │
└─────────────┘     │  (Express)   │     └─────────────┘
                    └──────┬───────┘
                           │
                    ┌──────▼───────┐
                    │    Redis     │
                    │   (Cache)    │
                    └──────────────┘
```

## Challenges & Solutions

### Challenge 1: Inventory Sync
**Problem**: Multiple users buying same product simultaneously causing overselling

**Solution**: Implemented optimistic locking with Redis to ensure inventory accuracy during concurrent purchases

### Challenge 2: Payment Processing
**Problem**: Handling payment failures gracefully while maintaining order integrity

**Solution**: Built robust state machine for order processing with automatic retry logic and customer notifications

### Challenge 3: Performance at Scale
**Problem**: Slow page loads during traffic spikes

**Solution**: Implemented multi-layer caching strategy (CDN, Redis, in-memory) and database query optimization

## Results

- **Performance**: 60% faster page load times compared to previous platform
- **Conversion**: 25% increase in conversion rate due to improved UX
- **Uptime**: 99.9% uptime over 6 months in production
- **Scale**: Successfully handled Black Friday with 10k concurrent users
- **Revenue**: Processing over $50k in monthly transactions

## Future Improvements

- [ ] Balances de energía por etapas
- [ ] Diseño estructural de la columna

## Lessons Learned

1. **Start with Performance**: Built with performance in mind from day one rather than optimizing later
2. **Testing Matters**: Comprehensive test suite caught critical bugs before production
3. **Monitor Everything**: Proper logging and monitoring essential for maintaining uptime
4. **User Feedback**: Regular user testing revealed UX issues we wouldn't have found otherwise

---

**Project Status**: ✅ Live in Production  
**GitHub**: [View Source Code](https://github.com/alexjohnson/ecommerce-platform)  
**Demo**: [Try it Live](https://shop-demo.example.com)
