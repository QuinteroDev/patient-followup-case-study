# Estudio de caso: plataforma de seguimiento de pacientes digestivos

> Proyecto real en producción para un cliente bajo NDA. Aquí no hay código, datos ni nombres; solo el problema, las decisiones y cómo está construido.

## Contexto

Plataforma web para una consulta médica especializada en reflujo y gastritis. Tiene dos caras: un panel para el equipo clínico y un área para el paciente. La he desarrollado y mantenido yo desde finales de 2024.

## Qué hace

- **Área del paciente:** cuestionarios diagnósticos validados (GERDQ, RSI, HADS), consentimiento informado firmado en PDF, plan de tratamiento y contenido que se desbloquea mes a mes.
- **Panel del equipo:** pacientes, programas de contenido, protocolos, suplementos, recetas, captación comercial y chat con cada paciente.
- **Avisos programados:** 8 tareas diarias con Celery Beat que desbloquean contenido según la fecha de cada paciente, controlan pagos y avisan de cuestionarios pendientes y de pacientes inactivos.

## Trabajo destacado

- **Auditoría de seguridad.** Cerré un acceso a datos de otros pacientes cambiando el identificador en la URL (IDOR), un salto del login en el alta, un endpoint sin control de permisos y un XSS en las notificaciones. Reforcé HTTPS en producción.
- **Actualización de Django 4.2 a 5.2 LTS** con tests de regresión para lo que se rompió.
- **Integridad de datos en flujos clínicos.** Eliminé envíos duplicados en chat, cuestionarios y ajustes del plan con restricciones de unicidad y transacciones.
- **Recálculo masivo de puntuaciones clínicas históricas** con actualización en bloque y sin disparar avisos falsos a pacientes.

## Stack

Python · Django (plantillas en servidor) · PostgreSQL · Celery + Celery Beat · Redis · WeasyPrint · Resend · Bootstrap · JavaScript · pytest (~140 tests)
