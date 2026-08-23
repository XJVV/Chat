# VitaOS — Bóveda final

VitaOS es un sistema personal de vida construido en Obsidian. Su principio rector es simple: **el sistema debe ser simple**. La bóveda no existe para administrar la vida, sino para capturarla, ejecutarla, observarla y mejorarla.

## Plugins
- Dataview
- Tasks
- Charts View
- Templater

## Configuración inicial
1. Configura `99 Templates` como carpeta de plantillas de Templater.
2. Activa **JavaScript Queries** en Dataview.
3. Mantén los cuatro plugins habilitados.
4. Usa `Home.md` como página inicial.

## Centro de operaciones
- **Home.md:** responde qué importa ahora, qué está pendiente y qué señales merecen atención.
- **00 System/Analytics.md:** responde qué está pasando, cómo cambia y qué relaciones aparecen.
- **00 System/VitaOS.md:** explica el sistema y sus principios.
- **00 System/VitaOS Config.md:** contiene variables centrales como `current_period`.

## Flujo completo
```text
Mundo → Captura → Inbox → Procesamiento → Contexto
→ Acción / Conocimiento / Referencia / Evidencia
→ Resultado → Record → Métrica → Analytics
→ Señal → Review → Decisión → Acción
→ Resultado → Nuevo Record → ...
```

## Estudios
Los Records nuevos deben crearse con `99 Templates/TPL - Study Record Auto.md`, porque hereda automáticamente `current_period` desde `VitaOS Config.md`.

Los Records históricos conservan su período original. Al cambiar de C1 a C2, solo se cambia `current_period`; no se reescribe el historial.

## Retroalimentación
Cuando Home o Analytics muestran una señal que merece investigación:
1. abre Analytics;
2. determina qué muestran realmente los datos;
3. crea una Review con `99 Templates/TPL - Review Cycle.md`;
4. registra la decisión y la próxima acción;
5. ejecuta la acción en su contexto correspondiente;
6. vuelve a medir;
7. registra el resultado y cierra la Review cuando exista suficiente evidencia para decidir el siguiente paso.

Workflow completo: `00 System/Workflows/Workflow - Ciclo de retroalimentacion.md`.

## Regla de fuente única
Los datos se escriben una sola vez en su nota de origen. Home y Analytics los consultan y calculan; no se mantienen números duplicados manualmente.

## Gráficas
Charts View se utiliza cuando una gráfica responde una pregunta real. Las visualizaciones actuales de Analytics cubren:
- horas por semana;
- horas por materia;
- rendimiento por materia;
- evolución del rendimiento;
- dificultad vs. rendimiento;
- dificultad vs. horas.

## Regla final
Si una parte de VitaOS empieza a costar más de administrar que lo que aporta, se simplifica o se elimina.
