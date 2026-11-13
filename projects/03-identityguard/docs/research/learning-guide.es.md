# Guía de aprendizaje — Fase 0

**Estado:** en progreso; no avanzar a Fase 1 sin aprobación del propietario.

## Conceptos

- **IAM (Identity & Access Management):** controlar quién obtiene acceso a qué sistemas y con qué mecanismos.
- **IGA (Identity Governance & Administration):** justificar, otorgar, revisar, certificar y revocar acceso con responsabilidad y evidencia.
- **JML (Joiner–Mover–Leaver):** altas, cambios de cargo y salidas de personas.
- **RBAC (Role-Based Access Control):** los roles permiten asignar grupos definidos de permisos.
- **SoD (Segregation of Duties):** evitar combinaciones de permisos incompatibles en procesos sensibles.
- **Reconciliation:** comparar el acceso esperado con el estado real de un sistema destino.

## Ejercicios guiados (sin programación)

1. **Leaver:** una persona terminó contrato hace 5 días pero su cuenta financiera sigue activa. Indica síntoma, causa posible, riesgo, control, propietario y evidencia.
2. **Mover:** una persona cambia de RR. HH. a Ventas pero conserva permisos sobre expedientes laborales. Indica cuál acceso debe retirarse y cómo comprobarlo.
3. **Aprobación:** un usuario obtiene permiso para aprobar pagos sin registro de autorización. Explica qué documento, flujo y evidencia necesitarías.
4. **Trazabilidad:** selecciona IAM-001 a IAM-004 y explica por qué cada prueba verifica un problema de negocio, no solo una función técnica.

## Comprobación

Responde con tus propias palabras:

1. ¿En qué se diferencia autenticar a alguien de gobernar sus permisos?
2. ¿Por qué una baja exitosa debe comprobarse en la aplicación destino y no solo en la base IAM?
3. ¿Por qué no debemos llamar “resultado empresarial” a una métrica generada con datos sintéticos?

## Preguntas de entrevista (English)

- "How do you handle an employee termination in an identity governance workflow?"
- "What is the difference between an identity, an account, a role, and an entitlement?"
- "How would you prove that access was revoked?"

**Respuesta honesta esperada:** explicar el diseño y el laboratorio. Nunca atribuir experiencia a RSM ni a una implementación SailPoint en producción.

## Criterios de cierre de Fase 0

- [ ] Comprendo la investigación y sus límites.
- [ ] Puedo describir el problema IAM que resolveremos.
- [ ] Revisé la trazabilidad IAM-001–IAM-004.
- [ ] Aprobé o corregí el alcance del MVP.
- [ ] Completé los ejercicios y recibí retroalimentación.
- [ ] Confirmé explícitamente el paso a Fase 1.
