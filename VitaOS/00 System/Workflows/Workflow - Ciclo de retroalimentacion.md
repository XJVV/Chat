---
type: workflow
status: active
---
# Workflow — Ciclo de retroalimentación

## Propósito
Convertir observaciones del sistema en decisiones y acciones, y después volver a medir el resultado.

## Flujo
```text
Datos → Analytics → Señal → Review → Decisión → Acción → Resultado → Nuevos datos
  ↑                                                                  │
  └──────────────────────────────────────────────────────────────────┘
```

## 1. Observar
Abrir `Analytics.md` cuando exista una pregunta, una revisión programada o una señal relevante en `Home.md`.

No se busca revisar todo. Se busca responder una pregunta concreta.

## 2. Detectar una señal
Ejemplos:
- rendimiento persistentemente bajo;
- dificultad alta;
- cambio fuerte en horas de estudio;
- tendencia positiva o negativa;
- proyecto estancado;
- una acción que se repite sin producir resultado.

Una señal no es todavía un problema. Es una razón para investigar.

## 3. Crear una Review
Usar `99 Templates/TPL - Review Cycle.md`.

Registrar:
- señal observada;
- qué muestran los datos;
- qué funcionó;
- qué no funcionó;
- decisión;
- próxima acción;
- fecha de seguimiento.

## 4. Decidir
La decisión debe ser pequeña, concreta y comprobable.

Mal:
> Estudiar más.

Bien:
> Aumentar Álgebra de 3 h/semana a 5 h/semana durante las próximas 2 semanas y observar rendimiento.

## 5. Actuar
La decisión se convierte en una tarea o conjunto de tareas en el proyecto o contexto correspondiente.

La acción vive donde se ejecuta. La Review solamente conserva la decisión y el motivo.

## 6. Medir
Registrar los nuevos resultados normalmente. No crear datos especiales para justificar la decisión.

## 7. Cerrar
En la fecha de seguimiento:
1. revisar Analytics;
2. comprobar el resultado;
3. registrar qué ocurrió en la Review;
4. decidir si mantener, cambiar o eliminar el ajuste;
5. cambiar `status: open` a `status: closed`.

## Regla
Una Review no se cierra porque la tarea esté marcada como hecha. Se cierra cuando existe retroalimentación suficiente para decidir el siguiente paso.

## Principio de simplicidad
Si una revisión no produce una decisión o aprendizaje útil, no necesita convertirse en un ritual permanente.
