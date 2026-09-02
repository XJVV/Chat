<%*
const date = tp.date.now("YYYY-MM-DD");
const subject = await tp.system.prompt("¿Qué materia?");

const configPath = "00 System/VitaOS Config.md";
const configFile = app.vault.getAbstractFileByPath(configPath);
let period = "";
if (configFile) {
    const config = await app.vault.read(configFile);
    const match = config.match(/^current_period:\s*(.+)$/m);
    period = match ? match[1].trim() : "";
}

await tp.file.rename(`Clase - ${subject} ${date}`);
%>---
type: class-note
date: <% date %>
study: Ingeniería en Sistemas Computacionales
period: <% period %>
subject: <% subject %>
life_area: Educación
---
# Clase — <% subject %> — <% date %>

## Tema

## Contenido de la clase


## Ejemplos


## Conceptos clave


## Dudas

- [ ] 

## Pendientes / tareas

- [ ] 

## Observaciones

