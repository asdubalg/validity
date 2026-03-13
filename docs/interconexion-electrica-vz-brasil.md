# Interconexión Eléctrica Venezuela–Brasil: Sistema Roraima

## Introducción

La interconexión eléctrica entre Venezuela y Brasil para alimentar al **Sistema Eléctrico Roraima** (SEA, ubicado en el estado Roraima de Brasil) es un caso de estudio relevante en sistemas de potencia. Roraima es el único estado brasileño que no está interconectado al Sistema Interconectado Nacional (SIN) de Brasil; históricamente ha dependido de generación térmica local y de importaciones de Venezuela a través de la línea de 230 kV que conecta la subestación Santa Elena de Uairén (Venezuela) con Boa Vista (Brasil).

A continuación se analizan los principales problemas técnicos que pueden presentarse en esta interconexión: control de frecuencia, control de tensión (voltaje) y oscilaciones de potencia.

---

## 1. Control de Frecuencia

### 1.1 Diferencias entre sistemas

Venezuela opera en **60 Hz**, mientras que Brasil opera en **60 Hz** también; en este caso no existe incompatibilidad de frecuencia nominal. Sin embargo, ambos sistemas son independientes y pueden operar con pequeñas desviaciones de frecuencia en tiempo real. Cuando se realiza la interconexión:

- La **diferencia de fase** acumulada entre los dos sistemas debe ser llevada a cero o a un valor mínimo antes de cerrar el enlace (*sincronización*).
- Si la sincronización no es correcta, el cierre del interruptor puede generar un **golpe de sincronización** (*out-of-step closing*) que cause daños en generadores y transformadores.

### 1.2 Regulación de frecuencia en un sistema débil

El sistema Roraima es eléctricamente **débil** (poca capacidad de generación propia, baja inercia). Los problemas derivados son:

| Problema | Descripción |
|----------|-------------|
| **Baja inercia** | Un sistema con poca generación rotante tiene poca inercia cinética (H bajo). Ante cualquier perturbación (salida de una carga grande o de un generador), la frecuencia cae o sube muy rápidamente (*rate of change of frequency* alto, ROCOF alto). |
| **Dependencia del nodo externo** | Si la mayor parte de la potencia proviene de Venezuela, cualquier perturbación en la red venezolana (desconexión de la línea, problemas de generación) impacta directamente la frecuencia del sistema Roraima. |
| **Regulación primaria** | El regulador de velocidad (*governor*) de las unidades generadoras locales en Roraima debe responder ante desviaciones de frecuencia. Si la capacidad de regulación primaria local es escasa, la frecuencia puede salirse del rango tolerable (±0,5 Hz en operación normal, ±2 Hz antes de que actúe la protección de sub/sobrefrecuencia). |
| **Control AGC (Automático de Generación)** | Se necesita un esquema de **Control Automático de Generación (AGC)** que coordine la potencia intercambiada con Venezuela, manteniendo el flujo de potencia programado en la línea de interconexión y la frecuencia en 60 Hz. La acción AGC (regulación secundaria) puede ser compleja si el tiempo de respuesta de las unidades venezolanas es lento. |

### 1.3 Riesgo de colapso de frecuencia

Si la línea de interconexión se desconecta repentinamente (*islanding*) y el sistema Roraima no tiene suficiente generación local para cubrir la demanda, la frecuencia cae en picada. Para mitigar esto se implementan:

- **Deslastre automático de carga por baja frecuencia** (Under-Frequency Load Shedding, UFLS): esquemas en varios umbrales (p. ej., 59,0 Hz, 58,5 Hz, 58,0 Hz) que desconectan bloques de carga para estabilizar la frecuencia.
- **Generación local de respaldo** (diesel, gas) lista para arranque rápido.

---

## 2. Control de Tensión (Voltaje)

### 2.1 Caída de tensión en líneas largas

La línea de interconexión entre Santa Elena de Uairén y Boa Vista tiene una longitud considerable (~680 km por carretera; la línea eléctrica sigue un trazado similar). En líneas largas de alta tensión:

- **Caída de tensión resistiva e inductiva**: El flujo de potencia activa (MW) y reactiva (MVAR) a lo largo de la línea produce caída de tensión. La potencia reactiva es especialmente sensible: enviar potencia reactiva a través de una línea larga es ineficiente y degrada la tensión en el extremo receptor.
- **Efecto Ferranti**: En condiciones de baja carga, una línea larga puede presentar una tensión en el extremo receptor *mayor* que en el extremo fuente (efecto de la capacitancia distribuida de la línea), lo que puede provocar **sobretensiones**.

### 2.2 Potencia reactiva y compensación

Para mantener la tensión dentro de los límites operativos (típicamente ±5% de la tensión nominal):

- Se requiere **compensación reactiva** a lo largo de la línea y en las subestaciones extremas:
  - **Reactores en derivación (shunt reactors)**: Absorben el exceso de reactivo capacitivo en condiciones de baja carga, evitando sobretensiones.
  - **Bancos de condensadores en derivación (shunt capacitors)**: Generan potencia reactiva capacitiva (MVAR) para suministrar el reactivo necesario y compensar la caída de tensión en condiciones de carga alta.
  - **Compensadores estáticos de reactivo (SVC o STATCOM)**: Regulación dinámica y continua de la tensión con respuesta rápida.
- Los generadores en la planta venezolana deben operar en **modo de control de tensión** (con el AVR —regulador automático de tensión— activo) para regular la tensión en la barra de alta tensión de su subestación.

### 2.3 Colapso de tensión

Un problema grave en sistemas débiles es el **colapso de tensión**:

- Cuando la demanda de potencia reactiva supera la capacidad de suministro de la red, la tensión entra en un proceso de caída progresiva e inestable.
- En sistemas radiales (como Roraima, alimentado desde un solo punto), el colapso es más probable porque no existe redundancia de rutas para el flujo de potencia reactiva.
- **Índice de estabilidad de tensión (VSI)**: Se deben realizar estudios de flujo de carga con curvas P-V y Q-V para identificar el margen de estabilidad de tensión y dimensionar la compensación reactiva necesaria.

### 2.4 Coordinación de la regulación de tensión

- El AVR del generador venezolano y los compensadores en Boa Vista deben coordinar sus set-points para evitar **guerras de reactivo** (reactive power hunting): situaciones en que dos reguladores compiten, generando oscilaciones en la tensión.
- Se recomienda usar **Power System Stabilizers (PSS)** en los generadores para amortiguar oscilaciones.

---

## 3. Oscilaciones de Potencia

### 3.1 Tipos de oscilaciones

Las oscilaciones de potencia en sistemas interconectados son variaciones periódicas del flujo de potencia activa. Se clasifican por su frecuencia:

| Modo | Frecuencia | Descripción |
|------|-----------|-------------|
| **Modo local** | 0,8 – 2,0 Hz | Oscilación de un generador (o planta) contra la red local |
| **Modo inter-área** | 0,1 – 0,8 Hz | Oscilación de grupos de generadores de una región contra grupos de otra región |

En el caso de la interconexión Venezuela–Brasil, el modo de mayor preocupación es el **modo inter-área**: los generadores venezolanos oscilando contra los generadores del SIN de Brasil, con el sistema Roraima en el medio del enlace.

### 3.2 Causas y condiciones de riesgo

- **Línea de interconexión larga con alta reactancia**: Una línea larga tiene alta reactancia serie (X elevada). El **límite de transmisión de potencia estática** es P_max = (V₁ × V₂) / X. Si el ángulo de transmisión (δ) es alto (cercano a 90°), el sistema opera cerca de su límite de estabilidad estática y es susceptible a oscilaciones.
- **Bajo amortiguamiento**: Si los generadores no tienen PSS activos o si el amortiguamiento natural del modo inter-área es negativo, las oscilaciones pueden crecer en amplitud hasta causar la pérdida de sincronismo (*out-of-step*), lo que dispara las protecciones de distancia y desconecta la interconexión.
- **Cambios de carga o perturbaciones**: Cambios abruptos en la carga, maniobras de subestación, fallas y su despeje pueden excitar los modos de oscilación.

### 3.3 Criterio de estabilidad transitoria

Ante una falla trifásica en la línea (el peor caso), el sistema debe ser capaz de mantener la sincronización después del despeje de la falla. Se evalúa con:
- **Método del área igual (Equal Area Criterion)**: Gráficamente, el área de aceleración (durante la falla) no debe superar el área de desaceleración (post-falla). Si lo supera, el generador pierde sincronismo.
- **Simulación dinámica transitoria**: Software como PSS/E, PowerWorld o PSCAD permite simular la respuesta dinámica del sistema ante contingencias.

### 3.4 Mitigación de oscilaciones

| Medida | Mecanismo |
|--------|----------|
| **Power System Stabilizer (PSS)** | Añade una señal estabilizadora al AVR basada en la velocidad o la potencia del generador, introduciendo amortiguamiento en los modos de oscilación. Es la medida más costo-efectiva. |
| **FACTS (SVC, STATCOM, TCSC, UPFC)** | Los dispositivos de Flexible AC Transmission Systems pueden regular el flujo de potencia y el voltaje dinámicamente, aumentando el amortiguamiento de oscilaciones inter-área. |
| **Reducción del ángulo de transmisión** | Operar con menor flujo de potencia (mayor margen de estabilidad) o aumentar la tensión de operación para reducir el ángulo δ. |
| **Esquemas de control especial (SPS/RAS)** | Esquemas de Protección de Sistema (SPS - *Special Protection Schemes*) / Esquemas de Acción Remedial (RAS - *Remedial Action Schemes*) que, ante una oscilación inestable detectada, desconectan cargas o generadores para evitar la desconexión incontrolada. |
| **Interconexión en HVDC** | Una solución de alto costo pero que elimina el problema de oscilaciones inter-área: un enlace en corriente continua (HVDC) desacopla la dinámica de los dos sistemas AC, impidiendo la propagación de oscilaciones. Además, el control del HVDC puede proveer amortiguamiento activo. |

---

## 4. Otros Problemas Asociados

### 4.1 Compatibilidad de los sistemas de protección

- Las protecciones de distancia en la línea de interconexión deben estar coordinadas para no operar incorrectamente durante oscilaciones de potencia (existe un riesgo de **operación indeseada de la zona 1 de distancia** durante oscilaciones lentas).
- Se recomienda implementar **bloqueo por oscilación de potencia (Power Swing Blocking, PSB)** y **disparo por oscilación de potencia (Out-Of-Step Tripping, OOST)** en los relés de protección.

### 4.2 Calidad de energía

- Las variaciones de frecuencia y tensión afectan la calidad de la energía suministrada a los usuarios del sistema Roraima (variaciones de tensión, flicker, armónicas).

### 4.3 Aspectos regulatorios y operativos

- Se requieren acuerdos operativos entre los operadores de red: **ONS** (Operador Nacional do Sistema Elétrico, Brasil) y **CORPOELEC** (Venezuela).
- La coordinación de despacho y el intercambio de información en tiempo real son fundamentales para la operación segura.

---

## 5. Resumen de Problemas y Recomendaciones

| Área | Problema Principal | Recomendación |
|------|-------------------|---------------|
| **Frecuencia** | Alta tasa de cambio de frecuencia (ROCOF); dependencia del sistema venezolano | AGC coordinado; UFLS; generación local de respaldo |
| **Tensión** | Caída de tensión en línea larga; riesgo de colapso de tensión | Compensación reactiva (SVC/STATCOM, condensadores); estudios P-V y Q-V |
| **Oscilaciones** | Modo inter-área de bajo amortiguamiento; riesgo de pérdida de sincronismo | PSS en todos los generadores; estudios de estabilidad dinámica; considerar HVDC a largo plazo |
| **Protecciones** | Operación incorrecta de relés durante oscilaciones | PSB y OOST en protecciones de distancia |
| **Operación** | Coordinación entre ONS y CORPOELEC | Acuerdos operativos formales; intercambio de datos SCADA en tiempo real |

---

## Referencias Técnicas

- Kundur, P. (1994). *Power System Stability and Control*. McGraw-Hill.
- Anderson, P. M., & Fouad, A. A. (2003). *Power System Control and Stability*. IEEE Press.
- CIGRÉ. (2013). *Interconnected Power Systems – Challenges and Opportunities*. Technical Brochure 553.
- IEEE Std 1110-2002. *Guide for Synchronous Generator Modeling Practices in Stability Analyses*.
- ONS (Operador Nacional do Sistema Elétrico). Estudios de integración del sistema Roraima al SIN.
