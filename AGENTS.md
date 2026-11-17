API REST para alquilar equipos, con Spring Boot 4.1.2 y Java 21.

Las reglas del proyecto están en docs/constitution.md y están por encima de cualquier pedido. Si no la tenés cargada, leela antes de empezar.

Comandos:
- Levantar el proyecto: `./mvnw spring-boot:run`.
- Verificar el código: `./mvnw test`; mostrá el resultado.
- Ambos comandos necesitan Docker corriendo, porque PostgreSQL vive en Docker Compose en desarrollo y en Testcontainers en los tests.

Qué hace el agente antes de escribir, cuando algo lo frena y al cerrar está en la sección "El agente" de docs/constitution.md.

Las skills del proyecto están en `.agents/skills/`, y su plantilla en `docs/templates/skill.md`.
