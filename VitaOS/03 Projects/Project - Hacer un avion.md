---
type: project
status: active
priority: high
life_area: Educación
---
# Hacer un avión

## Resultado esperado

Poder diseñar un avión desde los requisitos iniciales hasta un modelo capaz de ser simulado en SimScale, comprendiendo las decisiones de aerodinámica, propulsión, estabilidad, estructura y geometría que forman parte del diseño.

El objetivo final es desarrollar un primer avión funcional y utilizar las simulaciones y pruebas para iterar sobre el diseño.

> **Nota bibliográfica:** *Aerodinámica Básica* (Meseguer y Sanz Andrés) es un libro exclusivamente de aerodinámica. Cubre las Fases 1–4 y parte de la Fase 16. Las Fases 5 y 7 (propulsión y actuaciones) requieren bibliografía complementaria (Franchini o Anderson, según preferencia).

---

# Fases

## Fase 0 — Introducción al avión

### Objetivo

Comprender qué es una aeronave, cuáles son sus partes principales y qué función cumple cada una.

### Conceptos

- [[Knowledge - Qué es un avión]]
- [[Knowledge - Qué es un UAV]]
- [[Knowledge - Qué es un ala]]
- [[Knowledge - Qué es un perfil aerodinámico]]
- [[Knowledge - Qué es el fuselaje]]
- [[Knowledge - Qué son los estabilizadores]]
- [[Knowledge - Qué son las superficies de control]]
- [[Knowledge - Qué significa estabilidad]]
- [[Knowledge - Qué significa trimar un avión]]

### Resultado de la fase

Poder observar un avión y explicar:

- Qué función cumple cada componente.
- Cómo se genera la sustentación.
- Cómo se genera el empuje.
- Cómo se controla el avión.
- Qué diferencia existe entre estabilidad y control.

### Evidencia

- [] Avión de referencia seleccionado.
- [] Partes principales identificadas.
- [] Diagrama del avión realizado.
- [] Conceptos básicos documentados.

---

## Fase 1 — Atmósfera y condiciones de vuelo

### Objetivo

Comprender el entorno en el que vuela el avión y cómo las condiciones atmosféricas afectan su comportamiento.

### Estudio — Meseguer

**Capítulo 1 — La atmósfera**

Estudiar el capítulo completo:

- La atmósfera terrestre: composición y estructura vertical (troposfera, estratosfera, mesosfera, termosfera)
- Ecuación fundamental de la estática de fluidos (ecuación hidrostática)
- La atmósfera estándar: definición, capas y cálculo de presión, densidad y temperatura en función de la altitud

### Conceptos

- [[Knowledge - Atmósfera]]
- [[Knowledge - Atmósfera estándar]]
- [[Knowledge - Densidad del aire]]
- [[Knowledge - Presión atmosférica]]
- [[Knowledge - Temperatura atmosférica]]
- [[Knowledge - Número de Mach]]
- [[Knowledge - Número de Reynolds]]

### Resultado de la fase

Poder determinar las condiciones atmosféricas en las que se analizará el avión.

### Evidencia

- [] Condiciones de diseño definidas.
- [] Altitud de operación definida.
- [] Temperatura de operación definida.
- [] Densidad del aire determinada.
- [] Reynolds estimado.
- [] Mach estimado.

> *Nota: la tarjeta "Gravedad" se eliminó (venía del enfoque aeroespacial de Franchini, con entorno planetario y órbitas). Si se desea, crearla como conocimiento independiente.*

---

## Fase 2 — Mecánica de fluidos

### Objetivo

Comprender cómo se comporta el aire alrededor del avión.

### Estudio — Meseguer

**Capítulo 2 — Flujos incompresibles e irrotacionales**

Estudiar:

- Hipótesis del medio continuo
- Descripción del movimiento de un fluido: campo de velocidades, líneas de corriente, trayectorias
- Ecuación de conservación de masa (continuidad)
- Ecuación de Bernoulli
- Rotacional, flujo irrotacional, potencial de velocidades y función de corriente
- Flujos elementales: uniforme, fuente/sumidero, vórtice
- Superposición de flujos: flujo alrededor de un cilindro sin y con circulación
- Teorema de Kutta–Joukowski

Dejar para después:

- Flujos compresibles → Capítulo 5, Fase 16
- Capa límite y flujos viscosos → comprensión cualitativa aquí; profundización en Fase 16

### Conceptos

- [[Knowledge - Fluido]]
- [[Knowledge - Flujo]]
- [[Knowledge - Presión]]
- [[Knowledge - Velocidad del flujo]]
- [[Knowledge - Viscosidad]]
- [[Knowledge - Flujo viscoso]]
- [[Knowledge - Flujo compresible]]
- [[Knowledge - Capa límite]]
- [[Knowledge - Conservación de masa]]
- [[Knowledge - Cantidad de movimiento]]

### Herramienta

- [[SimScale]]
- [[XFLR5]]

### Resultado de la fase

Poder explicar qué ocurre con el aire cuando pasa alrededor de un objeto y comprender los fundamentos necesarios para posteriormente utilizar CFD.

### Evidencia

- [] Conceptos de flujo comprendidos.
- [] Conservación de masa comprendida.
- [] Cantidad de movimiento comprendida.
- [] Viscosidad comprendida.
- [] Compresibilidad comprendida.
- [] Primer experimento de flujo realizado.

---

## Fase 3 — Aerodinámica de perfiles

### Objetivo

Comprender cómo un perfil aerodinámico genera sustentación y resistencia y aprender a analizar diferentes perfiles.

### Estudio — Meseguer

**Capítulo 3 — Aerodinámica del perfil**

Estudiar:

- Geometría del perfil: cuerda, curvatura (línea de curvatura), espesor relativo
- Series NACA y nomenclatura de perfiles
- Origen de las cargas aerodinámicas; condición de Kutta
- Fuerza aerodinámica sobre un perfil: sustentación, resistencia, momento
- Coeficientes aerodinámicos
- Centro de presión y centro aerodinámico
- Teoría del perfil delgado (nivel de resultados y su uso; la deducción matemática completa se pospone a Fase 16)
- Curvas características del perfil y polar aerodinámica
- Entrada en pérdida de perfiles
- Perfiles laminares

Dejar inicialmente:

- Perfiles en régimen subsónico compresible (corrección de Prandtl–Glauert) → Capítulo 5, Fase 16
- Perfiles en régimen supersónico → Capítulo 5, Fase 16

### Conceptos

- [[Knowledge - Perfil aerodinámico]]
- [[Knowledge - Cuerda]]
- [[Knowledge - Línea de curvatura]]
- [[Knowledge - Espesor relativo]]
- [[Knowledge - Sustentación]]
- [[Knowledge - Resistencia]]
- [[Knowledge - Momento]]
- [[Knowledge - Coeficiente de sustentación]]
- [[Knowledge - Coeficiente de resistencia]]
- [[Knowledge - Coeficiente de momento]]
- [[Knowledge - Ángulo de ataque]]
- [[Knowledge - Pérdida]]
- [[Knowledge - Polar aerodinámica]]
- [[Knowledge - Reynolds]]

### Herramienta

- [[XFLR5]]

### Proyecto 1 — NACA 2412

Analizar el perfil NACA 2412.

Comparar posteriormente con:

- NACA 0012
- NACA 4412

### Analizar

- CL
- CD
- Cm
- CL/CD
- Ángulo de ataque
- Ángulo de pérdida

### Resultado de la fase

Poder seleccionar un perfil aerodinámico basándose en sus características y no únicamente en su apariencia.

### Evidencia

- [] NACA 2412 analizado.
- [] Polar obtenida.
- [] CL analizado.
- [] CD analizado.
- [] Cm analizado.
- [] Pérdida identificada.
- [] NACA 0012 comparado.
- [] NACA 4412 comparado.
- [] Perfil seleccionado para el proyecto.

---

## Fase 4 — Aerodinámica del ala

### Objetivo

Pasar del análisis de un perfil bidimensional al diseño de un ala tridimensional.

### Estudio — Meseguer

**Capítulo 4 — Aerodinámica del ala**

Estudiar:

- Geometría del ala: envergadura, alargamiento, estrechamiento, flecha, diedro, torsión
- Arquitectura de alas
- Flujo en alas de envergadura finita: vórtices de punta, descenso inducido
- Resistencia inducida
- Teoría de la línea de sustentación de Prandtl (nivel de resultados; desarrollo completo en Fase 16)
- Distribución de sustentación; ala elíptica
- Efecto del alargamiento y la flecha sobre las características del ala

Dejar inicialmente:

- Alas en régimen compresible → Capítulo 5, Fase 16
- Dispositivos hipersustentadores: si la edición no los desarrolla en profundidad, complementar con Franchini 5.7 (se retoman en Fase 16)

### Conceptos

- [[Knowledge - Ala]]
- [[Knowledge - Envergadura]]
- [[Knowledge - Cuerda]]
- [[Knowledge - Alargamiento]]
- [[Knowledge - Estrechamiento]]
- [[Knowledge - Flecha]]
- [[Knowledge - Diedro]]
- [[Knowledge - Torsión geométrica]]
- [[Knowledge - Vórtices de punta]]
- [[Knowledge - Resistencia inducida]]
- [[Knowledge - Distribución de sustentación]]
- [[Knowledge - Dispositivos hipersustentadores]]

### Herramienta

- [[XFLR5]]

### Proyecto 2 — Primera ala

Crear una primera ala utilizando el perfil seleccionado.

Definir:

- Envergadura
- Cuerda
- Alargamiento
- Estrechamiento
- Flecha
- Diedro
- Perfil
- Torsión

### Comparaciones

Modificar una variable a la vez y observar cómo cambia:

- Sustentación
- Resistencia
- Eficiencia
- Distribución de sustentación
- Pérdida

### Resultado de la fase

Tener una primera ala analizada en XFLR5 y comprender cómo sus dimensiones afectan el comportamiento aerodinámico.

### Evidencia

- [] Ala creada en XFLR5.
- [] Geometría documentada.
- [] Análisis aerodinámico realizado.
- [] Distribución de sustentación analizada.
- [] Diferentes alargamientos comparados.
- [] Diferentes estrechamientos comparados.
- [] Ala seleccionada para el avión.

---

## Fase 5 — Propulsión

### Objetivo

Comprender cómo proporcionar al avión el empuje necesario para cumplir su misión.

### Estudio

**No cubierto por Aerodinámica Básica** — el libro se limita a la aerodinámica. Usar bibliografía complementaria.

**Opción A — Franchini (como complemento):**

**Capítulo 6 — Introducción a la propulsión**

Estudiar:

- 6.1 Introducción
- 6.2 Rendimientos
- 6.3 Empuje
- 6.4 Consumo específico por unidad de empuje
- 6.5 Impulso específico y velocidad de salida efectiva
- 6.7 Clasificación de los sistemas de propulsión
- 6.8 Comparación de los sistemas de propulsión

**Capítulo 7 — Propulsión a hélice**

Estudiar:

- 7.1 Introducción
- 7.2 Geometría de la hélice
- 7.3 Campo de velocidades en un perfil de hélice
- 7.4 Fuerzas en un perfil de hélice
- 7.5 Teoría de cantidad de movimiento
- 7.6 Curvas características de una hélice
- 7.7 Regímenes de funcionamiento de la hélice
- 7.9 Sistema motor asociado a una hélice
- 7.10 Motor alternativo
- 7.13 Potencia en el eje del motor

**Opción B — Anderson, *Fundamentos de ingeniería aeronáutica***: capítulos de propulsión.

**Dejar para después**

- Franchini Capítulo 8 — Propulsión a chorro: no es necesario para el primer avión.

### Conceptos

- [[Knowledge - Empuje]]
- [[Knowledge - Potencia]]
- [[Knowledge - Eficiencia propulsiva]]
- [[Knowledge - Hélice]]
- [[Knowledge - Paso de hélice]]
- [[Knowledge - RPM]]
- [[Knowledge - Potencia en el eje]]
- [[Knowledge - Motor eléctrico]]
- [[Knowledge - Batería]]
- [[Knowledge - Relación empuje-peso]]

### Proyecto 3 — Sistema de propulsión

Seleccionar:

- Motor
- ESC
- Batería
- Hélice

Determinar:

- Potencia
- RPM
- Empuje
- Consumo
- Tiempo de funcionamiento

### Resultado de la fase

Tener un sistema de propulsión capaz de proporcionar el empuje necesario para el avión.

### Evidencia

- [] Motor seleccionado.
- [] ESC seleccionado.
- [] Batería seleccionada.
- [] Hélice seleccionada.
- [] Empuje estimado.
- [] Potencia estimada.
- [] Consumo estimado.
- [] Sistema de propulsión documentado.

---

## Fase 6 — Requisitos del avión

### Objetivo

Definir qué debe hacer el avión antes de decidir cómo será.

### Definir la misión

El avión debe tener una misión concreta.

Ejemplo:

> Diseñar un UAV eléctrico pequeño destinado a vuelo de entrenamiento y pruebas aerodinámicas.

### Parámetros

- Masa máxima
- Carga útil
- Velocidad de crucero
- Velocidad máxima
- Velocidad de pérdida
- Altitud de operación
- Autonomía
- Tiempo de vuelo
- Distancia de despegue
- Distancia de aterrizaje
- Tipo de despegue
- Tipo de aterrizaje
- Condiciones de viento
- Sistema de propulsión

### Conceptos

- [[Knowledge - Requisitos de diseño]]
- [[Knowledge - Misión de diseño]]
- [[Knowledge - Carga útil]]
- [[Knowledge - Velocidad de crucero]]
- [[Knowledge - Velocidad de pérdida]]
- [[Knowledge - Autonomía]]
- [[Knowledge - Carga alar]]
- [[Knowledge - Relación empuje-peso]]

### Resultado de la fase

Tener una especificación cuantitativa del avión.

### Evidencia

- [] Misión definida.
- [] Requisitos definidos.
- [] Masa objetivo definida.
- [] Velocidad de crucero definida.
- [] Velocidad de pérdida definida.
- [] Autonomía definida.
- [] Carga útil definida.
- [] Condiciones de operación definidas.

---

## Fase 7 — Actuaciones

### Objetivo

Determinar si el avión diseñado puede cumplir los requisitos establecidos.

### Estudio

**No cubierto por Aerodinámica Básica** — usar bibliografía complementaria.

**Opción A — Franchini (como complemento):**

**Capítulo 9 — Actuaciones**

Estudiar:

- 9.1 Introducción
- 9.2 Fuerzas externas sobre el avión
- 9.3 Ecuaciones del movimiento
- 9.4 Vuelo horizontal rectilíneo y uniforme
- 9.5 Ascenso y descenso rectilíneo uniforme
- 9.6 Vuelo de planeo rectilíneo y uniforme
- 9.7 Factor de carga
- 9.8 Viraje en un plano vertical
- 9.9 Viraje en un plano horizontal
- 9.10 Actuaciones integrales

**Opción B — Anderson**: capítulos de vuelo (crucero, ascenso, alcance y autonomía).

### Conceptos

- [[Knowledge - Peso]]
- [[Knowledge - Sustentación]]
- [[Knowledge - Resistencia]]
- [[Knowledge - Empuje]]
- [[Knowledge - Vuelo estacionario]]
- [[Knowledge - Vuelo de crucero]]
- [[Knowledge - Ascenso]]
- [[Knowledge - Descenso]]
- [[Knowledge - Planeo]]
- [[Knowledge - Factor de carga]]
- [[Knowledge - Radio de giro]]

### Proyecto 4 — Actuaciones

Calcular/estimar:

- Velocidad de pérdida
- Velocidad de crucero
- Velocidad máxima
- Capacidad de ascenso
- Planeo
- Radio de giro

### Resultado de la fase

Comprobar mediante cálculos si el avión cumple los requisitos definidos.

### Evidencia

- [] Velocidad de pérdida calculada.
- [] Velocidad de crucero calculada.
- [] Velocidad máxima estimada.
- [] Ascenso analizado.
- [] Planeo analizado.
- [] Viraje analizado.
- [] Requisitos comparados con resultados.

---

## Fase 8 — Estabilidad y control

### Objetivo

Diseñar un avión que no solamente pueda volar, sino que pueda mantenerse y controlarse.

### Conceptos

- [[Knowledge - Estabilidad estática]]
- [[Knowledge - Estabilidad dinámica]]
- [[Knowledge - Centro de gravedad]]
- [[Knowledge - Centro aerodinámico]]
- [[Knowledge - Punto neutro]]
- [[Knowledge - Margen estático]]
- [[Knowledge - Momento de cabeceo]]
- [[Knowledge - Estabilizador horizontal]]
- [[Knowledge - Estabilizador vertical]]
- [[Knowledge - Elevador]]
- [[Knowledge - Alerón]]
- [[Knowledge - Timón de dirección]]
- [[Knowledge - Trimado]]

### Estudiar

- Estabilidad longitudinal
- Estabilidad lateral
- Estabilidad direccional
- Posición del centro de gravedad
- Tamaño del estabilizador horizontal
- Tamaño del estabilizador vertical
- Superficies de control

### Herramienta

- [[XFLR5]]

### Proyecto 5 — Estabilidad

Agregar al avión:

- Cola horizontal
- Cola vertical
- Elevador
- Timón
- Alerones

Determinar:

- Posición del CG
- Margen estático
- Comportamiento longitudinal
- Comportamiento lateral
- Comportamiento direccional

### Resultado de la fase

Tener una configuración del avión que sea estable y controlable.

### Evidencia

- [] CG definido.
- [] Cola horizontal dimensionada.
- [] Cola vertical dimensionada.
- [] Elevador definido.
- [] Alerones definidos.
- [] Timón definido.
- [] Estabilidad longitudinal analizada.
- [] Estabilidad lateral analizada.
- [] Estabilidad direccional analizada.

---

## Fase 9 — Diseño conceptual

### Objetivo

Integrar aerodinámica, propulsión, actuaciones y estabilidad en una única configuración.

### Proyecto 6 — Aircraft V1

Definir:

- Configuración
- Ala
- Fuselaje
- Cola
- Motor
- Hélice
- Batería
- CG
- Superficies de control
- Tren de aterrizaje

### Herramientas

- [[XFLR5]]
- [[OpenVSP]]

### Proceso

Requisitos
↓
Dimensionamiento
↓
Configuración
↓
Aerodinámica
↓
Propulsión
↓
Estabilidad
↓
Actuaciones
↓
Aircraft V1

### Resultado de la fase

Obtener un diseño conceptual completo del avión.

### Evidencia

- [] Configuración seleccionada.
- [] Geometría definida.
- [] Ala definida.
- [] Fuselaje definido.
- [] Cola definida.
- [] Propulsión definida.
- [] CG definido.
- [] Superficies de control definidas.
- [] Modelo conceptual completo.

---

## Fase 10 — Diseño CAD

### Objetivo

Convertir el diseño conceptual en una geometría detallada y fabricable.

### Herramienta

- [[Onshape]]

### Estudiar

- Sketches
- Restricciones
- Partes
- Ensamblajes
- Configuraciones
- Curvas
- Superficies
- Loft
- Sweep
- Shell
- Diseño Top-Down
- Planos técnicos

### Proyecto 7 — CAD del avión

Modelar:

- Fuselaje
- Ala
- Costillas
- Largueros
- Cola
- Superficies de control
- Soporte del motor
- Tren de aterrizaje
- Compartimiento electrónico

### Resultado de la fase

Tener un modelo CAD completo y organizado del avión.

### Evidencia

- [] Fuselaje modelado.
- [] Ala modelada.
- [] Cola modelada.
- [] Superficies de control modeladas.
- [] Componentes internos modelados.
- [] Ensamblaje completo.
- [] Modelo preparado para fabricación.

---

## Fase 11 — Estructuras

### Objetivo

Comprobar que el avión puede soportar las cargas a las que estará sometido.

### Conceptos

- [[Knowledge - Cargas estructurales]]
- [[Knowledge - Esfuerzo]]
- [[Knowledge - Deformación]]
- [[Knowledge - Flexión]]
- [[Knowledge - Torsión]]
- [[Knowledge - Factor de seguridad]]
- [[Knowledge - Larguero]]
- [[Knowledge - Costilla]]

### Analizar

- Ala
- Largueros
- Costillas
- Fuselaje
- Soporte del motor
- Unión ala-fuselaje
- Tren de aterrizaje

### Herramienta

- [[SimScale]]

### Resultado de la fase

Tener una estructura capaz de soportar las cargas de diseño con un margen de seguridad adecuado.

### Evidencia

- [] Cargas de diseño definidas.
- [] Ala analizada.
- [] Fuselaje analizado.
- [] Factor de seguridad definido.
- [] Puntos críticos identificados.
- [] Estructura modificada según resultados.

---

## Fase 12 — CFD

### Objetivo

Simular el flujo de aire alrededor del avión y comparar los resultados con los modelos utilizados anteriormente.

### Herramienta

- [[SimScale]]

### Estudiar

- Geometría para CFD
- Dominio de flujo
- Mallado
- Condiciones de frontera
- Modelo de turbulencia
- Resolución
- Postprocesamiento
- Convergencia

### Proyecto 8 — CFD del avión

Comenzar con:

1. Perfil
2. Ala
3. Avión completo

### Analizar

- Presión
- Velocidad
- Sustentación
- Resistencia
- Separación del flujo
- Distribución de presión
- Vórtices
- Comportamiento a diferentes ángulos de ataque

### Comparar

**XFLR5 vs SimScale**

Registrar diferencias y posibles causas.

### Resultado de la fase

Tener una simulación CFD del avión y comprender sus limitaciones.

### Evidencia

- [] Geometría preparada.
- [] Dominio creado.
- [] Mallado realizado.
- [] Simulación ejecutada.
- [] Convergencia comprobada.
- [] Presiones analizadas.
- [] Velocidades analizadas.
- [] Sustentación obtenida.
- [] Resistencia obtenida.
- [] XFLR5 comparado con CFD.

---

## Fase 13 — Fabricación

### Objetivo

Construir físicamente el avión diseñado.

### Decisiones

Definir:

- Material
- Método de fabricación
- Electrónica
- Sistema de control
- Método de ensamblaje
- Reparabilidad

### Proyecto 9 — Aircraft V1 físico

Fabricar:

- Ala
- Fuselaje
- Cola
- Superficies de control
- Soporte del motor
- Sistema eléctrico

### Resultado de la fase

Tener un prototipo físico construido a partir del modelo CAD.

### Evidencia

- [] Materiales seleccionados.
- [] Piezas fabricadas.
- [] Ala construida.
- [] Fuselaje construido.
- [] Cola construida.
- [] Electrónica instalada.
- [] Avión ensamblado.

---

## Fase 14 — Pruebas

### Objetivo

Comprobar experimentalmente si el avión se comporta como fue previsto.

### Pruebas

- Peso
- Centro de gravedad
- Controles
- Motor
- Hélice
- Empuje
- Consumo
- Prueba de rodaje
- Planeo
- Vuelo
- Velocidad
- Ascenso
- Autonomía

### Resultado de la fase

Obtener datos reales del comportamiento del avión.

### Evidencia

- [] Peso medido.
- [] CG medido.
- [] Empuje medido.
- [] Consumo medido.
- [] Controles comprobados.
- [] Prueba de planeo realizada.
- [] Primer vuelo realizado.
- [] Datos registrados.

---

## Fase 15 — Validación e iteración

### Objetivo

Comparar el avión real con el modelo y utilizar las diferencias para mejorar el diseño.

### Comparar

**Teoría (Meseguer)**

vs.

**XFLR5**

vs.

**SimScale**

vs.

**Pruebas reales**

### Analizar diferencias

- Sustentación
- Resistencia
- Velocidad
- Consumo
- Ascenso
- Estabilidad
- Control
- Peso

### Proyecto 10 — Aircraft V2

Modificar el diseño según los datos obtenidos.

### Resultado de la fase

Crear una segunda versión del avión basada en evidencia experimental.

### Evidencia

- [] Datos teóricos registrados.
- [] Datos XFLR5 registrados.
- [] Datos CFD registrados.
- [] Datos reales registrados.
- [] Diferencias identificadas.
- [] Causas investigadas.
- [] Cambios definidos.
- [] Aircraft V2 diseñado.

---

## Fase 16 — Profundización

Una vez terminado el primer avión, volver a los temas que fueron simplificados durante la primera iteración.

### Meseguer — Aerodinámica Básica

- Capítulo 5 — Flujos compresibles: estudiar completo
  - Flujo isentrópico unidimensional
  - Ondas de choque normales y oblicuas
  - Perfiles en régimen subsónico compresible (corrección de Prandtl–Glauert)
  - Régimen transónico
  - Perfiles y alas en régimen supersónico
  - Alas en flecha
- Teoría del perfil delgado: deducción matemática completa (Capítulo 3)
- Teoría de la línea de sustentación: desarrollo completo (Capítulo 4)
- Capa límite y flujos viscosos: fricción, separación, resistencia de perfil

### Complementos (no cubiertos por Meseguer)

- Franchini Capítulo 8 — Propulsión a chorro (si no se hizo en Fase 5)
- Franchini Capítulo 10 — Análisis de órbitas
- Franchini Capítulo 11 — Misiones espaciales
- Franchini Capítulo 12 — Helicópteros
- Franchini Apéndices — Viento atmosférico, fuerzas sobre un fluido, análisis dimensional, control del rotor
- Dispositivos hipersustentadores (si no se complementaron en Fase 4)
- Estabilidad y control a nivel de texto especializado (Etkin, Nelson)

---

# Proyecto final

## Aircraft V1

### Misión

Pendiente.

### Requisitos

Pendiente.

### Aerodinámica

Pendiente.

### Perfil

Pendiente.

### Ala

Pendiente.

### Propulsión

Pendiente.

### Estabilidad

Pendiente.

### Actuaciones

Pendiente.

### Estructura

Pendiente.

### CAD

Pendiente.

### CFD

Pendiente.

### Fabricación

Pendiente.

### Pruebas

Pendiente.

### Resultados

Pendiente.

---

# Próximas acciones

- [] [[Knowledge - Qué es un avión]]
- [] [[Knowledge - Qué es un UAV]]
- [] [[Knowledge - Qué es un ala]]
- [] [[Knowledge - Qué es un perfil aerodinámico]]
- [] [[Knowledge - Qué es el fuselaje]]
- [] [[Knowledge - Qué son los estabilizadores]]
- [] [[Knowledge - Qué son las superficies de control]]
- [] [[Knowledge - Qué significa estabilidad]]
- [] [[Knowledge - Qué significa trimar un avión]]
- [] Comenzar Capítulo 1 de Meseguer (La atmósfera)
- [] Comenzar Capítulo 2 de Meseguer (Flujos incompresibles e irrotacionales)
- [] Comenzar análisis de perfiles en XFLR5

---

# Evidencia

## Diseños

## Simulaciones

## Cálculos

## Modelos CAD

## Experimentos

## Pruebas de vuelo

## Datos

---

# Notas

- Ruta adaptada a *Aerodinámica Básica* (Meseguer y Sanz Andrés) como texto principal de aerodinámica (Fases 1–4).
- Fases 5 (Propulsión) y 7 (Actuaciones) requieren Franchini u Anderson como complemento, ya que Meseguer no las cubre.
- Los temas compresibles y las deducciones matemáticas completas se posponen a la Fase 16 para no retrasar el primer avión.
- Verificar numeración de secciones contra la edición del libro en uso.