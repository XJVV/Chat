<%*
const title=await tp.system.prompt("¿Qué aprendiste?");
await tp.file.rename(`Knowledge - ${title}`);
%>
---
type: knowledge
created: <% tp.date.now("YYYY-MM-DD") %>
study:
subject:
life_area:
confidence:
---
# <% title %>
## Idea central
## En mis palabras
## Aplicación
## Qué todavía no entiendo
## Relacionado
## Referencias
