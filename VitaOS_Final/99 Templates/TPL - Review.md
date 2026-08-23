<%*
const date = tp.date.now("YYYY-MM-DD");
const signal = await tp.system.prompt("¿Qué señal o problema estás revisando?");
const decision = await tp.system.prompt("¿Qué decisión tomarás?");
const nextAction = await tp.system.prompt("¿Cuál es la próxima acción?");
const followUp = await tp.system.prompt("¿Cuándo revisarás el resultado? (YYYY-MM-DD)");
await tp.file.rename(`Review - ${date}`);
%>---
type: review
date: <% date %>
life_area: Sistema
status: open
signal: "<% signal %>"
decision: "<% decision %>"
next_action: "<% nextAction %>"
follow_up: <% followUp %>
---
# 🔄 Review — <% date %>

## Señal observada
<% signal %>

## Qué funcionó

## Qué no funcionó

## Qué muestran los datos

## Decisión
<% decision %>

## Próxima acción
- [ ] <% nextAction %>

## Fecha de seguimiento
<% followUp %>

## Resultado del seguimiento

## Cierre
Cuando la acción haya sido ejecutada y el resultado observado, cambia `status` de `open` a `closed` y registra qué ocurrió. No se cierra una revisión por completar la tarea; se cierra cuando existe retroalimentación suficiente para decidir el siguiente paso.
