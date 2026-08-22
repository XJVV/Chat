<%*
const date=tp.date.now("YYYY-MM-DD");
await tp.file.rename(`Review - ${date}`);
%>
---
type: review
date: <% date %>
life_area: Sistema
---
# Revisión — <% date %>
## Qué funcionó
## Qué no funcionó
## Qué muestran los datos
## Qué debo cambiar
## Próxima prueba
