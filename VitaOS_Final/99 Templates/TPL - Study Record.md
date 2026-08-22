<%*
const date=tp.date.now("YYYY-MM-DD");
const subject=await tp.system.prompt("¿Qué materia?");
const hours=await tp.system.prompt("¿Cuántas horas?");
const difficulty=await tp.system.prompt("Dificultad 1-10");
const performance=await tp.system.prompt("Rendimiento 0-100");
await tp.file.rename(`Record - Estudio ${subject} ${date}`);
%>---
type: study-record
date: <% date %>
study: Ingeniería en Sistemas Computacionales
subject: <% subject %>
hours: <% hours %>
difficulty: <% difficulty %>
performance: <% performance %>
life_area: Educación
---
# Record — Estudio <% subject %> — <% date %>
## Actividad
## Resultado
## Qué entendí
## Qué no entendí
## Siguiente paso
