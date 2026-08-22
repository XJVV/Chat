<%*  
const date = tp.date.now("YYYY-MM-DD");

const subject = await tp.system.prompt("¿Qué materia?");

const hours = await tp.system.prompt("¿Cuántas horas?");

const difficulty = await tp.system.prompt("Dificultad 1-10");

const performance = await tp.system.prompt("Rendimiento 0-100");

// ─────────────────────────────  
// OBTENER CUATRIMESTRE ACTUAL  
// ─────────────────────────────

const configPath = "00 System/VitaOS Config.md";

const configFile = app.vault.getAbstractFileByPath(configPath);

if (!configFile) {  
new Notice("⚠️ No se encontró VitaOS Config.md");  
throw new Error("No se encontró VitaOS Config.md");  
}

const configContent = await app.vault.read(configFile);

const periodMatch = configContent.match(  
/^current_period:\s*(.+)$/m  
);

if (!periodMatch) {  
new Notice("⚠️ No se encontró current_period en VitaOS Config.md");  
throw new Error("No se encontró current_period");  
}

const period = periodMatch[1].trim();

// ─────────────────────────────  
// RENOMBRAR RECORD  
// ─────────────────────────────

await tp.file.rename(  
`Record - Estudio ${subject} ${date}`  
);

%>---

type: study-record

date: <% date %>

study: Ingeniería en Sistemas Computacionales

period: <% period %>

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