---
title: "Destilación multicomponente ideal"
date: 2026-06-18
summary: "Modelamiento de un columna de destilación para separar componentes orgánicos ligeros. Basado en balances de masa y restricciones termodinámicas. Incluye diseño preliminar mediante correlaciones y método _shortcut_"
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
role: "Lead Developer"
duration: "1 semana"
team_size: 1
highlights:
  - "Handles 10k+ concurrent users"
math= true
---

Se elige el siguiente problema de modelamiento para resolver en Python. 

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

## Arquitectura


## Desafíos & Soluciones

### Desafío 1: Selección de variables a optimizar
**Problema**: El flujo de destilado $D$, la razón de reflujo $R$ y el perfil de temperaturas $(T_1 \dots T_{N})$ definen conjuntamente los coeficientes para la resolución de los balances internos de la columna.

**Solución**: Se nota que las variables de flujo y razón de reflujo definen el balance global de la torre, mientras que el perfil de temperaturas es dependiente de las recuperaciones en los flujos de salida. Por ello, el destilado y el reflujo se optimizan mientras que las temperaturas por etapas se resuelven ietrativamente en un _inner-loop_ en cada paso del optimizador.

### Desafío 2: Restricciones lógicas a variables internas
**Problema**: Para cada etapa, debe cumplirse que la suma de

**Solución**: 

### Desafío 3: Adivinanzas de temperaturas entre pasos del optimizador
**Problema**: Para cada iteración del optimizar, comenzar de una adivinanza inicial de un vector de temperaturas equiespaciado y fijo ralentiza la convergencia. 

**Solución**: Se implmenta un Programación Orientada al Objeto para guardar vectores de temperatura como resultados parical y entregarlos como adivinanza inicial a la función objetivo. La temperatura es guardado en los Atributos y la función en la Clase del Objeto. 

### Desafío 4: Elección de método de optimización
**Problema**: Métodos de gradiente como 

**Solución**: Se selecciona

## Resultados

- **Diseño**: Se consigue un diseño preliminar con el método _short cut_ de una columna de 16 platos con alimentación en el noveno. Método riguroso corrige flujos globales y calcula composiciones y temperaturas por etapas, obteniéndsoe un gradiente desde el tope a  hasta el fondo a 
- **Requerimientos**: Se consigue alcanzar 
- **Desempeño**: Rutina de optimización encuentra valor óptimo en un periodo aproximado de 12 minutos. 

## Future Improvements

- [ ] Balances de energía por etapas
- [ ] Diseño estructural de la columna

## Lecciones aprendidas

1. **Testear métodos de optimización**: 
2. **Programación dinámica**: 

---

**Estado del proyecto**: ✅ Completado
**GitHub**: [Código Fuente]()  
