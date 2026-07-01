---
title: "Destilación multicomponente ideal"
date: 2026-06-18
summary: "Modelamiento de una columna de destilación para separar componentes orgánicos ligeros. Basado en balances de masa y restricciones termodinámicas. Incluye diseño preliminar mediante correlaciones y método _short-cut_"
tags: 
  - Modelamiento
  - Oil & Gas
tech_stack:
  - Python
  - Modelamiento
  - Procesos
  - Oil & Gas
  - Termodinámica
featured: true
status: "Completado"
role: "Desarrollador"
duration: "1 semana"
team_size: 1
highlights:
  - "Métodos shortcut (FUG) y riguroso MESH implementados"
math: true
---

Se elige el siguiente problema de modelamiento para resolver en Python.

## Problema

Una corriente de líquido y vapor saturados (q = 0.30) a una presión de 405.4 KPa se alimenta a una torre de destilación en un flujo de 1000 mol/h. La composición global de la alimentación es n-butano ($z_{but}$ = 0.35), n-pentano ($z_{pent}$ = 0.30), n-hexano ($z_{hex}$ = 0.20) y n-heptano ($z_{hept}$ = 0.15). La corriente es destilada de manera de recuperar el 97% del n-pentano en el destilado y el 85% del n-hexano en el producto de cola. Calcule lo siguiente:

+ Flujo y composición de los productos y temperaturas del tope y la base de la columna.
+ Número de etapas a reflujo total y distribución de otros componentes en los productos.
+ Razón mínima de reflujo, número de etapas a 1.2 $R_{mín}$ y localización del plato de alimentación.

## Resolución

### Método _short cut_ (aproximación de diseño)
- **Elección de componentes claves** - Resolución de balances de masa e imposición de recuperaciones respecto a clave liviana (n-pentano) y pesada (n-heptano).
- **Temperaturas del tope y cola** - Estimación mediante punto de burbuja utilizando librería _thermo.Chemicals_ y _scipy_.
- **Método FUG** - Cálculo de etapas mínimas por método Fenske, reflujo mínimo por Underwood y número de etapas reales por Gilliland, resolviendo iterativamente con _fsolve_.
- **Plato de alimentación** - Resolución de ecuación empírica de Kirkbride.

### Método riguroso MESH
- **Definición de variables** - Cálculo de flujos y razón de _boil up_ según McCabe-Thiele.
- **Balance por etapas** - Definición de problema lineal $Ax= b$ con matriz tridiagonal con coeficientes variables en función de la temperatura por etapa.
- **Resolución de balances** - Resolución con iteración de punto fijo sobre el vector de temperaturas para encontrar fracciones molares en los flujos de líquido.
- **Problema de optimización** - Minimización de la suma de los errores cuadráticos entre las recuperaciones deseadas y reales, variando flujo de destilado y razón de reflujo. Para cada iteración del optimizador, se actualiza el gradiente de temperaturas iterativamente en un _inner-loop_.

## Arquitectura
---

---
## Desafíos & Soluciones

### Desafío 1: Restricciones lógicas a variables internas
**Problema**: Para cada etapa, debe cumplirse que la suma de las fracciones molares sea igual a uno y que el vector de temperaturas sea un vector creciente desde el tope hacia la cola.

**Solución**: Las fracciones molares son sumadas y normalizadas en cada iteración, por lo que la convergencia del método de punto fijo asegura la corrección. Además, se verifica la diferencia de temperaturas por etapas luego de terminada la resolución iterativa de los balances.

### Desafío 2: Adivinanzas de temperaturas entre pasos del optimizador
**Problema**: Para cada iteración del optimizador, comenzar de una adivinanza inicial de un vector de temperaturas equiespaciado y fijo ralentiza la convergencia.

**Solución**: Se implementa Programación Orientada al Objeto para guardar vectores de temperatura como resultados parciales y entregarlos como adivinanza inicial a la función objetivo. La temperatura es guardada en los Atributos y la función en la Clase del Objeto.

### Desafío 3: Elección de método de optimización
**Problema**: En _minimize_, el método de gradiente SLSQP con restricciones lineales no asegura la convergencia. De la misma forma, Powell con restricciones de rango tampoco converge a una solución.

**Solución**: Se selecciona el optimizador Nelder-Mead sin restricciones sobre las variables y se observa la variación entre pasos del optimizador, cumpliéndose la asignación de valores lógicos (positivos y en rango acotado).

## Resultados

- **Diseño**: Se consigue un diseño preliminar con el método _short cut_ de una columna de 16 platos con alimentación en el noveno. El método riguroso corrige flujos globales y calcula composiciones y temperaturas por etapas, obteniéndose un gradiente desde el tope a 72°C hasta el fondo a 131°C.
- **Requerimientos**: Se consigue alcanzar el valor óptimo y ajustar las recuperaciones deseadas bajo la tolerancia _default_. La función objetivo se minimiza al orden e-10. El costo computacional puede reducirse relajando la tolerancia.
- **Desempeño**: La rutina de optimización encuentra el valor óptimo en un periodo aproximado de 12 minutos en un total de 70 iteraciones del optimizador.

## Mejoras futuras

- [ ] Balances de energía por etapas.
- [ ] Diseño estructural de la columna.
- [ ] Comparación con simualdor de procesos. 

## Lecciones aprendidas

1. **Testear métodos de optimización**: los métodos de optimización son sugeridos en base a la naturaleza del problema; sin embargo, debe asegurarse la convergencia y replantearse el problema de optimización en caso de no aproximarse al óptimo en un tiempo razonable.
2. **Programación dinámica**: mejorar rapidez de convergencia manteniendo resultados parciales en iteraciones proximales.

---

**Estado del proyecto**: ✅ Completado  
**GitHub**: [Código Fuente]()
