import { useState, useEffect, useCallback, useRef } from "react";

// ─── BANCO DE PREGUNTAS CONASET CLASE B ────────────────────────────────
const PREGUNTAS_DB = [
  // ── SEÑALIZACIÓN ──
  {
    id: 1, tema: "Señalización",
    pregunta: "¿Cómo se clasifican las señales de tránsito verticales?",
    opciones: [
      "Por las vías donde se encuentran",
      "Por las luces que tienen",
      "Por las formas que tienen"
    ],
    correcta: 2,
    explicacion: "Las señales verticales se clasifican por su forma: reglamentarias (circulares), preventivas (romboidales) e informativas (rectangulares). Libro del Nuevo Conductor, Cap. Señales de Tránsito.",
    doble: false
  },
  {
    id: 2, tema: "Señalización",
    pregunta: "Una señal de tránsito con forma de triángulo invertido indica:",
    opciones: [
      "Pare obligatorio",
      "Ceda el paso",
      "Zona de peligro",
      "Velocidad máxima"
    ],
    correcta: 1,
    explicacion: "El triángulo invertido (vértice hacia abajo) es la señal de 'Ceda el Paso', que obliga a disminuir la velocidad y ceder a los vehículos que circulan por la vía preferente.",
    doble: false
  },
  {
    id: 3, tema: "Señalización",
    pregunta: "Para ingresar a una intersección con luz verde, usted debe verificar que:",
    opciones: [
      "Debe existir previamente luz amarilla",
      "Debe existir espacio suficiente para no bloquear el cruce",
      "No tener el paso de cebra demarcado"
    ],
    correcta: 1,
    explicacion: "Antes de ingresar a un cruce con luz verde, debe asegurarse de que existe espacio suficiente al otro lado para no quedar bloqueando la intersección. Art. 131 Ley de Tránsito.",
    doble: false
  },
  {
    id: 4, tema: "Señalización",
    pregunta: "La línea continua amarilla pintada junto a la acera o solera significa:",
    opciones: [
      "Prohibido estacionar y detenerse",
      "Estacionamiento permitido solo de noche",
      "Zona de carga y descarga"
    ],
    correcta: 0,
    explicacion: "La línea amarilla continua indica prohibición absoluta de estacionar y detenerse en esa zona. Ley de Tránsito, señalización horizontal.",
    doble: false
  },
  {
    id: 5, tema: "Señalización",
    pregunta: "¿A qué distancia mínima de una esquina o señal PARE se prohíbe estacionar?",
    opciones: [
      "A más de 10 metros, en ambos casos",
      "A menos de 10 metros, en ambos casos",
      "Nunca se podrá estacionar cerca de una esquina o signo Pare o Ceda el Paso"
    ],
    correcta: 0,
    explicacion: "Se prohíbe estacionar a menos de 10 metros de una esquina y de una señal PARE o CEDA EL PASO. Por lo tanto, se debe estacionar a más de 10 metros. Art. 153 Ley de Tránsito.",
    doble: false
  },
  // ── NORMATIVA DE TRÁNSITO ──
  {
    id: 6, tema: "Normativa",
    pregunta: "Si usted se ve involucrado en un accidente de tránsito y se comprueba que conducía bajo la influencia del alcohol, ¿qué ocurrirá?",
    opciones: [
      "Se presumirá que usted no tuvo responsabilidad alguna",
      "Se presumirá que usted ha sido el culpable del accidente",
      "A usted se le aplicará sólo una infracción a la Ley de Tránsito"
    ],
    correcta: 1,
    explicacion: "La Ley de Tránsito establece presunción de culpabilidad para quien conduce bajo los efectos del alcohol y se ve involucrado en un siniestro. Ley 20.770 (Ley Emilia).",
    doble: true
  },
  {
    id: 7, tema: "Normativa",
    pregunta: "Al conducir, ¿cuándo es obligatorio el uso de cinturón de seguridad?",
    opciones: [
      "Sólo en la noche",
      "Siempre",
      "Sólo en días de lluvia y niebla"
    ],
    correcta: 1,
    explicacion: "El uso del cinturón de seguridad es obligatorio SIEMPRE, tanto para el conductor como para todos los pasajeros del vehículo. Art. 75 bis Ley de Tránsito.",
    doble: false
  },
  {
    id: 8, tema: "Normativa",
    pregunta: "Si se equivoca de salida en una autopista, usted debe:",
    opciones: [
      "Moverse hacia la berma y conducir marcha atrás hasta la salida",
      "Realizar un viraje en 'U' para volver hasta donde se encontraba la salida",
      "Continuar avanzando hasta encontrar la siguiente salida autorizada de la autopista"
    ],
    correcta: 2,
    explicacion: "En una autopista jamás se debe retroceder ni hacer virajes en U. Debe continuar hasta la siguiente salida autorizada y buscar una ruta alternativa. Art. 113 Ley de Tránsito.",
    doble: false
  },
  {
    id: 9, tema: "Normativa",
    pregunta: "¿Dónde está permitido adelantar a otro vehículo?",
    opciones: [
      "En zonas rurales exclusivamente",
      "Donde la señalización o demarcación lo permitan",
      "En las intersecciones de calles, caminos y pasos peatonales"
    ],
    correcta: 1,
    explicacion: "Solo se puede adelantar donde la señalización y demarcación lo permitan (línea segmentada). Nunca en intersecciones, curvas, puentes o pasos peatonales. Art. 139 Ley de Tránsito.",
    doble: false
  },
  {
    id: 10, tema: "Normativa",
    pregunta: "Antes de virar (girar) en una intersección, el conductor debe:",
    opciones: [
      "Aumentar la velocidad antes de girar",
      "Señalizar tu intención de virar con anticipación suficiente",
      "Encender las luces bajas delanteras"
    ],
    correcta: 1,
    explicacion: "Toda maniobra de viraje debe señalizarse con anticipación suficiente (mínimo 30 metros en zona urbana). Art. 142 Ley de Tránsito.",
    doble: false
  },
  {
    id: 11, tema: "Normativa",
    pregunta: "Un inspector fiscal le solicita detenerse para un control. Usted:",
    opciones: [
      "Debe colaborar, ya que los inspectores fiscales pueden supervigilar el cumplimiento de la Ley de Tránsito",
      "Debe evadir el control y reportar esta situación a Carabineros de Chile",
      "Debe negarse, ya que él no tiene facultades para realizar esta acción"
    ],
    correcta: 0,
    explicacion: "Los inspectores fiscales del Ministerio de Transportes están facultados para fiscalizar el cumplimiento de la Ley de Tránsito. Es deber del conductor colaborar. Art. 4 Ley de Tránsito.",
    doble: false
  },
  {
    id: 12, tema: "Normativa",
    pregunta: "¿Cuál es la velocidad máxima permitida en zonas urbanas para vehículos livianos?",
    opciones: [
      "50 km/h",
      "60 km/h",
      "80 km/h",
      "40 km/h"
    ],
    correcta: 1,
    explicacion: "La velocidad máxima en zonas urbanas para vehículos livianos es de 60 km/h, salvo que la señalización indique otra velocidad. Art. 145 Ley de Tránsito.",
    doble: false
  },
  // ── SEGURIDAD VIAL ──
  {
    id: 13, tema: "Seguridad Vial",
    pregunta: "¿Qué es la 'distancia de seguimiento' o 'distancia de separación'?",
    opciones: [
      "Conducir a una velocidad constante",
      "Mantener una adecuada distancia de separación entre vehículos",
      "Asegurarse de que sus frenos sean eficientes y tener neumáticos en muy buen estado"
    ],
    correcta: 1,
    explicacion: "La distancia de seguimiento es el espacio que se debe mantener con el vehículo que va adelante, permitiendo reaccionar y frenar oportunamente. Regla de los 3 segundos.",
    doble: false
  },
  {
    id: 14, tema: "Seguridad Vial",
    pregunta: "Cuando un peatón se encuentra cruzando por un paso de cebra, el conductor debe:",
    opciones: [
      "Detenerse y ceder el paso al peatón",
      "Tocar la bocina para alertar al peatón",
      "Pasar el paso de peatones lo más rápido posible"
    ],
    correcta: 0,
    explicacion: "Los peatones tienen derecho preferente de paso en los cruces demarcados. El conductor debe detenerse completamente. Art. 176 Ley de Tránsito.",
    doble: false
  },
  {
    id: 15, tema: "Seguridad Vial",
    pregunta: "¿Por qué los conductores jóvenes tienen mayor riesgo de sufrir siniestros?",
    opciones: [
      "Poseen baja percepción del riesgo",
      "No aprenden a conducir correctamente",
      "Saben manejar bien"
    ],
    correcta: 0,
    explicacion: "Los conductores jóvenes tienden a subestimar los riesgos, sobreestimar sus habilidades y dejarse influir por la presión de los pares. Libro del Nuevo Conductor, Cap. El Individuo en el Tránsito.",
    doble: false
  },
  {
    id: 16, tema: "Seguridad Vial",
    pregunta: "La bocina del vehículo debe utilizarse para:",
    opciones: [
      "Apurar al vehículo que le antecede",
      "Anunciar que estacionará",
      "Prevenir un siniestro, si ello es estrictamente necesario"
    ],
    correcta: 2,
    explicacion: "La bocina es un elemento de seguridad que solo debe usarse para prevenir un siniestro cuando sea estrictamente necesario. Art. 78 Ley de Tránsito.",
    doble: false
  },
  {
    id: 17, tema: "Seguridad Vial",
    pregunta: "Conducir con sueño o fatiga puede provocar:",
    opciones: [
      "Aumento de la concentración",
      "Dificultad para mantener la atención en la conducción",
      "Mejora en los tiempos de reacción"
    ],
    correcta: 1,
    explicacion: "La fatiga y somnolencia reducen la atención, aumentan los tiempos de reacción y pueden provocar microsueños al volante. Libro del Nuevo Conductor, Cap. El Individuo en el Tránsito.",
    doble: false
  },
  {
    id: 18, tema: "Seguridad Vial",
    pregunta: "Al circular por una vía y acercarse a un ciclista, usted debe:",
    opciones: [
      "Tocar la bocina para advertirle",
      "Adelantarlo dejando al menos 1,5 metros de distancia lateral",
      "Pasar lo más cerca posible para no invadir la pista contraria"
    ],
    correcta: 1,
    explicacion: "La Ley de Convivencia Vial establece un distanciamiento mínimo de 1,5 metros al adelantar a un ciclista. Ley 21.088.",
    doble: false
  },
  // ── ALCOHOL Y DROGAS (DOBLE PUNTAJE) ──
  {
    id: 19, tema: "Alcohol y Drogas",
    pregunta: "¿Cuál es el efecto del alcohol sobre la capacidad de conducción?",
    opciones: [
      "Se percibe mejor el tiempo y el espacio",
      "Se mejora la visión",
      "Se puede presentar un comportamiento impulsivo y agresivo"
    ],
    correcta: 2,
    explicacion: "El alcohol deteriora las funciones cognitivas, genera desinhibición, comportamiento impulsivo, agresivo y una falsa sensación de seguridad. Ley Emilia / Libro del Nuevo Conductor.",
    doble: true
  },
  {
    id: 20, tema: "Alcohol y Drogas",
    pregunta: "Si un conductor tiene 0,3 g/l de alcohol en la sangre, la Ley establece que:",
    opciones: [
      "Está en condiciones normales para conducir",
      "Se encuentra en estado de ebriedad",
      "Se encuentra bajo la influencia del alcohol y no debe conducir"
    ],
    correcta: 2,
    explicacion: "Con 0,3 g/l de alcohol en sangre se configura conducción bajo la influencia del alcohol (Art. 110 Ley de Tránsito). Con 0,8 g/l se considera estado de ebriedad. Ambos son sancionados.",
    doble: true
  },
  {
    id: 21, tema: "Alcohol y Drogas",
    pregunta: "¿Qué sustancias, además del alcohol, pueden alterar la capacidad de conducción?",
    opciones: [
      "Determinados medicamentos",
      "Las bebidas gaseosas",
      "El agua mineral"
    ],
    correcta: 0,
    explicacion: "Medicamentos como ansiolíticos, antihistamínicos, antidepresivos y otros pueden producir somnolencia y alterar los reflejos. Siempre consulte al médico antes de conducir.",
    doble: false
  },
  // ── SISTEMAS DE RETENCIÓN INFANTIL (DOBLE PUNTAJE) ──
  {
    id: 22, tema: "Retención Infantil",
    pregunta: "Al elegir un Sistema de Retención Infantil (SRI), lo más importante es verificar:",
    opciones: [
      "Que el SRI esté en oferta en la tienda",
      "Que el SRI pueda instalarse correctamente en tu vehículo, considerando el tipo de anclaje y el tamaño",
      "Que el color del SRI combine con el interior del vehículo"
    ],
    correcta: 1,
    explicacion: "Lo fundamental es que el SRI sea compatible con el vehículo (tipo de anclaje ISOFIX o cinturón) y adecuado al peso y talla del niño. Ley 20.904 sobre SRI.",
    doble: true
  },
  {
    id: 23, tema: "Retención Infantil",
    pregunta: "Respecto al cinturón de seguridad en un automóvil, el conductor debe:",
    opciones: [
      "Asegurarte de que todas las personas, incluso en los asientos traseros, estén bien sujetas con su propio cinturón",
      "Solo preocuparse por el cinturón del conductor",
      "Permitir que dos personas compartan un mismo cinturón de seguridad"
    ],
    correcta: 0,
    explicacion: "Es responsabilidad del conductor que TODOS los ocupantes lleven puesto su cinturón de seguridad individual. Cada cinturón es para una sola persona. Art. 75 bis Ley de Tránsito.",
    doble: false
  },
  // ── MECÁNICA BÁSICA ──
  {
    id: 24, tema: "Mecánica Básica",
    pregunta: "¿Qué indica la luz de advertencia del aceite en el tablero del vehículo?",
    opciones: [
      "Que el nivel de combustible es bajo",
      "Que la presión de aceite del motor es insuficiente y debe detenerse",
      "Que debe cambiar el aceite de la transmisión"
    ],
    correcta: 1,
    explicacion: "La luz de aceite indica presión insuficiente en el sistema de lubricación. Debe detenerse de inmediato y verificar el nivel. Conducir sin aceite puede destruir el motor.",
    doble: false
  },
  {
    id: 25, tema: "Mecánica Básica",
    pregunta: "¿Cuál es la función principal del líquido de frenos?",
    opciones: [
      "Lubricar el motor",
      "Transmitir la presión del pedal a las ruedas para frenar el vehículo",
      "Enfriar el sistema de escape"
    ],
    correcta: 1,
    explicacion: "El líquido de frenos es un fluido hidráulico que transmite la fuerza del pedal a las pastillas o zapatas de freno. Su nivel debe revisarse periódicamente.",
    doble: false
  },
  {
    id: 26, tema: "Mecánica Básica",
    pregunta: "Los neumáticos con banda de rodamiento desgastada provocan:",
    opciones: [
      "Mayor agarre en piso mojado",
      "Menor distancia de frenado",
      "Mayor riesgo de aquaplaning y pérdida de adherencia"
    ],
    correcta: 2,
    explicacion: "Neumáticos desgastados pierden capacidad de evacuar agua, aumentando el riesgo de aquaplaning. La profundidad mínima legal del dibujo es 1,6 mm.",
    doble: false
  },
  {
    id: 27, tema: "Mecánica Básica",
    pregunta: "Una batería en mal estado puede causar que:",
    opciones: [
      "El vehículo consuma más combustible de lo normal",
      "El motor tenga dificultades para arrancar, especialmente con temperaturas bajas",
      "Los frenos dejen de funcionar"
    ],
    correcta: 1,
    explicacion: "Una batería descargada o deteriorada dificulta el arranque del motor, especialmente en climas fríos. Se recomienda verificar su estado periódicamente.",
    doble: false
  },
  // ── CONDUCCIÓN SEGURA ──
  {
    id: 28, tema: "Conducción Segura",
    pregunta: "¿Qué es el 'efecto túnel' en la conducción?",
    opciones: [
      "La pérdida progresiva del campo visual lateral al aumentar la velocidad",
      "La dificultad para ver dentro de un túnel oscuro",
      "Un efecto de la lluvia sobre el parabrisas"
    ],
    correcta: 0,
    explicacion: "El efecto túnel reduce el campo visual lateral a medida que aumenta la velocidad. A 130 km/h el campo visual se reduce a unos 30°. Libro del Nuevo Conductor.",
    doble: false
  },
  {
    id: 29, tema: "Conducción Segura",
    pregunta: "Si se duplica la velocidad de un vehículo, la distancia de frenado:",
    opciones: [
      "Se duplica",
      "Se cuadruplica",
      "Se mantiene igual",
      "Se triplica"
    ],
    correcta: 1,
    explicacion: "La energía cinética es proporcional al cuadrado de la velocidad. Al duplicar la velocidad, la distancia de frenado se multiplica por 4 (se cuadruplica).",
    doble: false
  },
  {
    id: 30, tema: "Conducción Segura",
    pregunta: "Un conductor defensivo se caracteriza porque:",
    opciones: [
      "Reacciona adecuadamente ante cualquier imprevisto",
      "Efectúa maniobras sorpresivas que sorprendan a los demás",
      "Conduce con excesiva precaución bloqueando el tránsito",
      "Actúa sin pensar en las consecuencias"
    ],
    correcta: 0,
    explicacion: "La conducción defensiva implica anticiparse a las situaciones de riesgo, mantener distancia segura y reaccionar correctamente ante imprevistos.",
    doble: false
  },
  // ── VELOCIDAD (DOBLE PUNTAJE) ──
  {
    id: 31, tema: "Velocidad",
    pregunta: "¿Por qué el exceso de velocidad es especialmente peligroso?",
    opciones: [
      "Porque puede llevar a errores en el cálculo de la distancia de frenado, aumentando el riesgo de siniestros",
      "Porque solo afecta a los peatones",
      "Porque el vehículo consume menos combustible"
    ],
    correcta: 0,
    explicacion: "El exceso de velocidad aumenta la distancia de frenado, reduce el campo visual (efecto túnel), disminuye el tiempo de reacción disponible y agrava las consecuencias de un impacto.",
    doble: true
  },
  {
    id: 32, tema: "Conducción Segura",
    pregunta: "Al conducir bajo lluvia intensa, usted debe:",
    opciones: [
      "Aumentar la velocidad para salir rápido de la zona de lluvia",
      "Reducir la velocidad, aumentar la distancia de seguimiento y encender las luces",
      "Mantener la misma velocidad que en condiciones normales"
    ],
    correcta: 1,
    explicacion: "Bajo lluvia se reduce la adherencia y visibilidad. Se debe reducir velocidad, aumentar distancia de seguimiento y encender luces bajas. Libro del Nuevo Conductor.",
    doble: false
  },
  {
    id: 33, tema: "Convivencia Vial",
    pregunta: "¿Quiénes son considerados 'usuarios vulnerables' de las vías?",
    opciones: [
      "Solo los conductores de camiones",
      "Peatones, ciclistas, motociclistas y personas con movilidad reducida",
      "Solo los pasajeros de buses"
    ],
    correcta: 1,
    explicacion: "Los usuarios vulnerables son aquellos con mayor riesgo en caso de siniestro: peatones, ciclistas, motociclistas, niños, adultos mayores y personas con discapacidad. Ley 21.088.",
    doble: false
  },
  {
    id: 34, tema: "Primeros Auxilios",
    pregunta: "Si presencia un accidente de tránsito, lo primero que debe hacer es:",
    opciones: [
      "Mover a los heridos rápidamente fuera del vehículo",
      "Proteger la zona, alertar a los servicios de emergencia y socorrer según sus capacidades (PAS)",
      "Continuar su camino si no está involucrado"
    ],
    correcta: 1,
    explicacion: "Se debe aplicar la conducta PAS: Proteger la zona (señalizar), Alertar a emergencias (131/132/133), y Socorrer según la capacidad de cada persona. No mover heridos innecesariamente.",
    doble: false
  },
  {
    id: 35, tema: "Alcohol y Drogas",
    pregunta: "El consumo de alcohol afecta al conductor porque:",
    opciones: [
      "El razonamiento estará gravemente afectado y las decisiones no serán las más seguras",
      "El tiempo de reacción se incrementará facilitando ver los obstáculos con mayor eficacia",
      "La cantidad y calidad de información del entorno disminuye, facilitando malinterpretar situaciones"
    ],
    correcta: 0,
    explicacion: "El alcohol deteriora el juicio, la coordinación motora, el tiempo de reacción y la capacidad de tomar decisiones seguras. Todas las opciones contienen algo cierto, pero la A es la más completa.",
    doble: true
  },
  // ── PREGUNTAS EXTRA PARA VARIEDAD ──
  {
    id: 36, tema: "Señalización",
    pregunta: "Las señales reglamentarias de tránsito tienen generalmente forma:",
    opciones: [
      "Rectangular",
      "Circular",
      "Romboidal",
      "Triangular"
    ],
    correcta: 1,
    explicacion: "Las señales reglamentarias (obligación/prohibición) son circulares, excepto PARE (octógono) y CEDA EL PASO (triángulo invertido).",
    doble: false
  },
  {
    id: 37, tema: "Normativa",
    pregunta: "La 'Ley Emilia' (Ley 20.770) establece penas más severas para:",
    opciones: [
      "Conductores que no porten licencia",
      "Conductores en estado de ebriedad que causen lesiones graves o muerte",
      "Conductores que no paguen el TAG de autopistas"
    ],
    correcta: 1,
    explicacion: "La Ley Emilia endurece las penas para quienes conduzcan en estado de ebriedad y causen lesiones gravísimas o muerte, incluyendo penas de cárcel efectiva.",
    doble: true
  },
  {
    id: 38, tema: "Seguridad Vial",
    pregunta: "El 'Efecto rebote' del airbag ocurre cuando:",
    opciones: [
      "El conductor usa correctamente el cinturón",
      "El conductor no lleva cinturón y el airbag lo empuja violentamente hacia atrás",
      "El airbag no se activa en un choque"
    ],
    correcta: 1,
    explicacion: "Sin cinturón, el cuerpo impacta el airbag con toda su inercia y es rebotado hacia atrás, pudiendo causar lesiones graves o fatales. El cinturón y airbag son complementarios.",
    doble: false
  },
  {
    id: 39, tema: "Mecánica Básica",
    pregunta: "¿Cada cuántos kilómetros se recomienda revisar la presión de los neumáticos?",
    opciones: [
      "Cada 50.000 km",
      "Cada 500 km o al menos una vez al mes, en frío",
      "Solo cuando se percibe visualmente que están desinflados"
    ],
    correcta: 1,
    explicacion: "Se recomienda verificar la presión de los neumáticos cada 500 km o mínimo una vez al mes, siempre con los neumáticos fríos para una lectura correcta.",
    doble: false
  },
  {
    id: 40, tema: "Conducción Segura",
    pregunta: "¿Qué es la 'zona de incertidumbre' al conducir?",
    opciones: [
      "El área alrededor de otros usuarios viales donde podrían realizar movimientos impredecibles",
      "La zona donde no hay señalización",
      "El espacio dentro del vehículo"
    ],
    correcta: 0,
    explicacion: "La zona de incertidumbre es el espacio alrededor de peatones, ciclistas u otros vehículos donde podrían hacer movimientos inesperados. Se debe ampliar la distancia al pasar cerca de ellos.",
    doble: false
  },
  {
    id: 41, tema: "Normativa",
    pregunta: "En Chile, ¿desde qué edad se puede obtener la licencia de conducir Clase B?",
    opciones: [
      "16 años",
      "17 años",
      "18 años",
      "21 años"
    ],
    correcta: 2,
    explicacion: "Para obtener la licencia Clase B se requiere tener al menos 18 años cumplidos, haber aprobado el examen teórico y práctico, y contar con la documentación requerida.",
    doble: false
  },
  {
    id: 42, tema: "Señalización",
    pregunta: "Las señales preventivas o de advertencia tienen forma de:",
    opciones: [
      "Círculo",
      "Rombo (cuadrado girado en 45°)",
      "Octágono",
      "Rectángulo"
    ],
    correcta: 1,
    explicacion: "Las señales preventivas tienen forma romboidal (diamante), fondo amarillo y símbolo negro. Advierten sobre condiciones peligrosas en la vía.",
    doble: false
  },
  {
    id: 43, tema: "Conducción Segura",
    pregunta: "Al conducir, el uso del teléfono celular:",
    opciones: [
      "Está permitido si se conduce a baja velocidad",
      "Está prohibido, salvo con sistema manos libres",
      "Está permitido solo en autopistas"
    ],
    correcta: 1,
    explicacion: "Está prohibido manipular el celular mientras se conduce. Solo se permite usar un sistema de manos libres. Las multas por esta infracción son gravísimas. Art. 107 Ley de Tránsito.",
    doble: false
  },
  {
    id: 44, tema: "Convivencia Vial",
    pregunta: "Cuando un vehículo de emergencia se acerca con sirenas y balizas encendidas, usted debe:",
    opciones: [
      "Aumentar la velocidad para dejarle espacio atrás",
      "Continuar conduciendo normalmente",
      "Ceder el paso desplazándose hacia un lado y deteniéndose si es necesario"
    ],
    correcta: 2,
    explicacion: "Los vehículos de emergencia tienen derecho preferente de paso. Todos los conductores deben despejar la vía, desplazándose a la derecha y deteniéndose si fuera necesario. Art. 65 Ley de Tránsito.",
    doble: false
  },
  {
    id: 45, tema: "Seguridad Vial",
    pregunta: "El uso de luces bajas durante el día es obligatorio:",
    opciones: [
      "Solo en carreteras fuera de zonas urbanas",
      "En todo momento y en todas las vías del país",
      "Solo cuando llueve o hay niebla"
    ],
    correcta: 1,
    explicacion: "En Chile, desde 2005, es obligatorio circular con las luces bajas encendidas durante las 24 horas del día, en todas las vías del país. Art. 68 Ley de Tránsito.",
    doble: false
  }
];

// ─── CONSTANTES DEL EXAMEN ────────────────────────────────────────────
const TOTAL_PREGUNTAS = 35;
const TIEMPO_MAXIMO = 45 * 60; // 45 minutos en segundos
const PUNTAJE_APROBACION = 33;
const PUNTAJE_MAXIMO = 38; // 32 normales + 6 doble = 38

// ─── UTILIDADES ───────────────────────────────────────────────────────
function shuffle(arr) {
  const a = [...arr];
  for (let i = a.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [a[i], a[j]] = [a[j], a[i]];
  }
  return a;
}

function formatTime(s) {
  const m = Math.floor(s / 60);
  const sec = s % 60;
  return `${m.toString().padStart(2, "0")}:${sec.toString().padStart(2, "0")}`;
}

// ─── TEMAS Y COLORES ─────────────────────────────────────────────────
const TEMA_COLORS = {
  "Señalización": "#2563eb",
  "Normativa": "#7c3aed",
  "Seguridad Vial": "#059669",
  "Alcohol y Drogas": "#dc2626",
  "Retención Infantil": "#ea580c",
  "Velocidad": "#b91c1c",
  "Mecánica Básica": "#4f46e5",
  "Conducción Segura": "#0891b2",
  "Convivencia Vial": "#ca8a04",
  "Primeros Auxilios": "#be185d"
};

// ─── COMPONENTE PRINCIPAL ─────────────────────────────────────────────
export default function SimuladorExamen() {
  const [pantalla, setPantalla] = useState("inicio"); // inicio | examen | modoEstudio | resultado | revision
  const [claseSeleccionada, setClaseSeleccionada] = useState("B");
  const [modoExamen, setModoExamen] = useState("examen"); // examen | estudio
  const [preguntas, setPreguntas] = useState([]);
  const [indicePregunta, setIndicePregunta] = useState(0);
  const [respuestas, setRespuestas] = useState({});
  const [tiempoRestante, setTiempoRestante] = useState(TIEMPO_MAXIMO);
  const [examenTerminado, setExamenTerminado] = useState(false);
  const [mostrarExplicacion, setMostrarExplicacion] = useState(false);
  const [navAbierta, setNavAbierta] = useState(false);
  const timerRef = useRef(null);

  // Generar examen
  const iniciarExamen = useCallback((modo) => {
    const shuffled = shuffle(PREGUNTAS_DB);
    // Ensure we include enough doble-puntaje questions
    const dobles = shuffled.filter(p => p.doble);
    const normales = shuffled.filter(p => !p.doble);
    const seleccionDobles = dobles.slice(0, Math.min(3, dobles.length));
    const seleccionNormales = normales.slice(0, TOTAL_PREGUNTAS - seleccionDobles.length);
    const examen = shuffle([...seleccionDobles, ...seleccionNormales]);
    
    setPreguntas(examen);
    setIndicePregunta(0);
    setRespuestas({});
    setTiempoRestante(TIEMPO_MAXIMO);
    setExamenTerminado(false);
    setMostrarExplicacion(false);
    setModoExamen(modo);
    setPantalla(modo === "estudio" ? "modoEstudio" : "examen");
  }, []);

  // Timer
  useEffect(() => {
    if (pantalla === "examen" && !examenTerminado) {
      timerRef.current = setInterval(() => {
        setTiempoRestante(prev => {
          if (prev <= 1) {
            clearInterval(timerRef.current);
            setExamenTerminado(true);
            setPantalla("resultado");
            return 0;
          }
          return prev - 1;
        });
      }, 1000);
    }
    return () => clearInterval(timerRef.current);
  }, [pantalla, examenTerminado]);

  const seleccionarRespuesta = (idx) => {
    if (examenTerminado) return;
    if (modoExamen === "examen" && respuestas[indicePregunta] !== undefined) return;
    setRespuestas(prev => ({ ...prev, [indicePregunta]: idx }));
    if (modoExamen === "estudio") setMostrarExplicacion(true);
  };

  const siguientePregunta = () => {
    setMostrarExplicacion(false);
    if (indicePregunta < preguntas.length - 1) {
      setIndicePregunta(prev => prev + 1);
    }
  };

  const preguntaAnterior = () => {
    setMostrarExplicacion(false);
    if (indicePregunta > 0) setIndicePregunta(prev => prev - 1);
  };

  const terminarExamen = () => {
    clearInterval(timerRef.current);
    setExamenTerminado(true);
    setPantalla("resultado");
  };

  // Calcular resultados
  const calcularResultado = () => {
    let correctas = 0;
    let puntaje = 0;
    let porTema = {};
    
    preguntas.forEach((p, i) => {
      const tema = p.tema;
      if (!porTema[tema]) porTema[tema] = { correctas: 0, total: 0 };
      porTema[tema].total++;
      if (respuestas[i] === p.correcta) {
        correctas++;
        puntaje += p.doble ? 2 : 1;
        porTema[tema].correctas++;
      }
    });
    
    const sinResponder = TOTAL_PREGUNTAS - Object.keys(respuestas).length;
    return { correctas, puntaje, porTema, sinResponder, aprobado: puntaje >= PUNTAJE_APROBACION };
  };

  const volverInicio = () => {
    clearInterval(timerRef.current);
    setPantalla("inicio");
    setNavAbierta(false);
  };

  // ─── PANTALLA DE INICIO ─────────────────────────────────────────────
  if (pantalla === "inicio") {
    return (
      <div style={styles.app}>
        <style>{globalCSS}</style>
        <div style={styles.inicioContainer}>
          <div style={styles.heroSection}>
            <div style={styles.logoBadge}>
              <svg width="48" height="48" viewBox="0 0 48 48" fill="none">
                <circle cx="24" cy="24" r="22" stroke="#f59e0b" strokeWidth="3" fill="none"/>
                <circle cx="24" cy="24" r="16" fill="#f59e0b"/>
                <path d="M24 12 L24 24 L32 28" stroke="#1e293b" strokeWidth="3" strokeLinecap="round" strokeLinejoin="round" fill="none"/>
              </svg>
            </div>
            <h1 style={styles.heroTitle}>Simulador de Examen</h1>
            <h2 style={styles.heroSubtitle}>Licencia de Conducir Chile 2026</h2>
            <p style={styles.heroDesc}>
              Prepárate para el examen teórico de la CONASET con nuestro simulador. 
              35 preguntas, 45 minutos, formato idéntico al de la municipalidad.
            </p>
          </div>

          <div style={styles.claseSelector}>
            <p style={styles.claseSelectorLabel}>Selecciona tu licencia:</p>
            <div style={styles.claseButtons}>
              {[
                { id: "B", icon: "🚗", label: "Clase B", desc: "Automóviles" },
                { id: "C", icon: "🏍️", label: "Clase C", desc: "Motocicletas" },
              ].map(c => (
                <button
                  key={c.id}
                  onClick={() => setClaseSeleccionada(c.id)}
                  style={{
                    ...styles.claseBtn,
                    ...(claseSeleccionada === c.id ? styles.claseBtnActive : {})
                  }}
                >
                  <span style={styles.claseBtnIcon}>{c.icon}</span>
                  <span style={styles.claseBtnLabel}>{c.label}</span>
                  <span style={styles.claseBtnDesc}>{c.desc}</span>
                </button>
              ))}
            </div>
          </div>

          <div style={styles.modosContainer}>
            <button onClick={() => iniciarExamen("examen")} style={styles.modoExamenBtn}>
              <div style={styles.modoBtnInner}>
                <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
                  <circle cx="12" cy="12" r="10"/><path d="M12 6v6l4 2"/>
                </svg>
                <div>
                  <strong style={styles.modoTitle}>Modo Examen</strong>
                  <p style={styles.modoDesc}>35 preguntas · 45 min · Sin ayudas</p>
                </div>
              </div>
            </button>
            <button onClick={() => iniciarExamen("estudio")} style={styles.modoEstudioBtn}>
              <div style={styles.modoBtnInner}>
                <svg width="28" height="28" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round" strokeLinejoin="round">
                  <path d="M2 3h6a4 4 0 0 1 4 4v14a3 3 0 0 0-3-3H2z"/><path d="M22 3h-6a4 4 0 0 0-4 4v14a3 3 0 0 1 3-3h7z"/>
                </svg>
                <div>
                  <strong style={styles.modoTitle}>Modo Aprendizaje</strong>
                  <p style={styles.modoDesc}>Con explicaciones detalladas</p>
                </div>
              </div>
            </button>
          </div>

          <div style={styles.infoCards}>
            <div style={styles.infoCard}>
              <div style={styles.infoCardNum}>35</div>
              <div style={styles.infoCardLabel}>Preguntas</div>
            </div>
            <div style={styles.infoCard}>
              <div style={styles.infoCardNum}>38</div>
              <div style={styles.infoCardLabel}>Puntaje Máx.</div>
            </div>
            <div style={styles.infoCard}>
              <div style={styles.infoCardNum}>33</div>
              <div style={styles.infoCardLabel}>Para aprobar</div>
            </div>
            <div style={styles.infoCard}>
              <div style={{...styles.infoCardNum, fontSize: "1.2rem"}}>×2</div>
              <div style={styles.infoCardLabel}>3 de doble</div>
            </div>
          </div>

          <p style={styles.disclaimer}>
            ⚠️ Este simulador es una herramienta de práctica. No está afiliado a la CONASET ni a ningún organismo gubernamental.
          </p>
        </div>
      </div>
    );
  }

  // ─── PANTALLA DE EXAMEN / ESTUDIO ───────────────────────────────────
  if (pantalla === "examen" || pantalla === "modoEstudio") {
    const pregActual = preguntas[indicePregunta];
    if (!pregActual) return null;
    const respuestaUsuario = respuestas[indicePregunta];
    const respondida = respuestaUsuario !== undefined;
    const totalRespondidas = Object.keys(respuestas).length;
    const progreso = ((totalRespondidas) / TOTAL_PREGUNTAS) * 100;
    const tiempoBajo = tiempoRestante < 300;

    return (
      <div style={styles.app}>
        <style>{globalCSS}</style>
        
        {/* Header */}
        <div style={styles.examHeader}>
          <button onClick={volverInicio} style={styles.backBtn}>
            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2.5" strokeLinecap="round" strokeLinejoin="round">
              <path d="M19 12H5M12 19l-7-7 7-7"/>
            </svg>
          </button>
          <div style={styles.examHeaderCenter}>
            <span style={styles.examHeaderTitle}>
              {modoExamen === "estudio" ? "📖 Aprendizaje" : "📝 Examen"} Clase {claseSeleccionada}
            </span>
          </div>
          {modoExamen === "examen" && (
            <div style={{
              ...styles.timerBadge,
              ...(tiempoBajo ? styles.timerBadgeLow : {})
            }}>
              <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2" strokeLinecap="round">
                <circle cx="12" cy="12" r="10"/><path d="M12 6v6l4 2"/>
              </svg>
              {formatTime(tiempoRestante)}
            </div>
          )}
        </div>

        {/* Progress */}
        <div style={styles.progressContainer}>
          <div style={styles.progressBar}>
            <div style={{...styles.progressFill, width: `${progreso}%`}}/>
          </div>
          <div style={styles.progressText}>
            {totalRespondidas}/{TOTAL_PREGUNTAS} respondidas
          </div>
        </div>

        {/* Navigation dots */}
        <div style={styles.dotsContainer}>
          <button onClick={() => setNavAbierta(!navAbierta)} style={styles.dotsToggle}>
            {navAbierta ? "Ocultar mapa ▲" : "Ver mapa de preguntas ▼"}
          </button>
          {navAbierta && (
            <div style={styles.dotsGrid}>
              {preguntas.map((p, i) => {
                const resp = respuestas[i];
                const esActual = i === indicePregunta;
                let dotStyle = styles.dot;
                if (esActual) dotStyle = {...dotStyle, ...styles.dotActual};
                else if (resp !== undefined) {
                  if (modoExamen === "estudio") {
                    dotStyle = resp === p.correcta 
                      ? {...dotStyle, ...styles.dotCorrecta}
                      : {...dotStyle, ...styles.dotIncorrecta};
                  } else {
                    dotStyle = {...dotStyle, ...styles.dotRespondida};
                  }
                }
                return (
                  <button key={i} style={dotStyle} onClick={() => { setIndicePregunta(i); setMostrarExplicacion(false); setNavAbierta(false); }}>
                    {i + 1}
                    {p.doble && <span style={styles.dotDoble}>×2</span>}
                  </button>
                );
              })}
            </div>
          )}
        </div>

        {/* Question */}
        <div style={styles.questionContainer}>
          <div style={styles.questionMeta}>
            <span style={{
              ...styles.temaBadge,
              backgroundColor: `${TEMA_COLORS[pregActual.tema] || "#6b7280"}18`,
              color: TEMA_COLORS[pregActual.tema] || "#6b7280",
              borderColor: `${TEMA_COLORS[pregActual.tema] || "#6b7280"}40`
            }}>
              {pregActual.tema}
            </span>
            {pregActual.doble && (
              <span style={styles.dobleBadge}>⚡ DOBLE PUNTAJE</span>
            )}
          </div>

          <div style={styles.questionNumber}>Pregunta {indicePregunta + 1} de {TOTAL_PREGUNTAS}</div>
          <h3 style={styles.questionText}>{pregActual.pregunta}</h3>

          <div style={styles.opcionesContainer}>
            {pregActual.opciones.map((opc, idx) => {
              const letra = String.fromCharCode(65 + idx);
              const seleccionada = respuestaUsuario === idx;
              const esCorrecta = idx === pregActual.correcta;
              
              let opcionStyle = {...styles.opcion};
              if (modoExamen === "estudio" && respondida) {
                if (esCorrecta) opcionStyle = {...opcionStyle, ...styles.opcionCorrecta};
                else if (seleccionada && !esCorrecta) opcionStyle = {...opcionStyle, ...styles.opcionIncorrecta};
              } else if (seleccionada) {
                opcionStyle = {...opcionStyle, ...styles.opcionSeleccionada};
              }

              return (
                <button
                  key={idx}
                  style={opcionStyle}
                  onClick={() => seleccionarRespuesta(idx)}
                  disabled={modoExamen === "estudio" && respondida}
                >
                  <span style={{
                    ...styles.opcionLetra,
                    ...(seleccionada ? styles.opcionLetraActive : {}),
                    ...(modoExamen === "estudio" && respondida && esCorrecta ? styles.opcionLetraCorrecta : {}),
                    ...(modoExamen === "estudio" && respondida && seleccionada && !esCorrecta ? styles.opcionLetraIncorrecta : {})
                  }}>
                    {modoExamen === "estudio" && respondida ? (
                      esCorrecta ? "✓" : (seleccionada ? "✗" : letra)
                    ) : letra}
                  </span>
                  <span style={styles.opcionTexto}>{opc}</span>
                </button>
              );
            })}
          </div>

          {/* Explicación modo estudio */}
          {modoExamen === "estudio" && mostrarExplicacion && (
            <div style={styles.explicacionBox}>
              <div style={styles.explicacionHeader}>
                {respuestaUsuario === pregActual.correcta ? "✅ ¡Correcto!" : "❌ Incorrecto"}
              </div>
              <p style={styles.explicacionText}>{pregActual.explicacion}</p>
            </div>
          )}
        </div>

        {/* Navigation */}
        <div style={styles.navButtons}>
          <button onClick={preguntaAnterior} disabled={indicePregunta === 0} style={{...styles.navBtn, ...(indicePregunta === 0 ? styles.navBtnDisabled : {})}}>
            ← Anterior
          </button>
          
          {indicePregunta === preguntas.length - 1 ? (
            <button onClick={terminarExamen} style={styles.finalizarBtn}>
              Finalizar Examen
            </button>
          ) : (
            <button onClick={siguientePregunta} style={styles.navBtnNext}>
              Siguiente →
            </button>
          )}
        </div>
      </div>
    );
  }

  // ─── PANTALLA DE RESULTADOS ─────────────────────────────────────────
  if (pantalla === "resultado") {
    const res = calcularResultado();
    const tiempoUsado = TIEMPO_MAXIMO - tiempoRestante;
    
    return (
      <div style={styles.app}>
        <style>{globalCSS}</style>
        <div style={styles.resultContainer}>
          <div style={{
            ...styles.resultBanner,
            background: res.aprobado 
              ? "linear-gradient(135deg, #059669, #10b981)" 
              : "linear-gradient(135deg, #dc2626, #ef4444)"
          }}>
            <div style={styles.resultIcon}>{res.aprobado ? "🎉" : "📚"}</div>
            <h2 style={styles.resultTitle}>{res.aprobado ? "¡APROBADO!" : "NO APROBADO"}</h2>
            <p style={styles.resultSubtitle}>
              {res.aprobado 
                ? "¡Felicidades! Estás listo para el examen real." 
                : "Sigue practicando, ¡puedes lograrlo!"}
            </p>
          </div>

          <div style={styles.scoreGrid}>
            <div style={styles.scoreCard}>
              <div style={styles.scoreNum}>{res.puntaje}</div>
              <div style={styles.scoreLabel}>Puntaje</div>
              <div style={styles.scoreSub}>de {PUNTAJE_MAXIMO} posibles</div>
            </div>
            <div style={styles.scoreCard}>
              <div style={styles.scoreNum}>{res.correctas}</div>
              <div style={styles.scoreLabel}>Correctas</div>
              <div style={styles.scoreSub}>de {TOTAL_PREGUNTAS} preguntas</div>
            </div>
            <div style={styles.scoreCard}>
              <div style={styles.scoreNum}>{formatTime(tiempoUsado)}</div>
              <div style={styles.scoreLabel}>Tiempo</div>
              <div style={styles.scoreSub}>de 45:00 min</div>
            </div>
            {res.sinResponder > 0 && (
              <div style={{...styles.scoreCard, borderColor: "#f59e0b"}}>
                <div style={{...styles.scoreNum, color: "#f59e0b"}}>{res.sinResponder}</div>
                <div style={styles.scoreLabel}>Sin responder</div>
              </div>
            )}
          </div>

          <div style={styles.temaResultados}>
            <h3 style={styles.temaResultTitle}>Rendimiento por tema</h3>
            {Object.entries(res.porTema).map(([tema, data]) => {
              const pct = Math.round((data.correctas / data.total) * 100);
              return (
                <div key={tema} style={styles.temaRow}>
                  <div style={styles.temaRowHeader}>
                    <span style={{
                      ...styles.temaRowName,
                      color: TEMA_COLORS[tema] || "#6b7280"
                    }}>{tema}</span>
                    <span style={styles.temaRowScore}>{data.correctas}/{data.total}</span>
                  </div>
                  <div style={styles.temaBarBg}>
                    <div style={{
                      ...styles.temaBarFill,
                      width: `${pct}%`,
                      backgroundColor: pct >= 80 ? "#059669" : pct >= 50 ? "#f59e0b" : "#dc2626"
                    }}/>
                  </div>
                </div>
              );
            })}
          </div>

          <div style={styles.resultActions}>
            <button onClick={() => setPantalla("revision")} style={styles.revisionBtn}>
              📋 Revisar respuestas
            </button>
            <button onClick={volverInicio} style={styles.nuevoExamenBtn}>
              🔄 Nuevo examen
            </button>
          </div>
        </div>
      </div>
    );
  }

  // ─── PANTALLA DE REVISIÓN ───────────────────────────────────────────
  if (pantalla === "revision") {
    return (
      <div style={styles.app}>
        <style>{globalCSS}</style>
        <div style={styles.revisionContainer}>
          <div style={styles.revisionHeader}>
            <button onClick={() => setPantalla("resultado")} style={styles.backBtn}>
              <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" strokeWidth="2.5" strokeLinecap="round" strokeLinejoin="round">
                <path d="M19 12H5M12 19l-7-7 7-7"/>
              </svg>
            </button>
            <h2 style={styles.revisionTitle}>Revisión del Examen</h2>
          </div>

          {preguntas.map((p, i) => {
            const resp = respuestas[i];
            const esCorrecta = resp === p.correcta;
            const sinResponder = resp === undefined;

            return (
              <div key={i} style={{
                ...styles.revisionCard,
                borderLeft: `4px solid ${sinResponder ? "#9ca3af" : esCorrecta ? "#059669" : "#dc2626"}`
              }}>
                <div style={styles.revisionCardHeader}>
                  <span style={styles.revisionQNum}>
                    {sinResponder ? "⬜" : esCorrecta ? "✅" : "❌"} Pregunta {i + 1}
                  </span>
                  <div style={{display: "flex", gap: "6px", flexWrap: "wrap"}}>
                    <span style={{
                      ...styles.temaBadgeSmall,
                      backgroundColor: `${TEMA_COLORS[p.tema] || "#6b7280"}18`,
                      color: TEMA_COLORS[p.tema] || "#6b7280"
                    }}>{p.tema}</span>
                    {p.doble && <span style={styles.dobleBadgeSmall}>×2</span>}
                  </div>
                </div>
                <p style={styles.revisionQText}>{p.pregunta}</p>
                <div style={styles.revisionOpciones}>
                  {p.opciones.map((opc, idx) => {
                    const letra = String.fromCharCode(65 + idx);
                    const esLaCorrecta = idx === p.correcta;
                    const esLaElegida = idx === resp;
                    return (
                      <div key={idx} style={{
                        ...styles.revisionOpcion,
                        ...(esLaCorrecta ? styles.revisionOpcionCorrecta : {}),
                        ...(esLaElegida && !esLaCorrecta ? styles.revisionOpcionIncorrecta : {})
                      }}>
                        <span style={{
                          ...styles.revisionOpcionLetra,
                          ...(esLaCorrecta ? {background: "#059669", color: "#fff"} : {}),
                          ...(esLaElegida && !esLaCorrecta ? {background: "#dc2626", color: "#fff"} : {})
                        }}>{esLaCorrecta ? "✓" : (esLaElegida ? "✗" : letra)}</span>
                        <span>{opc}</span>
                      </div>
                    );
                  })}
                </div>
                <div style={styles.revisionExplicacion}>
                  <strong>Explicación:</strong> {p.explicacion}
                </div>
              </div>
            );
          })}

          <button onClick={volverInicio} style={{...styles.nuevoExamenBtn, margin: "24px auto", display: "block"}}>
            🔄 Nuevo examen
          </button>
        </div>
      </div>
    );
  }

  return null;
}

// ─── GLOBAL CSS ───────────────────────────────────────────────────────
const globalCSS = `
  @import url('https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,300;0,9..40,400;0,9..40,500;0,9..40,600;0,9..40,700&family=JetBrains+Mono:wght@400;600&display=swap');
  
  * { box-sizing: border-box; margin: 0; padding: 0; }
  
  button { cursor: pointer; font-family: 'DM Sans', sans-serif; }
  button:disabled { cursor: not-allowed; opacity: 0.5; }
  
  @keyframes fadeIn {
    from { opacity: 0; transform: translateY(8px); }
    to { opacity: 1; transform: translateY(0); }
  }
  
  @keyframes slideUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }
  
  @keyframes pulse {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.6; }
  }

  @keyframes shimmer {
    0% { background-position: -200% center; }
    100% { background-position: 200% center; }
  }
`;

// ─── STYLES ───────────────────────────────────────────────────────────
const styles = {
  app: {
    fontFamily: "'DM Sans', sans-serif",
    background: "#f8fafc",
    minHeight: "100vh",
    color: "#1e293b",
    maxWidth: "100%",
    overflow: "hidden"
  },

  // INICIO
  inicioContainer: {
    maxWidth: "600px",
    margin: "0 auto",
    padding: "24px 16px 40px",
    animation: "fadeIn 0.5s ease"
  },
  heroSection: {
    textAlign: "center",
    padding: "32px 0 24px"
  },
  logoBadge: {
    display: "inline-flex",
    alignItems: "center",
    justifyContent: "center",
    width: "72px",
    height: "72px",
    borderRadius: "20px",
    background: "linear-gradient(135deg, #1e293b, #334155)",
    boxShadow: "0 8px 32px rgba(30,41,59,0.3)",
    marginBottom: "20px"
  },
  heroTitle: {
    fontSize: "1.75rem",
    fontWeight: "700",
    color: "#0f172a",
    letterSpacing: "-0.02em",
    lineHeight: "1.2"
  },
  heroSubtitle: {
    fontSize: "1rem",
    fontWeight: "500",
    color: "#64748b",
    marginTop: "4px"
  },
  heroDesc: {
    fontSize: "0.875rem",
    color: "#94a3b8",
    marginTop: "12px",
    lineHeight: "1.5",
    maxWidth: "440px",
    marginLeft: "auto",
    marginRight: "auto"
  },

  // Selector de clase
  claseSelector: {
    marginTop: "28px"
  },
  claseSelectorLabel: {
    fontSize: "0.8rem",
    fontWeight: "600",
    color: "#64748b",
    textTransform: "uppercase",
    letterSpacing: "0.05em",
    marginBottom: "10px",
    textAlign: "center"
  },
  claseButtons: {
    display: "flex",
    gap: "12px",
    justifyContent: "center"
  },
  claseBtn: {
    flex: "1",
    maxWidth: "180px",
    padding: "16px 12px",
    border: "2px solid #e2e8f0",
    borderRadius: "14px",
    background: "#fff",
    display: "flex",
    flexDirection: "column",
    alignItems: "center",
    gap: "4px",
    transition: "all 0.2s",
    cursor: "pointer"
  },
  claseBtnActive: {
    borderColor: "#f59e0b",
    background: "#fffbeb",
    boxShadow: "0 0 0 3px rgba(245,158,11,0.15)"
  },
  claseBtnIcon: { fontSize: "1.8rem" },
  claseBtnLabel: { fontSize: "0.95rem", fontWeight: "700", color: "#0f172a" },
  claseBtnDesc: { fontSize: "0.75rem", color: "#94a3b8" },

  // Modos
  modosContainer: {
    display: "flex",
    flexDirection: "column",
    gap: "12px",
    marginTop: "28px"
  },
  modoExamenBtn: {
    width: "100%",
    padding: "18px 20px",
    border: "none",
    borderRadius: "14px",
    background: "linear-gradient(135deg, #1e293b, #334155)",
    color: "#fff",
    textAlign: "left",
    transition: "transform 0.15s",
    boxShadow: "0 4px 20px rgba(30,41,59,0.25)"
  },
  modoEstudioBtn: {
    width: "100%",
    padding: "18px 20px",
    border: "2px solid #e2e8f0",
    borderRadius: "14px",
    background: "#fff",
    color: "#1e293b",
    textAlign: "left",
    transition: "transform 0.15s"
  },
  modoBtnInner: {
    display: "flex",
    alignItems: "center",
    gap: "14px"
  },
  modoTitle: {
    fontSize: "1rem",
    display: "block"
  },
  modoDesc: {
    fontSize: "0.8rem",
    opacity: 0.7,
    marginTop: "2px"
  },

  // Info cards
  infoCards: {
    display: "grid",
    gridTemplateColumns: "repeat(4, 1fr)",
    gap: "10px",
    marginTop: "28px"
  },
  infoCard: {
    textAlign: "center",
    padding: "14px 8px",
    background: "#fff",
    borderRadius: "12px",
    border: "1px solid #e2e8f0"
  },
  infoCardNum: {
    fontSize: "1.5rem",
    fontWeight: "700",
    color: "#f59e0b",
    fontFamily: "'JetBrains Mono', monospace"
  },
  infoCardLabel: {
    fontSize: "0.7rem",
    color: "#94a3b8",
    marginTop: "2px",
    fontWeight: "500"
  },

  disclaimer: {
    fontSize: "0.72rem",
    color: "#94a3b8",
    textAlign: "center",
    marginTop: "28px",
    lineHeight: "1.5"
  },

  // EXAMEN HEADER
  examHeader: {
    display: "flex",
    alignItems: "center",
    justifyContent: "space-between",
    padding: "12px 16px",
    background: "#fff",
    borderBottom: "1px solid #e2e8f0",
    position: "sticky",
    top: 0,
    zIndex: 100
  },
  backBtn: {
    background: "none",
    border: "none",
    color: "#64748b",
    padding: "6px",
    borderRadius: "8px",
    display: "flex",
    alignItems: "center"
  },
  examHeaderCenter: {
    flex: 1,
    textAlign: "center"
  },
  examHeaderTitle: {
    fontSize: "0.85rem",
    fontWeight: "600",
    color: "#475569"
  },
  timerBadge: {
    display: "flex",
    alignItems: "center",
    gap: "6px",
    padding: "6px 12px",
    borderRadius: "20px",
    background: "#f1f5f9",
    fontSize: "0.85rem",
    fontWeight: "600",
    fontFamily: "'JetBrains Mono', monospace",
    color: "#334155"
  },
  timerBadgeLow: {
    background: "#fef2f2",
    color: "#dc2626",
    animation: "pulse 1s ease infinite"
  },

  // PROGRESS
  progressContainer: {
    padding: "8px 16px",
    background: "#fff"
  },
  progressBar: {
    height: "4px",
    borderRadius: "2px",
    background: "#e2e8f0",
    overflow: "hidden"
  },
  progressFill: {
    height: "100%",
    borderRadius: "2px",
    background: "linear-gradient(90deg, #f59e0b, #eab308)",
    transition: "width 0.4s ease"
  },
  progressText: {
    fontSize: "0.72rem",
    color: "#94a3b8",
    textAlign: "right",
    marginTop: "4px"
  },

  // DOTS NAV
  dotsContainer: {
    padding: "0 16px 8px",
    background: "#fff",
    borderBottom: "1px solid #e2e8f0"
  },
  dotsToggle: {
    background: "none",
    border: "none",
    color: "#64748b",
    fontSize: "0.75rem",
    fontWeight: "500",
    padding: "4px 0",
    width: "100%",
    textAlign: "center"
  },
  dotsGrid: {
    display: "grid",
    gridTemplateColumns: "repeat(7, 1fr)",
    gap: "6px",
    padding: "10px 0",
    animation: "fadeIn 0.2s ease"
  },
  dot: {
    width: "100%",
    aspectRatio: "1",
    borderRadius: "8px",
    border: "1.5px solid #e2e8f0",
    background: "#fff",
    fontSize: "0.7rem",
    fontWeight: "600",
    color: "#94a3b8",
    display: "flex",
    flexDirection: "column",
    alignItems: "center",
    justifyContent: "center",
    position: "relative",
    lineHeight: "1"
  },
  dotActual: {
    borderColor: "#f59e0b",
    background: "#fffbeb",
    color: "#b45309",
    boxShadow: "0 0 0 2px rgba(245,158,11,0.2)"
  },
  dotRespondida: {
    background: "#f1f5f9",
    borderColor: "#94a3b8",
    color: "#475569"
  },
  dotCorrecta: {
    background: "#f0fdf4",
    borderColor: "#059669",
    color: "#059669"
  },
  dotIncorrecta: {
    background: "#fef2f2",
    borderColor: "#dc2626",
    color: "#dc2626"
  },
  dotDoble: {
    position: "absolute",
    top: "-3px",
    right: "-3px",
    fontSize: "0.5rem",
    background: "#dc2626",
    color: "#fff",
    borderRadius: "4px",
    padding: "1px 3px",
    fontWeight: "700"
  },

  // QUESTION
  questionContainer: {
    padding: "20px 16px",
    maxWidth: "600px",
    margin: "0 auto",
    animation: "fadeIn 0.3s ease"
  },
  questionMeta: {
    display: "flex",
    alignItems: "center",
    gap: "8px",
    flexWrap: "wrap",
    marginBottom: "12px"
  },
  temaBadge: {
    fontSize: "0.72rem",
    fontWeight: "600",
    padding: "4px 10px",
    borderRadius: "6px",
    border: "1px solid"
  },
  dobleBadge: {
    fontSize: "0.72rem",
    fontWeight: "700",
    padding: "4px 10px",
    borderRadius: "6px",
    background: "linear-gradient(135deg, #dc2626, #ef4444)",
    color: "#fff",
    letterSpacing: "0.02em"
  },
  questionNumber: {
    fontSize: "0.75rem",
    fontWeight: "500",
    color: "#94a3b8",
    marginBottom: "6px"
  },
  questionText: {
    fontSize: "1.05rem",
    fontWeight: "600",
    color: "#0f172a",
    lineHeight: "1.5",
    marginBottom: "20px"
  },

  // OPCIONES
  opcionesContainer: {
    display: "flex",
    flexDirection: "column",
    gap: "10px"
  },
  opcion: {
    display: "flex",
    alignItems: "flex-start",
    gap: "12px",
    padding: "14px 16px",
    border: "2px solid #e2e8f0",
    borderRadius: "12px",
    background: "#fff",
    textAlign: "left",
    transition: "all 0.15s",
    width: "100%",
    fontSize: "0.9rem",
    lineHeight: "1.4",
    color: "#334155"
  },
  opcionSeleccionada: {
    borderColor: "#f59e0b",
    background: "#fffbeb",
    boxShadow: "0 0 0 3px rgba(245,158,11,0.12)"
  },
  opcionCorrecta: {
    borderColor: "#059669",
    background: "#f0fdf4"
  },
  opcionIncorrecta: {
    borderColor: "#dc2626",
    background: "#fef2f2"
  },
  opcionLetra: {
    minWidth: "28px",
    height: "28px",
    borderRadius: "8px",
    display: "flex",
    alignItems: "center",
    justifyContent: "center",
    fontSize: "0.8rem",
    fontWeight: "700",
    background: "#f1f5f9",
    color: "#64748b",
    flexShrink: 0
  },
  opcionLetraActive: {
    background: "#f59e0b",
    color: "#fff"
  },
  opcionLetraCorrecta: {
    background: "#059669",
    color: "#fff"
  },
  opcionLetraIncorrecta: {
    background: "#dc2626",
    color: "#fff"
  },
  opcionTexto: {
    paddingTop: "3px"
  },

  // EXPLICACIÓN
  explicacionBox: {
    marginTop: "20px",
    padding: "16px",
    borderRadius: "12px",
    background: "#f0fdf4",
    border: "1px solid #bbf7d0",
    animation: "slideUp 0.3s ease"
  },
  explicacionHeader: {
    fontSize: "0.9rem",
    fontWeight: "700",
    marginBottom: "8px"
  },
  explicacionText: {
    fontSize: "0.85rem",
    color: "#334155",
    lineHeight: "1.6"
  },

  // NAV BUTTONS
  navButtons: {
    display: "flex",
    gap: "10px",
    padding: "16px",
    maxWidth: "600px",
    margin: "0 auto"
  },
  navBtn: {
    flex: 1,
    padding: "12px",
    border: "2px solid #e2e8f0",
    borderRadius: "12px",
    background: "#fff",
    fontSize: "0.85rem",
    fontWeight: "600",
    color: "#64748b"
  },
  navBtnDisabled: { opacity: 0.4 },
  navBtnNext: {
    flex: 1,
    padding: "12px",
    border: "none",
    borderRadius: "12px",
    background: "#1e293b",
    color: "#fff",
    fontSize: "0.85rem",
    fontWeight: "600"
  },
  finalizarBtn: {
    flex: 1,
    padding: "12px",
    border: "none",
    borderRadius: "12px",
    background: "linear-gradient(135deg, #f59e0b, #eab308)",
    color: "#1e293b",
    fontSize: "0.85rem",
    fontWeight: "700",
    boxShadow: "0 4px 16px rgba(245,158,11,0.3)"
  },

  // RESULTADOS
  resultContainer: {
    maxWidth: "600px",
    margin: "0 auto",
    padding: "0 16px 40px",
    animation: "fadeIn 0.5s ease"
  },
  resultBanner: {
    textAlign: "center",
    padding: "36px 20px",
    borderRadius: "0 0 24px 24px",
    color: "#fff"
  },
  resultIcon: { fontSize: "3rem", marginBottom: "8px" },
  resultTitle: {
    fontSize: "1.8rem",
    fontWeight: "800",
    letterSpacing: "-0.02em"
  },
  resultSubtitle: {
    fontSize: "0.9rem",
    opacity: 0.9,
    marginTop: "4px"
  },
  scoreGrid: {
    display: "grid",
    gridTemplateColumns: "repeat(3, 1fr)",
    gap: "10px",
    marginTop: "20px"
  },
  scoreCard: {
    textAlign: "center",
    padding: "16px 8px",
    background: "#fff",
    borderRadius: "14px",
    border: "1px solid #e2e8f0",
    boxShadow: "0 2px 8px rgba(0,0,0,0.04)"
  },
  scoreNum: {
    fontSize: "1.5rem",
    fontWeight: "800",
    color: "#0f172a",
    fontFamily: "'JetBrains Mono', monospace"
  },
  scoreLabel: {
    fontSize: "0.75rem",
    fontWeight: "600",
    color: "#64748b",
    marginTop: "2px"
  },
  scoreSub: {
    fontSize: "0.68rem",
    color: "#94a3b8",
    marginTop: "1px"
  },

  // TEMA RESULTADOS
  temaResultados: {
    marginTop: "24px",
    background: "#fff",
    borderRadius: "14px",
    border: "1px solid #e2e8f0",
    padding: "20px"
  },
  temaResultTitle: {
    fontSize: "0.9rem",
    fontWeight: "700",
    color: "#0f172a",
    marginBottom: "16px"
  },
  temaRow: {
    marginBottom: "14px"
  },
  temaRowHeader: {
    display: "flex",
    justifyContent: "space-between",
    marginBottom: "4px"
  },
  temaRowName: {
    fontSize: "0.8rem",
    fontWeight: "600"
  },
  temaRowScore: {
    fontSize: "0.8rem",
    fontWeight: "600",
    color: "#475569",
    fontFamily: "'JetBrains Mono', monospace"
  },
  temaBarBg: {
    height: "6px",
    borderRadius: "3px",
    background: "#f1f5f9",
    overflow: "hidden"
  },
  temaBarFill: {
    height: "100%",
    borderRadius: "3px",
    transition: "width 0.6s ease"
  },

  // RESULT ACTIONS
  resultActions: {
    display: "flex",
    gap: "10px",
    marginTop: "24px"
  },
  revisionBtn: {
    flex: 1,
    padding: "14px",
    border: "2px solid #e2e8f0",
    borderRadius: "12px",
    background: "#fff",
    fontSize: "0.85rem",
    fontWeight: "600",
    color: "#475569"
  },
  nuevoExamenBtn: {
    flex: 1,
    padding: "14px",
    border: "none",
    borderRadius: "12px",
    background: "linear-gradient(135deg, #1e293b, #334155)",
    color: "#fff",
    fontSize: "0.85rem",
    fontWeight: "600",
    boxShadow: "0 4px 16px rgba(30,41,59,0.2)"
  },

  // REVISIÓN
  revisionContainer: {
    maxWidth: "600px",
    margin: "0 auto",
    padding: "0 16px 40px"
  },
  revisionHeader: {
    display: "flex",
    alignItems: "center",
    gap: "12px",
    padding: "16px 0",
    position: "sticky",
    top: 0,
    background: "#f8fafc",
    zIndex: 10
  },
  revisionTitle: {
    fontSize: "1.1rem",
    fontWeight: "700",
    color: "#0f172a"
  },
  revisionCard: {
    background: "#fff",
    borderRadius: "14px",
    border: "1px solid #e2e8f0",
    padding: "18px",
    marginBottom: "14px",
    animation: "fadeIn 0.3s ease"
  },
  revisionCardHeader: {
    display: "flex",
    justifyContent: "space-between",
    alignItems: "flex-start",
    marginBottom: "10px",
    flexWrap: "wrap",
    gap: "6px"
  },
  revisionQNum: {
    fontSize: "0.85rem",
    fontWeight: "700",
    color: "#0f172a"
  },
  temaBadgeSmall: {
    fontSize: "0.65rem",
    fontWeight: "600",
    padding: "2px 8px",
    borderRadius: "5px"
  },
  dobleBadgeSmall: {
    fontSize: "0.65rem",
    fontWeight: "700",
    padding: "2px 8px",
    borderRadius: "5px",
    background: "#dc2626",
    color: "#fff"
  },
  revisionQText: {
    fontSize: "0.9rem",
    fontWeight: "500",
    color: "#1e293b",
    lineHeight: "1.5",
    marginBottom: "12px"
  },
  revisionOpciones: {
    display: "flex",
    flexDirection: "column",
    gap: "6px",
    marginBottom: "12px"
  },
  revisionOpcion: {
    display: "flex",
    alignItems: "flex-start",
    gap: "8px",
    padding: "8px 10px",
    borderRadius: "8px",
    fontSize: "0.82rem",
    color: "#475569",
    lineHeight: "1.4",
    background: "#f8fafc"
  },
  revisionOpcionCorrecta: {
    background: "#f0fdf4",
    color: "#065f46",
    fontWeight: "500"
  },
  revisionOpcionIncorrecta: {
    background: "#fef2f2",
    color: "#991b1b",
    textDecoration: "line-through",
    opacity: 0.8
  },
  revisionOpcionLetra: {
    minWidth: "22px",
    height: "22px",
    borderRadius: "6px",
    display: "flex",
    alignItems: "center",
    justifyContent: "center",
    fontSize: "0.7rem",
    fontWeight: "700",
    background: "#e2e8f0",
    color: "#64748b",
    flexShrink: 0
  },
  revisionExplicacion: {
    fontSize: "0.8rem",
    color: "#475569",
    lineHeight: "1.6",
    padding: "12px",
    background: "#f8fafc",
    borderRadius: "8px",
    borderLeft: "3px solid #f59e0b"
  }
};
