---
title: "Pasteurizador batch"
date: 2026-07-28
summary: "Diseño y simulación de un pasteurizador batch en estanque agitado con chaqueta para productos lácteos"
tags: 
  - Diseño
  - Simulación
  - Alimentos
tech_stack:
  - MATLAB
  - Excel
  - Diseño
  - Procesos
  - Alimentos
  - Transferencia de calor
featured: true
status: "Completado"
role: "Desarrollador"
duration: "1 semana"
team_size: 1
highlights:
  - "Transferencia de calor transiente"
math: true
---

El siguiente problema corresponde al enunciado de un proyecto que preparé para que mis alumnos del curso IQ4313 Operaciones de Transferencia de Calor.

## Problema

La empresa lechera _SitCo_ produce leche y derivados lácteos. Según los requerimientos normativos del proceso, se debe pasteurizar los lácteos previo a su distribución y conversión en otros productos para asegurar la inocuidad de los alimentos. En base a lo anterior, se desea evaluar la pasteurización de un volumen de 500 litros de leche descremada mediante el método HTST por lotes y programar el proceso dentro de la Carta Gantt de operación de la planta.

El pasteurizador corresponde a un estanque agitado de acero inoxidable con una chaqueta intercambiadora externa y un agitador tipo _propeller_ que gira a una velocidad tangencial de 300 m/min y entrega una potencia de 200 W. La chaqueta opera a 0,3 MPa y permite la circulación de un flujo de agua saturada durante la etapa de calentamiento y pasteurización. Luego de estos periodos, el agitador disminuye su velocidad a 60 m/min otorgando una potencia despreciable mientras un flujo de refrigerante 134a ingresa a unos -30°C por la misma chaqueta hasta enfriar el líquido a 4°C.

Se les solicita identificar los mecanismos de transferencia presentes, plantear los balances requeridos, calcular el requerimiento de agua caliente y refrigerante 134a, identificar el área de intercambio y reportar el tiempo total de la operación por batch de leche pasteurizada.

## Resolución

- **Definición de criterios de diseño** - Establecer condiciones de operación para el método HTST y búsqueda propiedades termodinámicas para los fluidos dentro del estanque y por la chaqueta intercambiadora. 
- **Imposiciones de geometría** - Imponer diseño geométrico del estanque en base a requerimiento del volumen. Se decide modelar un estanque cilíndrico estándar de 1.1*volumen de leche con pared de 5 mm y chaqueta soldada a media caña con 10 vueltas del tubo.
- **Balances de energía por etapas** - Se calcula el requerimiento másico de agua caliente y refrigerante en base a calor requerido, con salidas a temperaturas mínima y máxima de 87°C y 0°C, respectivamente. Se impone 97% de eficiencia térmica. 
- **Coeficiente de transferencia y correlaciones** - Se modela resistencia total considerando convección interna en el estanque, conducción de la pared del estanque y convección interna por el tubo helicoidal de la chaqueta. Se utiliza la correlación Gnielinski con corrección para tubos helicoidales y la correlación del número de potencia para el estanque agitado con _propeller_. 
- **Ecuación de diseño y modelamiento** - Las ecuacioines de diseño y modelamiento por periodos corresponden a:
    - Calentamiento: $$ m_w Cp_w dT_h = -U_h (T_h - T) dA $$
      $$ m Cp \frac{dT}{dt} = \eta U_h A \Delta T_{ml} + Po$$
   
    - Enfriamiento: $$m_r Cp_r dT_c = U_c (T - T_c) dA $$
      $$ m Cp \frac{dT}{dt} = -\frac{U_c A}{\eta} \Delta T_{ml}$$

  La solución al sistema de ecuaciones se describe mediante solución analítica resuelta en hoja de cálculo en Excel y simulación numérica de las EDO's en MATLAB. 

## Resultados
Las soluciones para los tiempos de operación y las temperaturas de salida de los fluidos en la chaqueta son: 
- Calentamiento: $$ t_{heating} = \frac{m Cp}{\eta m_w Cp_w(1- e^{-\frac{U_h A}{m_wCp_w}})} \ln \left(\frac{T_h + \tfrac{Po}{K} - T_0}{T_h + \tfrac{Po}{K} - T_{HTST}}\right) $$ donde $K= \eta m_wCp_w (1 - e^{-\frac{U_h A}{m_wCp_w}})$
  $$ T_{ho}(t) = T (t) + (T_h - T(t))\cdot e^{-\frac{U_h A}{m_wCp_w}}$$
- Enfriamiento:
      $$ t_{cooling} = \frac{\eta m Cp}{m_r Cp_r(1-e^{-\frac{U_c A}{m_rCp_r}})} \ln \left(\frac{T_{HTST} - T_c}{T_0 - T_c}\right) $$
  $$ T_{co}(t) = T (t) - (T(t)- T_c)\cdot e^{-\frac{U_c A}{m_cCp_c}}$$

Los resultados de la simulación temporal de los perfiles de temperatura en MATLAB se visualizan en el siguiente gráfico:

## Mejoras a futuro
- [ ] Modelamiento de pasteurización con vapor saturado e inetrcambio de calor latente. 
- [ ] Sistema de control de temperatura que varíe apertura de válvula para flujo en chaqueta. 

## Lecciones aprendidas

1. **Formas de resolución**: Recuerdo que cuando diseñé este ejercicio, encontré una solución analítica aproximada al problema sin incluir la potencia de agitación, no obstante, mis alumnos optaron por la solución numérica para describir la EDO no homogénea. Ahora corregí la expresión, encontrando una expresión más precisa pero más complicada en cuanto a un cálculo de servilleta.
2. **Simplificaciones razonables**: Mis alumnos de cuarto año decidieron simplificar el modelo considerando una temperatura promedio aritmética asumiendo una temperatura promedio constante en el líquido de la chaqueta. Considerando que es su primer curso con diseño de equipos en estado estacionario y no tienen nociones de dinámica de procesos, me pareció un supuesto razonable para abordar la variación de la temperatura en la chaqueta.  
---

**Estado del proyecto**: ✅ Completado  
**GitHub**: [Código Fuente]()
