<%*
const title=await tp.system.prompt("¿Qué apareció?");
await tp.file.rename(`Inbox - ${title}`);
%>
---
type: inbox
status: raw
captured: <% tp.date.now("YYYY-MM-DD") %>
---
# <% title %>
## Entrada
## Contexto
## Procesamiento
