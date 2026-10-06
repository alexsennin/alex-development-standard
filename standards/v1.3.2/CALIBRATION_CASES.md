# Casos iniciales de calibración v1.3.2

Estos casos son ejemplos de referencia, no una cuarta taxonomía. Se ampliarán con evidencia de proyectos reales.

## Caso 1 — Texto/UI trivial
Solicitud: «Cambia Guardad por Guardar».
- Modo: PATCH
- Nivel: 1
- Capacidad: FOCUSED
- Plan visible: no
- Verificación: focal/visual
- Documentación: sólo si cambió una verdad persistente

## Caso 2 — Bug funcional con causa conocida
Solicitud: «El botón permite doble submit; bloquea mientras envía».
- Modo: FEATURE o PATCH según alcance local
- Nivel: 2
- Capacidad: FOCUSED/ADVANCED
- Plan: interno breve
- Verificación: doble clic produce una sola solicitud

## Caso 3 — Bug con causa desconocida
Solicitud: «A veces se duplican usuarios».
- Modo inicial: FEATURE
- Nivel inicial: 2, sujeto a reclasificación
- Capacidad: EXPERT para diagnóstico
- Si se confirma persistencia/idempotencia/contrato: escalar a SYSTEM/Nivel 3; después delegar implementación por Execution Packets

## Caso 4 — Auth/DB/RLS
Solicitud: «Agrega acceso por organización y cambia políticas RLS».
- Señal de escalamiento forzado: sí
- Modo: SYSTEM
- Nivel: 3 normalmente; 4 si toca permisos críticos/datos reales/Producción difícil de revertir
- Capacidad: EXPERT para diseño, ADVANCED/FOCUSED para unidades concretas
- RELEASE separado y explícito

## Caso 5 — Operación crítica en Producción
Solicitud: «Migra datos reales y elimina la estructura anterior».
- Modo: SYSTEM para preparar; RELEASE para aplicar
- Nivel: 4
- Capacidad: EXPERT/FRONTIER según dificultad
- Requisitos: recuperación definida, revisión EXPERT independiente en contexto separado, autorización explícita de Producción y verificación posterior