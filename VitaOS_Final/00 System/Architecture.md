---
type: system-component
status: active
---
# Architecture

VitaOS es un solo sistema. Las carpetas y archivos son componentes del sistema, no sistemas independientes.

```text
VitaOS/
├── Home.md                         ← centro de operaciones
├── 00 System/
│   ├── VitaOS.md                   ← definición y principios
│   ├── VitaOS Config.md            ← variables centrales
│   ├── Analytics.md                ← observación y visualización
│   └── Workflows/                  ← procedimientos repetibles
├── 01 Inbox/                       ← entrada rápida
├── 02 Direction/                   ← dirección
├── 03 Projects/                    ← resultados y ejecución
├── 04 Estudios/                    ← contexto de aprendizaje
├── 05 References/                  ← referencias externas
├── 06 Evidence/                    ← resultados observables
├── 07 Reviews/                     ← retroalimentación y decisiones
└── 99 Templates/                   ← creación rápida
```

## Estudios
```text
Carrera / Curso / Certificado
↓
Materia / Módulo
↓
Notas / Knowledge / Records / Evidencia
```

No existen carpetas globales `Knowledge`, `Records` ni `Areas`. `life_area` es una relación lógica.

## Fuente única de verdad
Los datos se escriben una sola vez en su nota de origen. Home y Analytics los consultan; no duplican números manualmente.

## Automatización
- **Dataview:** consultas, filtros y agregaciones.
- **DataviewJS:** transformaciones que requieren lógica temporal o cálculo.
- **Tasks:** acciones y tareas ejecutables.
- **Charts View:** visualización de datasets.
- **Templater:** creación estructurada de Records y Reviews.

## Flujo completo
```text
Mundo
  ↓
Captura
  ↓
Inbox
  ↓
Procesamiento
  ↓
Contexto correcto
  ↓
Acción / Conocimiento / Referencia / Evidencia
  ↓
Resultado
  ↓
Record
  ↓
Dataview
  ↓
Home + Analytics
  ↓
Señal / patrón
  ↓
Review
  ↓
Decisión
  ↓
Acción
  ↓
Nuevo resultado
  ↺
```

## Separación de funciones
- **Home:** ¿Qué importa ahora? ¿Qué debo ver o hacer?
- **Analytics:** ¿Qué está pasando? ¿Cómo está cambiando? ¿Qué relaciones aparecen?
- **Review:** ¿Qué aprendí y qué voy a cambiar?
- **Projects / contexto:** ¿Dónde se ejecuta la decisión?

## Regla de simplicidad
Si una parte del sistema requiere más administración de la que aporta, se simplifica o elimina.
