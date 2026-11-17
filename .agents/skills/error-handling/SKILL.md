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

### La excepción de una feature vive en su subpaquete `exception` y extiende `NotFoundException` o `BusinessRuleException`

Crear la clase en el subpaquete `exception` de la feature, extendiendo la base que corresponda al código HTTP. Ejemplo:

```java
package com.devtalles.rental.catalog.exception;

import com.devtalles.rental.shared.error.NotFoundException;

public class EquipmentNotFoundException extends NotFoundException {
    public EquipmentNotFoundException(Long id) {
        super("No existe el equipo con id " + id);
    }
}
```

**Cómo se verifica:** ninguno todavía.

### La excepción arma su mensaje en castellano en el constructor, a partir del dato del caso

El constructor recibe los datos necesarios y construye el mensaje que verá el cliente. Vale para `NotFoundException` y `BusinessRuleException`. Ejemplos:

```java
public class EquipmentNotFoundException extends NotFoundException {
    public EquipmentNotFoundException(Long id) {
        super("No existe el equipo con id " + id);
    }
}

public class EquipmentAlreadyRentedException extends BusinessRuleException {
    public EquipmentAlreadyRentedException(Long id) {
        super("El equipo " + id + " ya está alquilado");
    }
}
```

**Cómo se verifica:** el test que pide el equipo 99 y espera 404 con `"detail": "No existe el equipo con id 99"`.

### El service lanza la excepción y el controller no la atrapa

El service es el responsable de detectar el error de negocio y lanzar la excepción correspondiente. El controller nunca usa `try/catch`. Ejemplo:

```java
public EquipmentResponse findEquipment(Long id) {
    return equipmentRepository.findById(id)
        .map(equipmentMapper::toResponse)
        .orElseThrow(() -> new EquipmentNotFoundException(id));
}
```

**Cómo se verifica:** el mismo test del 404.

### Una excepción nueva no suma métodos a `GlobalExceptionHandler`

El handler global responde por la excepción base: `NotFoundException` con 404 y `BusinessRuleException` con 409. No se agrega un método por cada excepción concreta. Ejemplo: no se crea un `handleEquipmentNotFoundException` en `GlobalExceptionHandler`; basta con el método para `NotFoundException`.

**Cómo se verifica:** ninguno todavía.

## Qué evitar
