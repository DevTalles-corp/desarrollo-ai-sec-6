---
name: error-handling
description: Usala cuando una tarea crea o cambia una excepción, el handler global o la respuesta de un error HTTP.
---

# Manejo de errores

Explica cómo se crean las excepciones de una feature y cómo las responde el handler global. Desarrolla la sección Errores de `docs/constitution.md`.

## Cuándo aplica

- Crear la excepción de una feature. Ejemplo: `EquipmentNotFoundException`.
- Lanzar una excepción desde un service. Ejemplo: `EquipmentService` cuando no encuentra un equipo.
- Agregar o cambiar un método de `GlobalExceptionHandler`.

## Reglas

## Qué evitar
