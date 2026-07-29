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

La empresa lechera SitCo produce leche y derivados lácteos. Según los requerimientos normativos del proceso, se debe pasteurizar los lácteos previo a su distribución y conversión en otros productos para asegurar la inocuidad de los alimentos. En base a lo anterior, se desea evaluar la pasteurización de un volumen de 500 litros de leche descremada mediante el método HTST por lotes y programar el proceso dentro de la Carta Gantt de operación de la planta.

El pasteurizador corresponde a un estanque agitado de acero inoxidable con una chaqueta intercambiadora externa y un agitador tipo _propeller_que gira a una velocidad tangencial de 300 m/min y entrega una potencia de 200 W. La chaqueta opera a 0,3 MPa y permite la circulación de un flujo de agua saturada durante la etapa de calentamiento y pasteurización. Luego de estos periodos, el agitador disminuye su velocidad a 60 m/min otorgando una potencia despreciable mientras un flujo de refrigerante 134a ingresa a unos -35°C por la misma chaqueta hasta enfriar el líquido a 4°C.

Se les solicita identificar los mecanismos de transferencia presentes, plantear los balances requeridos, calcular el requerimiento de agua caliente y refrigerante 134a, identificar el área de intercambio y reportar el tiempo total de la operación por batch de leche pasteurizada.

## Resolución

- **Definición de criterios de diseño** - Establecer condiciones de operación para el método HTST y búsqueda propiedades termodinámicas para los fluidos dentro del estanque y por la chaqueta intercambiadora. 
- **Supuestos de geometría del equipo** - Imponer diseño geométrico del estanque en base a requerimiento del volumen. Se decide modelar un estanque cliíndrico estándar de 1.1*volumen de leche con chaqueta soldada a media caña con 15 vueltas del tubo.
- **Balances de energía por etapas** - Se calcula el requerimiento másico de agua caliente y refrigerante en base a calor requerido. Se impone 90% de eficiencia térmica. 
- **Coeficiente de transferencia y correlaciones** - Se modela resistencia total considerando convección interna en el estanque, conducción de la pared del estanque y convección interna por el tubo helicoidal de la chaqueta. Se utiliza la correlación Gnielinski para el tubo de la chaqueta y ... para el estanque agitado con _propeller_. 
- **Ecuación de diseño y modelamiento** - La ecuación de diseño por periodos corresponde a:
    - Calentamiento: $$ m_w Cp_w dT_h = -U_h (T_h - T) dA $$
      $$ m Cp \frac{dT}{dt} = U_h A \Delta T_{ml} + Po$$
   
    - Enfriamiento: $$m_r Cp_r dT_c = U_c (T - T_c) dA $$
      $$ m Cp \frac{dT}{dt} = -U_c A \Delta T_{ml}$$
    - Soluciones: $$ t_{heating} = \frac{m Cp \cdot e^{\frac{U_h A}{m_wCp_w}}}{m_w Cp_w(e^{\frac{U_h A}{m_wCp_w}}-1)} \ln \left(\frac{T_h + \tfrac{Po}{K} - T_0}{T_h + \tfrac{Po}{K} - T_{HTST}}\right) $$ donde $K= m_wCp_w (1 - e^{-\frac{U_h A}{m_wCp_w}})$ 
      $$ t_{cooling} = \frac{m Cp \cdot e^{\frac{U_c A}{m_rCp_r}}}{m_r Cp_r(e^{\frac{U_c A}{m_rCp_r}} -1)} \ln \left(\frac{T_{HTST} - T_c}{T_0 - T_c}\right) $$
 
## Desafíos & Soluciones

### Desafío 1: 
**Problema**: 

## Resultados


## Mejoras a futuro
[] Sistema de control de temperatura que varíe apertura de válvula para flujo en chaqueta


## Lecciones aprendidas

1. ** **: 
2. ** **: 
---

**Estado del proyecto**: ✅ Completado  
**GitHub**: [Código Fuente](https://github.com/MatiMoraga/proyectos-privados/blob/2dbba4a1a7337c857aff7bbf0f7d1ee107f4433c/multicomponent_distillation.ipynb)
