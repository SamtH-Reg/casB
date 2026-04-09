import { useState, useEffect, useCallback, useRef } from "react";

// ═══════════════════════════════════════════════════════════════════════
// AUTOESCUELA CHILE - Simulador Examen CONASET Clase B
// Con temarios ilustrados, progreso del alumno y refuerzo adaptativo
// ═══════════════════════════════════════════════════════════════════════

// ── SVG ILLUSTRATIONS (inline, no external deps) ─────────────────────
const SVG = {
  // Señales de tránsito
  pare: `<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"><polygon points="50,5 85,20 95,55 80,88 50,98 20,88 5,55 15,20" fill="#cc0000" stroke="#fff" stroke-width="3"/><text x="50" y="58" text-anchor="middle" fill="#fff" font-size="20" font-weight="bold" font-family="sans-serif">PARE</text></svg>`,
  cedaPaso: `<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"><polygon points="50,90 5,10 95,10" fill="#fff" stroke="#cc0000" stroke-width="5"/><text x="50" y="42" text-anchor="middle" fill="#333" font-size="11" font-weight="bold" font-family="sans-serif">CEDA</text><text x="50" y="58" text-anchor="middle" fill="#333" font-size="11" font-weight="bold" font-family="sans-serif">EL PASO</text></svg>`,
  velocidad: `<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"><circle cx="50" cy="50" r="44" fill="#fff" stroke="#cc0000" stroke-width="6"/><text x="50" y="58" text-anchor="middle" fill="#333" font-size="28" font-weight="bold" font-family="sans-serif">60</text></svg>`,
  noEntrar: `<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"><circle cx="50" cy="50" r="44" fill="#cc0000" stroke="#fff" stroke-width="3"/><rect x="15" y="40" width="70" height="20" rx="3" fill="#fff"/></svg>`,
  noAdelantar: `<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"><circle cx="50" cy="50" r="44" fill="#fff" stroke="#cc0000" stroke-width="6"/><line x1="15" y1="15" x2="85" y2="85" stroke="#cc0000" stroke-width="6"/><circle cx="38" cy="50" r="14" fill="none" stroke="#333" stroke-width="3"/><circle cx="62" cy="50" r="14" fill="none" stroke="#cc0000" stroke-width="3"/></svg>`,
  curva: `<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"><rect x="10" y="10" width="80" height="80" rx="4" fill="#f7c948" stroke="#333" stroke-width="2" transform="rotate(45 50 50)"/><path d="M35 70 Q35 35 65 35" fill="none" stroke="#333" stroke-width="6" stroke-linecap="round"/><polygon points="65,25 75,35 65,40" fill="#333"/></svg>`,
  peatones: `<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"><rect x="10" y="10" width="80" height="80" rx="4" fill="#f7c948" stroke="#333" stroke-width="2" transform="rotate(45 50 50)"/><circle cx="50" cy="30" r="7" fill="#333"/><line x1="50" y1="37" x2="50" y2="58" stroke="#333" stroke-width="4"/><line x1="50" y1="42" x2="38" y2="52" stroke="#333" stroke-width="3"/><line x1="50" y1="42" x2="62" y2="52" stroke="#333" stroke-width="3"/><line x1="50" y1="58" x2="38" y2="75" stroke="#333" stroke-width="3"/><line x1="50" y1="58" x2="62" y2="75" stroke="#333" stroke-width="3"/></svg>`,
  info: `<svg viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg"><rect x="8" y="20" width="84" height="60" rx="6" fill="#006b3f" stroke="#fff" stroke-width="3"/><text x="50" y="48" text-anchor="middle" fill="#fff" font-size="12" font-weight="bold" font-family="sans-serif">Santiago</text><text x="50" y="65" text-anchor="middle" fill="#fff" font-size="11" font-family="sans-serif">120 km →</text></svg>`,
  // Vehículo
  auto: `<svg viewBox="0 0 120 60" xmlns="http://www.w3.org/2000/svg"><rect x="10" y="25" width="100" height="25" rx="5" fill="#3b82f6"/><path d="M30 25 Q35 8 55 8 L75 8 Q85 8 90 25" fill="#60a5fa"/><rect x="38" y="11" width="15" height="13" rx="2" fill="#bfdbfe" opacity="0.7"/><rect x="58" y="11" width="15" height="13" rx="2" fill="#bfdbfe" opacity="0.7"/><circle cx="30" cy="52" r="8" fill="#1e293b"/><circle cx="30" cy="52" r="4" fill="#64748b"/><circle cx="90" cy="52" r="8" fill="#1e293b"/><circle cx="90" cy="52" r="4" fill="#64748b"/><rect x="95" y="30" width="12" height="6" rx="2" fill="#fbbf24"/><rect x="5" y="30" width="12" height="6" rx="2" fill="#ef4444"/></svg>`,
  // Tablero
  tablero: `<svg viewBox="0 0 140 70" xmlns="http://www.w3.org/2000/svg"><rect x="5" y="5" width="130" height="60" rx="8" fill="#1e293b"/><circle cx="35" cy="35" r="18" fill="none" stroke="#475569" stroke-width="2"/><line x1="35" y1="35" x2="35" y2="20" stroke="#ef4444" stroke-width="2"/><text x="35" y="60" text-anchor="middle" fill="#94a3b8" font-size="7" font-family="sans-serif">RPM</text><circle cx="75" cy="35" r="18" fill="none" stroke="#475569" stroke-width="2"/><text x="75" y="40" text-anchor="middle" fill="#22c55e" font-size="14" font-weight="bold" font-family="sans-serif">80</text><text x="75" y="60" text-anchor="middle" fill="#94a3b8" font-size="7" font-family="sans-serif">km/h</text><rect x="100" y="20" width="25" height="8" rx="2" fill="#1e293b" stroke="#475569" stroke-width="1"/><rect x="100" y="20" width="15" height="8" rx="2" fill="#22c55e"/><text x="112" y="42" text-anchor="middle" fill="#94a3b8" font-size="6" font-family="sans-serif">FUEL</text><circle cx="108" cy="52" r="4" fill="#ef4444"/><circle cx="120" cy="52" r="4" fill="#fbbf24"/></svg>`,
  // Neumático
  neumatico: `<svg viewBox="0 0 80 80" xmlns="http://www.w3.org/2000/svg"><circle cx="40" cy="40" r="35" fill="#1e293b"/><circle cx="40" cy="40" r="28" fill="#334155"/><circle cx="40" cy="40" r="12" fill="#94a3b8"/><circle cx="40" cy="40" r="6" fill="#64748b"/><line x1="40" y1="12" x2="40" y2="5" stroke="#1e293b" stroke-width="3"/><line x1="40" y1="68" x2="40" y2="75" stroke="#1e293b" stroke-width="3"/><line x1="12" y1="40" x2="5" y2="40" stroke="#1e293b" stroke-width="3"/><line x1="68" y1="40" x2="75" y2="40" stroke="#1e293b" stroke-width="3"/></svg>`,
  // Alcohol
  alcohol: `<svg viewBox="0 0 80 90" xmlns="http://www.w3.org/2000/svg"><rect x="25" y="5" width="30" height="40" rx="3" fill="none" stroke="#dc2626" stroke-width="3"/><rect x="28" y="25" width="24" height="18" rx="1" fill="#fca5a5" opacity="0.6"/><rect x="30" y="45" width="6" height="30" fill="#dc2626"/><rect x="44" y="45" width="6" height="30" fill="#dc2626"/><line x1="15" y1="10" x2="65" y2="80" stroke="#dc2626" stroke-width="5" stroke-linecap="round"/><circle cx="40" cy="45" r="35" fill="none" stroke="#dc2626" stroke-width="3"/></svg>`,
  // SRI (silla infantil)
  sri: `<svg viewBox="0 0 80 90" xmlns="http://www.w3.org/2000/svg"><path d="M20 85 L20 35 Q20 15 40 15 Q60 15 60 35 L60 85" fill="none" stroke="#f59e0b" stroke-width="4"/><rect x="22" y="35" width="36" height="48" rx="8" fill="#fef3c7" stroke="#f59e0b" stroke-width="2"/><circle cx="40" cy="28" r="8" fill="#fbbf24"/><line x1="32" y1="50" x2="48" y2="50" stroke="#f59e0b" stroke-width="3" stroke-linecap="round"/><line x1="40" y1="42" x2="40" y2="65" stroke="#f59e0b" stroke-width="3" stroke-linecap="round"/></svg>`,
  // Cinturón
  cinturon: `<svg viewBox="0 0 80 90" xmlns="http://www.w3.org/2000/svg"><circle cx="40" cy="22" r="10" fill="none" stroke="#0891b2" stroke-width="3"/><line x1="40" y1="32" x2="40" y2="60" stroke="#0891b2" stroke-width="3"/><path d="M25 42 L40 60 L55 42" fill="none" stroke="#ef4444" stroke-width="4" stroke-linecap="round" stroke-linejoin="round"/><rect x="35" y="58" width="10" height="6" rx="2" fill="#ef4444"/><line x1="40" y1="64" x2="40" y2="80" stroke="#94a3b8" stroke-width="2"/></svg>`,
  // Efecto túnel
  efectoTunel: `<svg viewBox="0 0 120 70" xmlns="http://www.w3.org/2000/svg"><rect x="0" y="0" width="120" height="70" fill="#1e293b"/><ellipse cx="60" cy="35" rx="55" ry="30" fill="none" stroke="#475569" stroke-width="1.5" stroke-dasharray="4,3"/><ellipse cx="60" cy="35" rx="40" ry="22" fill="none" stroke="#64748b" stroke-width="1.5" stroke-dasharray="4,3"/><ellipse cx="60" cy="35" rx="20" ry="12" fill="#f59e0b" opacity="0.3"/><ellipse cx="60" cy="35" rx="8" ry="5" fill="#f59e0b" opacity="0.6"/><text x="60" y="65" text-anchor="middle" fill="#94a3b8" font-size="8" font-family="sans-serif">Campo visual reducido</text></svg>`,
  // Lluvia
  lluvia: `<svg viewBox="0 0 100 80" xmlns="http://www.w3.org/2000/svg"><path d="M25 40 Q25 20 50 20 Q65 10 78 25 Q90 25 85 40" fill="#94a3b8"/><line x1="30" y1="50" x2="25" y2="65" stroke="#3b82f6" stroke-width="2" stroke-linecap="round"/><line x1="45" y1="48" x2="40" y2="68" stroke="#3b82f6" stroke-width="2" stroke-linecap="round"/><line x1="60" y1="50" x2="55" y2="65" stroke="#3b82f6" stroke-width="2" stroke-linecap="round"/><line x1="75" y1="48" x2="70" y2="63" stroke="#3b82f6" stroke-width="2" stroke-linecap="round"/><line x1="38" y1="55" x2="33" y2="70" stroke="#3b82f6" stroke-width="2" stroke-linecap="round"/><line x1="68" y1="52" x2="63" y2="72" stroke="#3b82f6" stroke-width="2" stroke-linecap="round"/></svg>`,
  // Primeros auxilios
  primerAux: `<svg viewBox="0 0 80 80" xmlns="http://www.w3.org/2000/svg"><rect x="10" y="10" width="60" height="60" rx="12" fill="#dc2626"/><rect x="32" y="20" width="16" height="40" rx="3" fill="#fff"/><rect x="20" y="32" width="40" height="16" rx="3" fill="#fff"/></svg>`,
  // Logo app
  logo: `<svg viewBox="0 0 50 50" xmlns="http://www.w3.org/2000/svg"><circle cx="25" cy="25" r="23" fill="#0f172a" stroke="#f59e0b" stroke-width="2"/><path d="M15 32 L25 12 L35 32" fill="none" stroke="#f59e0b" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"/><line x1="19" y1="26" x2="31" y2="26" stroke="#f59e0b" stroke-width="2.5" stroke-linecap="round"/><circle cx="25" cy="37" r="2.5" fill="#f59e0b"/></svg>`,
  // Check / X
  check: `<svg viewBox="0 0 24 24" fill="none" stroke="#059669" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="M20 6L9 17l-5-5"/></svg>`,
  x: `<svg viewBox="0 0 24 24" fill="none" stroke="#dc2626" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><line x1="18" y1="6" x2="6" y2="18"/><line x1="6" y1="6" x2="18" y2="18"/></svg>`,
};

function InlineSVG({ svg, size = 60, style = {} }) {
  return <div style={{ width: size, height: size, flexShrink: 0, ...style }} dangerouslySetInnerHTML={{ __html: svg }} />;
}

// ── TEMARIOS COMPLETOS ───────────────────────────────────────────────
const TEMARIOS = [
  {
    id: "convivencia",
    titulo: "Convivencia Vial",
    icono: "🤝",
    color: "#059669",
    descripcion: "Educación vial, respeto y seguridad compartida en las vías",
    ilustracion: SVG.auto,
    contenido: [
      { subtitulo: "¿Qué es la Convivencia Vial?", texto: "Es la interacción armoniosa y segura entre conductores, peatones, ciclistas y todos los usuarios de las vías. Se basa en el respeto mutuo, la solidaridad, la comprensión y la tolerancia.", svg: null },
      { subtitulo: "Educación Vial", texto: "Es la adquisición de valores para la conducción: hábitos positivos, conocimiento de la Ley de Tránsito y de las señales. La meta es eliminar los siniestros de tránsito.", svg: null },
      { subtitulo: "Siniestros vs Accidentes", texto: "En Chile se usa el término 'siniestro' en lugar de 'accidente', porque la mayoría son prevenibles. El 90% se produce por falla humana. Más de 3.000 personas fallecen diariamente en el mundo por esta causa.", svg: null },
      { subtitulo: "Responsabilidad Colectiva", texto: "Conducir bajo los efectos del alcohol o sin cinturón no es una decisión personal: afecta a todos. Los costos médicos, legales y emocionales los paga toda la sociedad.", svg: null },
    ],
    preguntas: [0,1,2,3,4] // índices en PREGUNTAS
  },
  {
    id: "individuo",
    titulo: "El Individuo en el Tránsito",
    icono: "🧠",
    color: "#7c3aed",
    descripcion: "Capacidades del conductor, percepción del riesgo, fatiga y alcohol",
    ilustracion: SVG.alcohol,
    contenido: [
      { subtitulo: "Capacidades del Conductor", texto: "Para conducir de forma segura se necesita: buena visión, capacidad de concentración, velocidad de reacción adecuada y estado emocional estable. Cualquier alteración aumenta el riesgo.", svg: null },
      { subtitulo: "Efectos del Alcohol", texto: "Con 0,3 g/l se configura 'bajo la influencia del alcohol'. Con 0,8 g/l 'estado de ebriedad'. El alcohol deteriora el juicio, la coordinación, el tiempo de reacción y genera falsa confianza.", svg: SVG.alcohol },
      { subtitulo: "Ley Emilia (Ley 20.770)", texto: "Establece penas de cárcel efectiva para quien conduzca en estado de ebriedad y cause lesiones graves o muerte. Si hay siniestro, se presume culpabilidad del conductor ebrio.", svg: null },
      { subtitulo: "Fatiga y Somnolencia", texto: "La fatiga reduce atención, aumenta tiempos de reacción y puede provocar microsueños. Se recomienda descansar cada 2 horas y no conducir más de 4 horas seguidas.", svg: null },
      { subtitulo: "Medicamentos", texto: "Ansiolíticos, antihistamínicos, antidepresivos y otros fármacos pueden producir somnolencia y alterar reflejos. Siempre consultar al médico antes de conducir.", svg: null },
    ],
    preguntas: [5,6,7,8,9]
  },
  {
    id: "vulnerables",
    titulo: "Usuarios Vulnerables",
    icono: "🚶",
    color: "#ea580c",
    descripcion: "Peatones, ciclistas, niños, adultos mayores y personas con discapacidad",
    ilustracion: SVG.peatones,
    contenido: [
      { subtitulo: "¿Quiénes son?", texto: "Peatones, ciclistas, motociclistas, niños, adultos mayores y personas con discapacidad. Representan el 15% de los siniestros pero casi el 40% de las muertes.", svg: SVG.peatones },
      { subtitulo: "Peatones", texto: "Tienen derecho preferente en cruces demarcados. El conductor debe detenerse completamente cuando un peatón cruza por un paso de cebra. Sus movimientos pueden ser impredecibles.", svg: null },
      { subtitulo: "Ciclistas", texto: "La Ley de Convivencia Vial (Ley 21.088) establece mínimo 1,5 metros de distancia lateral al adelantar a un ciclista. Se debe respetar ciclovías y zonas de espera adelantada.", svg: null },
      { subtitulo: "Niños y Adultos Mayores", texto: "Los niños tienen baja percepción del riesgo y pueden aparecer inesperadamente. Los adultos mayores pueden tener movilidad o audición reducida. Ambos requieren precaución extra.", svg: null },
    ],
    preguntas: [10,11,12,13]
  },
  {
    id: "normas",
    titulo: "Normas de Circulación",
    icono: "📜",
    color: "#2563eb",
    descripcion: "Velocidades, adelantamientos, estacionamiento, virajes y prioridades",
    ilustracion: SVG.velocidad,
    contenido: [
      { subtitulo: "Velocidades Máximas", texto: "Zona urbana: 60 km/h. Zona rural: 100 km/h (livianos), 90 km/h (pesados). Autopistas: 120 km/h. Zonas escolares y de hospital: 30 km/h. Siempre prevalece la señalización local.", svg: SVG.velocidad },
      { subtitulo: "Adelantamiento", texto: "Solo donde la señalización lo permita (línea segmentada). Nunca en intersecciones, curvas, puentes, pasos peatonales o túneles. Se adelanta por la izquierda.", svg: null },
      { subtitulo: "Estacionamiento", texto: "Prohibido a menos de 10 metros de esquinas y señales PARE/CEDA. Línea amarilla continua = prohibido estacionar y detenerse. No estacionar en doble fila.", svg: null },
      { subtitulo: "Virajes y Señalización", texto: "Todo viraje debe señalizarse con anticipación mínima de 30m en zona urbana. Usar señalizadores (intermitentes). Verificar espejos y punto ciego antes de maniobrar.", svg: null },
      { subtitulo: "Autopistas", texto: "Si se pasa una salida, continuar hasta la siguiente autorizada. Nunca retroceder ni hacer virajes en U. Velocidad mínima establecida por señalización.", svg: null },
      { subtitulo: "Luces", texto: "En Chile es obligatorio circular con luces bajas encendidas las 24 horas del día, en todas las vías del país, desde el año 2005 (Art. 68 Ley de Tránsito).", svg: null },
    ],
    preguntas: [14,15,16,17,18]
  },
  {
    id: "conduccion",
    titulo: "Conducción Segura",
    icono: "🛡️",
    color: "#0891b2",
    descripcion: "Conducción defensiva, distancias, efecto túnel y condiciones adversas",
    ilustracion: SVG.efectoTunel,
    contenido: [
      { subtitulo: "Conducción Defensiva", texto: "Consiste en anticiparse a las situaciones de riesgo, mantener distancia segura, estar atento al entorno y reaccionar correctamente. Un conductor defensivo prevé lo que otros pueden hacer mal.", svg: null },
      { subtitulo: "Efecto Túnel", texto: "A mayor velocidad, el campo visual lateral se reduce progresivamente. A 65 km/h se ve en un ángulo de 70°. A 130 km/h se reduce a solo 30°, como mirar por un túnel.", svg: SVG.efectoTunel },
      { subtitulo: "Distancia de Frenado", texto: "Al duplicar la velocidad, la distancia de frenado se cuadruplica (energía cinética = ½mv²). La regla de los 3 segundos ayuda a mantener distancia segura de seguimiento.", svg: null },
      { subtitulo: "Zona de Incertidumbre", texto: "Es el espacio alrededor de peatones, ciclistas u otros vehículos donde podrían realizar movimientos impredecibles. Se debe ampliar la distancia al pasar cerca de ellos.", svg: null },
      { subtitulo: "Conducción bajo Lluvia", texto: "Reducir velocidad, aumentar distancia de seguimiento, encender luces bajas. Los neumáticos pierden adherencia en pavimento mojado. Riesgo de aquaplaning.", svg: SVG.lluvia },
      { subtitulo: "Uso del Celular", texto: "Prohibido manipular el celular mientras se conduce. Solo se permite sistema de manos libres. Multa gravísima por infracción (Art. 107 Ley de Tránsito).", svg: null },
    ],
    preguntas: [19,20,21,22,23]
  },
  {
    id: "senales",
    titulo: "Señales de Tránsito",
    icono: "🚦",
    color: "#dc2626",
    descripcion: "Reglamentarias, preventivas, informativas y demarcación horizontal",
    ilustracion: SVG.pare,
    contenido: [
      { subtitulo: "Clasificación", texto: "Las señales verticales se clasifican por su forma: Reglamentarias (circulares), Preventivas (romboidales/diamante) e Informativas (rectangulares). Las señales PARE y CEDA EL PASO son excepciones.", svg: null },
      { subtitulo: "Señales Reglamentarias", texto: "Son de cumplimiento obligatorio. Incluyen prioridad (PARE, CEDA), prohibición (No entrar, No adelantar), restricción (Velocidad máxima) y obligación (Dirección obligatoria). Forma circular, borde rojo.", svg: SVG.pare },
      { subtitulo: "Señales Preventivas", texto: "Advierten sobre peligros o condiciones inusuales: curvas, cruces, peatones, animales, resaltos. Forma de rombo, fondo amarillo con símbolo negro. Se ubican antes del riesgo.", svg: SVG.curva },
      { subtitulo: "Señales Informativas", texto: "Guían al conductor con información de rutas, distancias, servicios y destinos. Forma rectangular, generalmente fondo verde con texto blanco.", svg: SVG.info },
      { subtitulo: "Demarcación Horizontal", texto: "Línea continua: no cruzar. Línea segmentada: permitido cruzar/adelantar. Línea amarilla en solera: prohibido estacionar. Paso cebra: preferencia peatonal.", svg: null },
      { subtitulo: "Nuevas Señales (2021+)", texto: "Zonas 30, preferencia ciclista al virar, zonas de espera adelantada para motos, ciclo calles, vías compartidas peatones-ciclistas.", svg: null },
    ],
    preguntas: [24,25,26,27,28]
  },
  {
    id: "vehiculo",
    titulo: "Conoce tu Vehículo",
    icono: "🔧",
    color: "#4f46e5",
    descripcion: "Panel de instrumentos, frenos, neumáticos, aceite y mecánica básica",
    ilustracion: SVG.tablero,
    contenido: [
      { subtitulo: "Panel de Instrumentos", texto: "Es el medio de comunicación del vehículo. Indicadores de velocidad, RPM, temperatura, combustible y testigos de alerta (aceite, batería, ABS, airbag, etc.).", svg: SVG.tablero },
      { subtitulo: "Sistema de Frenos", texto: "Frenos convencionales y ABS (antibloqueo). El ABS evita que las ruedas se bloqueen al frenar de emergencia, manteniendo el control de la dirección. El líquido de frenos transmite la presión hidráulica.", svg: null },
      { subtitulo: "Neumáticos", texto: "Profundidad mínima del dibujo: 1,6 mm (recomendable 3 mm). Revisar presión cada 500 km o mensualmente, en frío. Neumáticos desgastados aumentan riesgo de aquaplaning.", svg: SVG.neumatico },
      { subtitulo: "Aceite del Motor", texto: "La luz de aceite indica presión insuficiente. Detenerse de inmediato. Cambiar aceite y filtro según recomendaciones del fabricante. Usar aceites certificados.", svg: null },
      { subtitulo: "Batería", texto: "Batería en mal estado dificulta el arranque, especialmente en frío. Verificar estado periódicamente. Controlar bornes y conexiones.", svg: null },
    ],
    preguntas: [29,30,31,32]
  },
  {
    id: "seguridad",
    titulo: "Seguridad Pasiva y SRI",
    icono: "🧒",
    color: "#f59e0b",
    descripcion: "Cinturón, airbag, sistemas de retención infantil y seguridad del vehículo",
    ilustracion: SVG.sri,
    contenido: [
      { subtitulo: "Cinturón de Seguridad", texto: "Obligatorio SIEMPRE para conductor y todos los pasajeros. Cada cinturón es individual. Reduce hasta un 50% el riesgo de muerte en siniestros frontales.", svg: SVG.cinturon },
      { subtitulo: "Airbag", texto: "Es complementario al cinturón, NO lo reemplaza. Sin cinturón ocurre el 'efecto rebote': el airbag empuja el cuerpo violentamente hacia atrás causando lesiones graves.", svg: null },
      { subtitulo: "Sistema de Retención Infantil (SRI)", texto: "Obligatorio para niños. Elegir SRI compatible con el vehículo (anclaje ISOFIX o cinturón) y adecuado al peso/talla del niño. Ley 20.904. Instalarlo en asientos traseros.", svg: SVG.sri },
      { subtitulo: "Preguntas de Doble Puntaje", texto: "En el examen real, las preguntas sobre alcohol, drogas, velocidad y SRI valen doble puntaje (2 puntos cada una). Hay 3 de estas preguntas por examen, sumando un máximo de 38 puntos.", svg: null },
    ],
    preguntas: [33,34]
  },
  {
    id: "emergencias",
    titulo: "Emergencias y Primeros Auxilios",
    icono: "🚑",
    color: "#be185d",
    descripcion: "Conducta PAS, qué hacer ante siniestros y documentación obligatoria",
    ilustracion: SVG.primerAux,
    contenido: [
      { subtitulo: "Conducta PAS", texto: "Proteger (señalizar la zona), Alertar (llamar a 131/132/133) y Socorrer (según capacidad). No mover heridos innecesariamente a menos que haya riesgo vital inmediato.", svg: SVG.primerAux },
      { subtitulo: "Documentación Obligatoria", texto: "Licencia de conducir vigente, permiso de circulación, SOAP (Seguro Obligatorio de Accidentes Personales), revisión técnica al día y certificado de homologación del gas si aplica.", svg: null },
      { subtitulo: "Vehículos de Emergencia", texto: "Ambulancias, bomberos y policía con sirenas y balizas tienen preferencia absoluta. Desplazarse a la derecha y detenerse si es necesario para dejar pasar.", svg: null },
    ],
    preguntas: [35,36]
  },
];

// ── BANCO DE PREGUNTAS ───────────────────────────────────────────────
const PREGUNTAS = [
  // Convivencia Vial (0-4)
  { id:"cv1", tema:"convivencia", pregunta:"¿Qué es la Convivencia Vial?", opciones:["Solo respetar los semáforos","La interacción armoniosa y segura entre todos los usuarios de las vías","Conducir sin exceder la velocidad máxima"], correcta:1, explicacion:"La Convivencia Vial es la interacción armoniosa y segura entre conductores, peatones, ciclistas y todos los usuarios, basada en respeto, solidaridad y tolerancia.", doble:false, svg:null },
  { id:"cv2", tema:"convivencia", pregunta:"¿Por qué se usa el término 'siniestro' en lugar de 'accidente' de tránsito?", opciones:["Porque suena más formal","Porque la mayoría son prevenibles y no casuales","Porque lo exige la ley internacional"], correcta:1, explicacion:"El término 'siniestro' refleja que estos eventos son evitables. El 90% ocurre por falla humana, no son casuales.", doble:false, svg:null },
  { id:"cv3", tema:"convivencia", pregunta:"La Educación Vial busca inculcar:", opciones:["Solo el conocimiento de señales","Valores de respeto, solidaridad, tolerancia y conocimiento de normas","Habilidades mecánicas del vehículo"], correcta:1, explicacion:"La Educación Vial incluye valores para la convivencia, normas de comportamiento (Ley de Tránsito) y conocimiento de señalización.", doble:false, svg:null },
  { id:"cv4", tema:"convivencia", pregunta:"¿Conducir bajo la influencia del alcohol es una decisión personal?", opciones:["Sí, solo afecta al conductor","No, afecta a toda la sociedad","Sí, si no causa siniestros"], correcta:1, explicacion:"No es una decisión personal. Si el conductor sufre un siniestro, los costos médicos, legales y emocionales los paga toda la sociedad.", doble:false, svg:null },
  { id:"cv5", tema:"convivencia", pregunta:"La meta de la Seguridad Vial es:", opciones:["Reducir la velocidad máxima","La eliminación total de los siniestros de tránsito","Aumentar las multas"], correcta:1, explicacion:"La meta de la Seguridad Vial es la eliminación total de los siniestros, partiendo de la reducción y minimización de sus consecuencias.", doble:false, svg:null },
  // Individuo (5-9)
  { id:"in1", tema:"individuo", pregunta:"¿Cuál es el efecto del alcohol sobre la conducción?", opciones:["Mejora la visión nocturna","Se puede presentar comportamiento impulsivo y agresivo","Aumenta la concentración"], correcta:1, explicacion:"El alcohol genera desinhibición, comportamiento impulsivo, agresivo y falsa sensación de seguridad. Deteriora juicio y coordinación.", doble:true, svg:SVG.alcohol },
  { id:"in2", tema:"individuo", pregunta:"Con 0,3 g/l de alcohol en sangre, la Ley establece que:", opciones:["Está en condiciones normales","Se encuentra en estado de ebriedad","Se encuentra bajo la influencia del alcohol"], correcta:2, explicacion:"Con 0,3 g/l = bajo la influencia del alcohol. Con 0,8 g/l = estado de ebriedad. Ambos son sancionados por la Ley de Tránsito.", doble:true, svg:null },
  { id:"in3", tema:"individuo", pregunta:"La Ley Emilia establece penas más severas para:", opciones:["Conductores sin licencia","Conductores ebrios que causen lesiones graves o muerte","No pagar TAG"], correcta:1, explicacion:"La Ley 20.770 (Ley Emilia) impone cárcel efectiva para quien conduzca ebrio y cause lesiones gravísimas o muerte.", doble:true, svg:null },
  { id:"in4", tema:"individuo", pregunta:"Conducir con fatiga o sueño puede provocar:", opciones:["Aumento de concentración","Dificultad para mantener la atención en la conducción","Mejora en tiempos de reacción"], correcta:1, explicacion:"La fatiga reduce atención, aumenta tiempos de reacción y puede provocar microsueños. Descansar cada 2 horas.", doble:false, svg:null },
  { id:"in5", tema:"individuo", pregunta:"¿Qué sustancias además del alcohol alteran la conducción?", opciones:["Determinados medicamentos","Las bebidas gaseosas","El agua mineral"], correcta:0, explicacion:"Ansiolíticos, antihistamínicos, antidepresivos y otros medicamentos pueden producir somnolencia y alterar reflejos.", doble:false, svg:null },
  // Vulnerables (10-13)
  { id:"vu1", tema:"vulnerables", pregunta:"Los usuarios vulnerables representan el 15% de los siniestros pero casi el __% de las muertes:", opciones:["10%","25%","40%"], correcta:2, explicacion:"Los usuarios vulnerables representan el 15% de los siniestros pero casi el 40% de las muertes por su mayor exposición.", doble:false, svg:SVG.peatones },
  { id:"vu2", tema:"vulnerables", pregunta:"Al adelantar a un ciclista, la distancia lateral mínima es:", opciones:["0,5 metros","1,0 metro","1,5 metros"], correcta:2, explicacion:"La Ley 21.088 de Convivencia Vial establece mínimo 1,5 metros de distancia lateral al adelantar a un ciclista.", doble:false, svg:null },
  { id:"vu3", tema:"vulnerables", pregunta:"Cuando un peatón cruza por un paso de cebra, el conductor debe:", opciones:["Detenerse y ceder el paso","Tocar la bocina para alertar","Pasar lo más rápido posible"], correcta:0, explicacion:"Los peatones tienen derecho preferente en cruces demarcados. El conductor debe detenerse completamente (Art. 176).", doble:false, svg:null },
  { id:"vu4", tema:"vulnerables", pregunta:"¿Por qué los conductores jóvenes tienen mayor riesgo?", opciones:["Poseen baja percepción del riesgo","No saben manejar","Conducen vehículos viejos"], correcta:0, explicacion:"Los jóvenes tienden a subestimar riesgos, sobreestimar habilidades y dejarse influir por presión de pares.", doble:false, svg:null },
  // Normas (14-18)
  { id:"no1", tema:"normas", pregunta:"¿Cuál es la velocidad máxima en zona urbana para vehículos livianos?", opciones:["50 km/h","60 km/h","80 km/h"], correcta:1, explicacion:"La velocidad máxima urbana para livianos es 60 km/h, salvo señalización que indique otra (Art. 145 Ley de Tránsito).", doble:false, svg:SVG.velocidad },
  { id:"no2", tema:"normas", pregunta:"¿Dónde se permite adelantar?", opciones:["En zonas rurales exclusivamente","Donde la señalización o demarcación lo permitan","En intersecciones y pasos peatonales"], correcta:1, explicacion:"Solo donde la señalización lo permita (línea segmentada). Nunca en intersecciones, curvas, puentes o pasos peatonales.", doble:false, svg:null },
  { id:"no3", tema:"normas", pregunta:"Si se equivoca de salida en una autopista, debe:", opciones:["Retroceder por la berma","Hacer viraje en U","Continuar hasta la siguiente salida autorizada"], correcta:2, explicacion:"Nunca retroceder ni hacer virajes en U en autopista. Continuar hasta la siguiente salida autorizada (Art. 113).", doble:false, svg:null },
  { id:"no4", tema:"normas", pregunta:"¿A qué distancia mínima de una esquina se prohíbe estacionar?", opciones:["5 metros","10 metros","20 metros"], correcta:1, explicacion:"Se prohíbe estacionar a menos de 10 metros de una esquina y de señales PARE/CEDA EL PASO (Art. 153).", doble:false, svg:null },
  { id:"no5", tema:"normas", pregunta:"El uso de luces bajas durante el día es obligatorio:", opciones:["Solo en carreteras","En todo momento y en todas las vías","Solo cuando llueve"], correcta:1, explicacion:"Desde 2005, es obligatorio circular con luces bajas las 24 horas, en todas las vías del país (Art. 68).", doble:false, svg:null },
  // Conducción (19-23)
  { id:"co1", tema:"conduccion", pregunta:"¿Qué es el 'efecto túnel'?", opciones:["Pérdida del campo visual lateral al aumentar velocidad","Dificultad para ver en túneles oscuros","Efecto de la lluvia en el parabrisas"], correcta:0, explicacion:"El efecto túnel reduce el campo visual lateral con la velocidad. A 130 km/h se reduce a unos 30°.", doble:false, svg:SVG.efectoTunel },
  { id:"co2", tema:"conduccion", pregunta:"Si se duplica la velocidad, la distancia de frenado:", opciones:["Se duplica","Se cuadruplica","Se mantiene igual"], correcta:1, explicacion:"La energía cinética es proporcional al cuadrado de la velocidad. Al duplicar velocidad, la distancia de frenado ×4.", doble:false, svg:null },
  { id:"co3", tema:"conduccion", pregunta:"Un conductor defensivo se caracteriza porque:", opciones:["Reacciona adecuadamente ante imprevistos","Hace maniobras sorpresivas","Conduce bloqueando el tránsito"], correcta:0, explicacion:"La conducción defensiva implica anticiparse a riesgos, mantener distancia segura y reaccionar correctamente.", doble:false, svg:null },
  { id:"co4", tema:"conduccion", pregunta:"Al conducir bajo lluvia intensa, debe:", opciones:["Aumentar velocidad para salir de la zona","Reducir velocidad, aumentar distancia y encender luces","Mantener la misma velocidad"], correcta:1, explicacion:"Bajo lluvia: reducir velocidad, aumentar distancia de seguimiento y encender luces bajas.", doble:false, svg:SVG.lluvia },
  { id:"co5", tema:"conduccion", pregunta:"El uso del celular al conducir:", opciones:["Permitido a baja velocidad","Prohibido, salvo con manos libres","Permitido en autopistas"], correcta:1, explicacion:"Prohibido manipular el celular. Solo manos libres. Multa gravísima (Art. 107 Ley de Tránsito).", doble:false, svg:null },
  // Señales (24-28)
  { id:"se1", tema:"senales", pregunta:"Las señales reglamentarias tienen generalmente forma:", opciones:["Rectangular","Circular","Romboidal"], correcta:1, explicacion:"Reglamentarias = circulares (excepto PARE octógono y CEDA triángulo invertido). Borde rojo, fondo blanco.", doble:false, svg:SVG.pare },
  { id:"se2", tema:"senales", pregunta:"Las señales preventivas tienen forma de:", opciones:["Círculo","Rombo (diamante)","Octágono"], correcta:1, explicacion:"Las preventivas son romboidales (diamante), fondo amarillo, símbolo negro. Advierten sobre peligros en la vía.", doble:false, svg:SVG.curva },
  { id:"se3", tema:"senales", pregunta:"Un triángulo invertido indica:", opciones:["Pare obligatorio","Ceda el paso","Zona de peligro"], correcta:1, explicacion:"El triángulo invertido es la señal CEDA EL PASO. Obliga a reducir velocidad y ceder a la vía preferente.", doble:false, svg:SVG.cedaPaso },
  { id:"se4", tema:"senales", pregunta:"Para ingresar a un cruce con luz verde, debe verificar:", opciones:["Que haya luz amarilla antes","Que exista espacio para no bloquear el cruce","Que no haya paso de cebra"], correcta:1, explicacion:"Antes de ingresar con luz verde, verificar que hay espacio al otro lado para no bloquear la intersección (Art. 131).", doble:false, svg:null },
  { id:"se5", tema:"senales", pregunta:"La línea amarilla continua en la acera significa:", opciones:["Prohibido estacionar y detenerse","Estacionamiento nocturno","Zona de carga y descarga"], correcta:0, explicacion:"Línea amarilla continua = prohibición absoluta de estacionar y detenerse en esa zona.", doble:false, svg:null },
  // Vehículo (29-32)
  { id:"ve1", tema:"vehiculo", pregunta:"¿Qué indica la luz de aceite en el tablero?", opciones:["Combustible bajo","Presión de aceite insuficiente, detenerse","Cambiar aceite de transmisión"], correcta:1, explicacion:"La luz de aceite indica presión insuficiente. Detenerse de inmediato y verificar nivel. Conducir sin aceite destruye el motor.", doble:false, svg:SVG.tablero },
  { id:"ve2", tema:"vehiculo", pregunta:"La función del líquido de frenos es:", opciones:["Lubricar el motor","Transmitir la presión del pedal a las ruedas","Enfriar el escape"], correcta:1, explicacion:"El líquido de frenos es un fluido hidráulico que transmite la fuerza del pedal a las pastillas/zapatas de freno.", doble:false, svg:null },
  { id:"ve3", tema:"vehiculo", pregunta:"Neumáticos desgastados provocan:", opciones:["Mayor agarre en mojado","Menor distancia de frenado","Mayor riesgo de aquaplaning"], correcta:2, explicacion:"Neumáticos desgastados pierden capacidad de evacuar agua. Profundidad mínima legal: 1,6 mm.", doble:false, svg:SVG.neumatico },
  { id:"ve4", tema:"vehiculo", pregunta:"¿Cada cuánto revisar presión de neumáticos?", opciones:["Cada 50.000 km","Cada 500 km o una vez al mes, en frío","Solo cuando se ven desinflados"], correcta:1, explicacion:"Revisar presión cada 500 km o mínimo mensualmente, siempre con neumáticos fríos para lectura correcta.", doble:false, svg:null },
  // Seguridad (33-34)
  { id:"sg1", tema:"seguridad", pregunta:"Al elegir un SRI, lo más importante es:", opciones:["Que esté en oferta","Que sea compatible con el vehículo y adecuado al niño","Que combine con el interior"], correcta:1, explicacion:"El SRI debe ser compatible (ISOFIX o cinturón) y adecuado al peso/talla del niño. Ley 20.904.", doble:true, svg:SVG.sri },
  { id:"sg2", tema:"seguridad", pregunta:"Respecto al cinturón, el conductor debe:", opciones:["Que todos los ocupantes lleven cinturón individual","Solo preocuparse del suyo","Permitir compartir cinturón"], correcta:0, explicacion:"Es responsabilidad del conductor que TODOS los ocupantes usen cinturón individual (Art. 75 bis).", doble:false, svg:SVG.cinturon },
  // Emergencias (35-36)
  { id:"em1", tema:"emergencias", pregunta:"Ante un siniestro, lo primero es aplicar:", opciones:["Mover a los heridos rápido","Conducta PAS: Proteger, Alertar, Socorrer","Continuar si no está involucrado"], correcta:1, explicacion:"PAS: Proteger (señalizar zona), Alertar (131/132/133), Socorrer según capacidad. No mover heridos innecesariamente.", doble:false, svg:SVG.primerAux },
  { id:"em2", tema:"emergencias", pregunta:"Ante un vehículo de emergencia con sirenas:", opciones:["Aumentar velocidad","Continuar normalmente","Ceder paso desplazándose y deteniéndose si es necesario"], correcta:2, explicacion:"Vehículos de emergencia tienen preferencia absoluta. Desplazarse a la derecha y detenerse (Art. 65).", doble:false, svg:null },
  // Extra para completar variedad
  { id:"ex1", tema:"conduccion", pregunta:"¿Qué es la 'zona de incertidumbre'?", opciones:["Área donde otros podrían hacer movimientos impredecibles","Zona sin señalización","Interior del vehículo"], correcta:0, explicacion:"Es el espacio alrededor de otros usuarios donde podrían moverse inesperadamente. Ampliar distancia.", doble:false, svg:null },
  { id:"ex2", tema:"normas", pregunta:"La bocina debe usarse para:", opciones:["Apurar al vehículo delantero","Anunciar estacionamiento","Prevenir un siniestro si es estrictamente necesario"], correcta:2, explicacion:"La bocina es un elemento de seguridad que solo debe usarse para prevenir siniestros (Art. 78).", doble:false, svg:null },
  { id:"ex3", tema:"individuo", pregunta:"¿Por qué el exceso de velocidad es especialmente peligroso?", opciones:["Aumenta distancia de frenado y riesgo de siniestro","Solo afecta peatones","El vehículo consume menos"], correcta:0, explicacion:"Exceso de velocidad: mayor distancia de frenado, menor campo visual, menor tiempo de reacción, peores consecuencias.", doble:true, svg:null },
];

// ── UTILIDADES ─────────────────────────────────────────────────────────
function shuffle(a){const b=[...a];for(let i=b.length-1;i>0;i--){const j=Math.floor(Math.random()*(i+1));[b[i],b[j]]=[b[j],b[i]];}return b;}
function formatTime(s){return`${Math.floor(s/60).toString().padStart(2,"0")}:${(s%60).toString().padStart(2,"0")}`;}

// ═══════════════════════════════════════════════════════════════════════
// COMPONENTE PRINCIPAL
// ═══════════════════════════════════════════════════════════════════════
export default function AutoescuelaChile() {
  const [vista, setVista] = useState("inicio"); // inicio|temario|temarioDetalle|examen|resultado|revision|refuerzo
  const [progreso, setProgreso] = useState({});
  const [loading, setLoading] = useState(true);
  const [temarioActual, setTemarioActual] = useState(null);
  // Examen state
  const [preguntas, setPreguntas] = useState([]);
  const [idx, setIdx] = useState(0);
  const [resp, setResp] = useState({});
  const [timer, setTimer] = useState(2700);
  const [finalizado, setFinalizado] = useState(false);
  const [showExpl, setShowExpl] = useState(false);
  const [modoEx, setModoEx] = useState("examen");
  const [navOpen, setNavOpen] = useState(false);
  const timerRef = useRef(null);
  // Refuerzo state
  const [refuerzoPreguntas, setRefuerzoPreguntas] = useState([]);

  // ── LOAD/SAVE PROGRESS ─────────────────────────────────────────────
  useEffect(() => {
    (async () => {
      try {
        const r = await window.storage.get("autoescuela-progreso");
        if (r && r.value) setProgreso(JSON.parse(r.value));
      } catch(e) { /* first time */ }
      setLoading(false);
    })();
  }, []);

  const saveProgreso = useCallback(async (p) => {
    setProgreso(p);
    try { await window.storage.set("autoescuela-progreso", JSON.stringify(p)); } catch(e) {}
  }, []);

  // ── TIMER ──────────────────────────────────────────────────────────
  useEffect(() => {
    if (vista === "examen" && modoEx === "examen" && !finalizado) {
      timerRef.current = setInterval(() => {
        setTimer(prev => {
          if (prev <= 1) { clearInterval(timerRef.current); setFinalizado(true); setVista("resultado"); return 0; }
          return prev - 1;
        });
      }, 1000);
    }
    return () => clearInterval(timerRef.current);
  }, [vista, modoEx, finalizado]);

  // ── EXAM HELPERS ───────────────────────────────────────────────────
  const iniciarExamen = (modo, preguntasCustom = null) => {
    let qs;
    if (preguntasCustom) {
      qs = shuffle(preguntasCustom).slice(0, Math.min(35, preguntasCustom.length));
    } else {
      const dobles = PREGUNTAS.filter(p => p.doble);
      const normales = PREGUNTAS.filter(p => !p.doble);
      const sd = shuffle(dobles).slice(0, 3);
      const sn = shuffle(normales).slice(0, 32);
      qs = shuffle([...sd, ...sn]);
    }
    setPreguntas(qs);
    setIdx(0); setResp({}); setTimer(2700); setFinalizado(false); setShowExpl(false); setModoEx(modo); setNavOpen(false);
    setVista(modo === "refuerzo" ? "examen" : "examen");
  };

  const seleccionar = (i) => {
    if (finalizado) return;
    if (modoEx === "examen" && resp[idx] !== undefined) return;
    const newResp = { ...resp, [idx]: i };
    setResp(newResp);
    if (modoEx !== "examen") setShowExpl(true);
  };

  const calcResult = () => {
    let correctas=0, puntaje=0, porTema={}, erroresTema={};
    preguntas.forEach((p,i)=>{
      if(!porTema[p.tema]) porTema[p.tema]={c:0,t:0};
      porTema[p.tema].t++;
      if(resp[i]===p.correcta){correctas++;puntaje+=p.doble?2:1;porTema[p.tema].c++;}
      else {
        if(!erroresTema[p.tema]) erroresTema[p.tema]=[];
        erroresTema[p.tema].push(i);
      }
    });
    const sinResp = preguntas.length - Object.keys(resp).length;
    return { correctas, puntaje, porTema, sinResp, aprobado: puntaje >= 33, erroresTema };
  };

  const terminar = () => {
    clearInterval(timerRef.current);
    setFinalizado(true);
    // Save progress
    const res = calcResult();
    const newProg = { ...progreso };
    if (!newProg.examenes) newProg.examenes = [];
    newProg.examenes.push({
      fecha: new Date().toISOString(),
      puntaje: res.puntaje,
      correctas: res.correctas,
      total: preguntas.length,
      aprobado: res.aprobado,
      porTema: res.porTema,
    });
    // Track weak topics
    if (!newProg.erroresPorTema) newProg.erroresPorTema = {};
    preguntas.forEach((p, i) => {
      if (resp[i] !== p.correcta) {
        newProg.erroresPorTema[p.tema] = (newProg.erroresPorTema[p.tema] || 0) + 1;
      }
    });
    if (!newProg.temasEstudiados) newProg.temasEstudiados = {};
    saveProgreso(newProg);
    setVista("resultado");
  };

  const marcarTemarioEstudiado = (temaId) => {
    const newProg = { ...progreso };
    if (!newProg.temasEstudiados) newProg.temasEstudiados = {};
    newProg.temasEstudiados[temaId] = true;
    saveProgreso(newProg);
  };

  const iniciarRefuerzo = () => {
    // Get weak topics
    const errores = progreso.erroresPorTema || {};
    const sorted = Object.entries(errores).sort((a,b) => b[1] - a[1]);
    const weakTopics = sorted.slice(0, 3).map(e => e[0]);
    if (weakTopics.length === 0) { alert("No hay temas débiles aún. Realiza un examen primero."); return; }
    const qs = PREGUNTAS.filter(p => weakTopics.includes(p.tema));
    setRefuerzoPreguntas(qs);
    iniciarExamen("estudio", qs);
  };

  const resetProgreso = async () => {
    if (confirm("¿Borrar todo el progreso? Esta acción no se puede deshacer.")) {
      setProgreso({});
      try { await window.storage.delete("autoescuela-progreso"); } catch(e) {}
    }
  };

  // ── GLOBAL PROGRESS CALC ───────────────────────────────────────────
  const calcGlobalProgress = () => {
    const temasEst = Object.keys(progreso.temasEstudiados || {}).length;
    const totalTemas = TEMARIOS.length;
    const examenes = progreso.examenes || [];
    const aprobados = examenes.filter(e => e.aprobado).length;
    const ultimoExamen = examenes.length > 0 ? examenes[examenes.length - 1] : null;
    const pctTemas = Math.round((temasEst / totalTemas) * 100);
    const errores = progreso.erroresPorTema || {};
    const topErrors = Object.entries(errores).sort((a,b)=>b[1]-a[1]).slice(0,3);
    return { temasEst, totalTemas, pctTemas, examenes: examenes.length, aprobados, ultimoExamen, topErrors };
  };

  if (loading) return <div style={S.loadingScreen}><style>{CSS}</style><InlineSVG svg={SVG.logo} size={60}/><p style={{marginTop:16,color:"#94a3b8",fontSize:"0.9rem"}}>Cargando tu progreso...</p></div>;

  const gp = calcGlobalProgress();

  // ═════════════════════════════════════════════════════════════════════
  // VISTA: INICIO
  // ═════════════════════════════════════════════════════════════════════
  if (vista === "inicio") {
    return (
      <div style={S.app}><style>{CSS}</style>
        {/* Header */}
        <div style={S.homeHeader}>
          <InlineSVG svg={SVG.logo} size={42}/>
          <div>
            <h1 style={S.brandTitle}>AutoEscuela Chile</h1>
            <p style={S.brandSub}>Licencia Clase B · CONASET 2026</p>
          </div>
        </div>

        {/* Progress Card */}
        <div style={S.progressCard}>
          <div style={S.progressCardTop}>
            <div>
              <p style={S.progressLabel}>Tu progreso general</p>
              <p style={S.progressPct}>{gp.pctTemas}%</p>
            </div>
            <div style={S.progressRing}>
              <svg viewBox="0 0 36 36" width="58" height="58">
                <path d="M18 2.0845 a 15.9155 15.9155 0 0 1 0 31.831 a 15.9155 15.9155 0 0 1 0 -31.831" fill="none" stroke="#1e293b" strokeWidth="3"/>
                <path d="M18 2.0845 a 15.9155 15.9155 0 0 1 0 31.831 a 15.9155 15.9155 0 0 1 0 -31.831" fill="none" stroke="#f59e0b" strokeWidth="3" strokeDasharray={`${gp.pctTemas}, 100`} strokeLinecap="round"/>
              </svg>
            </div>
          </div>
          <div style={S.progressStats}>
            <div style={S.progressStat}><span style={S.statNum}>{gp.temasEst}/{gp.totalTemas}</span><span style={S.statLabel}>Temas</span></div>
            <div style={S.progressStat}><span style={S.statNum}>{gp.examenes}</span><span style={S.statLabel}>Exámenes</span></div>
            <div style={S.progressStat}><span style={{...S.statNum, color: gp.aprobados > 0 ? "#059669" : "#94a3b8"}}>{gp.aprobados}</span><span style={S.statLabel}>Aprobados</span></div>
          </div>
          {gp.ultimoExamen && (
            <div style={S.lastExam}>
              Último: <strong>{gp.ultimoExamen.puntaje}/38 pts</strong> — {gp.ultimoExamen.aprobado ? "✅ Aprobado" : "❌ Reprobado"}
            </div>
          )}
        </div>

        {/* Weak Topics Alert */}
        {gp.topErrors.length > 0 && (
          <div style={S.weakAlert}>
            <div style={S.weakAlertHeader}>⚠️ Temas a reforzar</div>
            <div style={S.weakTopics}>
              {gp.topErrors.map(([tema, count]) => {
                const t = TEMARIOS.find(t => t.id === tema);
                return <span key={tema} style={{...S.weakChip, borderColor: t?.color || "#94a3b8"}}>{t?.icono} {t?.titulo || tema} ({count} errores)</span>;
              })}
            </div>
            <button onClick={iniciarRefuerzo} style={S.refuerzoBtn}>🎯 Practicar temas débiles</button>
          </div>
        )}

        {/* Main Actions */}
        <div style={S.mainActions}>
          <button onClick={() => setVista("temario")} style={S.actionBtn}>
            <span style={S.actionIcon}>📚</span>
            <div><strong>Temarios</strong><p style={S.actionDesc}>9 capítulos ilustrados</p></div>
            <span style={S.actionArrow}>→</span>
          </button>
          <button onClick={() => iniciarExamen("examen")} style={{...S.actionBtn, ...S.actionBtnExam}}>
            <span style={S.actionIcon}>📝</span>
            <div><strong>Examen Simulado</strong><p style={{...S.actionDesc, color:"rgba(255,255,255,0.7)"}}>35 preguntas · 45 min</p></div>
            <span style={{...S.actionArrow, color:"rgba(255,255,255,0.7)"}}>→</span>
          </button>
          <button onClick={() => iniciarExamen("estudio")} style={S.actionBtn}>
            <span style={S.actionIcon}>💡</span>
            <div><strong>Modo Aprendizaje</strong><p style={S.actionDesc}>Con explicaciones</p></div>
            <span style={S.actionArrow}>→</span>
          </button>
        </div>

        {/* Info bar */}
        <div style={S.infoBar}>
          <div style={S.infoItem}><span style={S.infoNum}>35</span>Preguntas</div>
          <div style={S.infoItem}><span style={S.infoNum}>38</span>Pts máx</div>
          <div style={S.infoItem}><span style={S.infoNum}>33</span>Aprueba</div>
          <div style={S.infoItem}><span style={S.infoNum}>×2</span>3 doble</div>
        </div>

        {gp.examenes > 0 && <button onClick={resetProgreso} style={S.resetBtn}>Reiniciar progreso</button>}
        <p style={S.disclaimer}>⚠️ Herramienta de práctica. No afiliada a CONASET.</p>
      </div>
    );
  }

  // ═════════════════════════════════════════════════════════════════════
  // VISTA: TEMARIOS (LISTA)
  // ═════════════════════════════════════════════════════════════════════
  if (vista === "temario") {
    return (
      <div style={S.app}><style>{CSS}</style>
        <div style={S.topBar}>
          <button onClick={() => setVista("inicio")} style={S.backBtn}>←</button>
          <h2 style={S.topTitle}>📚 Temarios Clase B</h2>
        </div>
        <p style={S.temIntro}>9 capítulos del Libro para la Conducción en Chile (CONASET 2026). Estudia cada uno y luego practica con el examen.</p>
        <div style={S.temList}>
          {TEMARIOS.map((t, i) => {
            const estudiado = progreso.temasEstudiados?.[t.id];
            const errores = progreso.erroresPorTema?.[t.id] || 0;
            return (
              <button key={t.id} onClick={() => { setTemarioActual(t); setVista("temarioDetalle"); }} style={{...S.temCard, animationDelay: `${i*0.05}s`}}>
                <div style={{...S.temCardIcon, background: `${t.color}15`, color: t.color}}>
                  <InlineSVG svg={t.ilustracion} size={44}/>
                </div>
                <div style={S.temCardContent}>
                  <div style={S.temCardHeader}>
                    <span style={S.temCardTitle}>{t.icono} {t.titulo}</span>
                    {estudiado && <span style={S.temStudied}>✓</span>}
                  </div>
                  <p style={S.temCardDesc}>{t.descripcion}</p>
                  {errores > 0 && <span style={S.temErrors}>{errores} errores en exámenes</span>}
                </div>
                <span style={S.temArrow}>›</span>
              </button>
            );
          })}
        </div>
      </div>
    );
  }

  // ═════════════════════════════════════════════════════════════════════
  // VISTA: TEMARIO DETALLE
  // ═════════════════════════════════════════════════════════════════════
  if (vista === "temarioDetalle" && temarioActual) {
    const t = temarioActual;
    return (
      <div style={S.app}><style>{CSS}</style>
        <div style={S.topBar}>
          <button onClick={() => setVista("temario")} style={S.backBtn}>←</button>
          <h2 style={S.topTitle}>{t.icono} {t.titulo}</h2>
        </div>
        {/* Hero */}
        <div style={{...S.temHero, background: `linear-gradient(135deg, ${t.color}15, ${t.color}08)`}}>
          <InlineSVG svg={t.ilustracion} size={80}/>
          <p style={{...S.temHeroDesc, color: t.color}}>{t.descripcion}</p>
        </div>
        {/* Content */}
        <div style={S.temContent}>
          {t.contenido.map((sec, i) => (
            <div key={i} style={{...S.temSection, animationDelay: `${i*0.06}s`}}>
              <h3 style={{...S.temSecTitle, color: t.color}}>{sec.subtitulo}</h3>
              {sec.svg && <div style={S.temSecIllust}><InlineSVG svg={sec.svg} size={80}/></div>}
              <p style={S.temSecText}>{sec.texto}</p>
            </div>
          ))}
        </div>
        {/* Actions */}
        <div style={S.temActions}>
          <button onClick={() => {
            marcarTemarioEstudiado(t.id);
            const qs = PREGUNTAS.filter((_,i) => t.preguntas.includes(i));
            iniciarExamen("estudio", qs);
          }} style={{...S.temTestBtn, background: t.color}}>
            📝 Practicar este tema ({t.preguntas.length} preguntas)
          </button>
          <button onClick={() => {
            marcarTemarioEstudiado(t.id);
            setVista("temario");
          }} style={S.temMarkBtn}>
            ✅ Marcar como estudiado
          </button>
        </div>
      </div>
    );
  }

  // ═════════════════════════════════════════════════════════════════════
  // VISTA: EXAMEN
  // ═════════════════════════════════════════════════════════════════════
  if (vista === "examen") {
    const q = preguntas[idx];
    if (!q) return null;
    const r = resp[idx];
    const answered = r !== undefined;
    const totalR = Object.keys(resp).length;
    const pct = (totalR / preguntas.length) * 100;
    const lowTime = timer < 300;
    const temaData = TEMARIOS.find(t => t.id === q.tema);

    return (
      <div style={S.app}><style>{CSS}</style>
        {/* Header */}
        <div style={S.examTop}>
          <button onClick={() => { clearInterval(timerRef.current); setVista("inicio"); }} style={S.backBtn}>←</button>
          <span style={S.examLabel}>{modoEx === "estudio" ? "💡 Aprendizaje" : "📝 Examen"}</span>
          {modoEx === "examen" && <span style={{...S.timerBadge, ...(lowTime ? S.timerLow : {})}}>{formatTime(timer)}</span>}
        </div>

        {/* Progress bar */}
        <div style={S.progBarWrap}><div style={{...S.progBarFill, width: `${pct}%`}}/></div>
        <div style={S.progText}>{totalR}/{preguntas.length}</div>

        {/* Nav dots toggle */}
        <button onClick={() => setNavOpen(!navOpen)} style={S.dotsToggle}>{navOpen ? "Ocultar mapa ▲" : "Mapa de preguntas ▼"}</button>
        {navOpen && (
          <div style={S.dotsGrid}>
            {preguntas.map((p, i) => {
              const rd = resp[i];
              const cur = i === idx;
              let bg = "#fff", border = "#e2e8f0", col = "#94a3b8";
              if (cur) { bg = "#fffbeb"; border = "#f59e0b"; col = "#b45309"; }
              else if (rd !== undefined) {
                if (modoEx !== "examen") {
                  if (rd === p.correcta) { bg = "#f0fdf4"; border = "#059669"; col = "#059669"; }
                  else { bg = "#fef2f2"; border = "#dc2626"; col = "#dc2626"; }
                } else { bg = "#f1f5f9"; border = "#94a3b8"; col = "#475569"; }
              }
              return <button key={i} onClick={() => { setIdx(i); setShowExpl(false); setNavOpen(false); }} style={{...S.dot, background: bg, borderColor: border, color: col}}>{i+1}{p.doble && <span style={S.dotX2}>×2</span>}</button>;
            })}
          </div>
        )}

        {/* Question */}
        <div style={S.qBox}>
          <div style={S.qMeta}>
            <span style={{...S.qTema, background: `${temaData?.color||"#6b7280"}12`, color: temaData?.color||"#6b7280"}}>{temaData?.icono} {temaData?.titulo||q.tema}</span>
            {q.doble && <span style={S.qDoble}>⚡ ×2</span>}
          </div>
          {q.svg && <div style={S.qIllust}><InlineSVG svg={q.svg} size={70}/></div>}
          <div style={S.qNum}>Pregunta {idx+1} de {preguntas.length}</div>
          <h3 style={S.qText}>{q.pregunta}</h3>

          <div style={S.optsWrap}>
            {q.opciones.map((o, oi) => {
              const letra = String.fromCharCode(65+oi);
              const sel = r === oi;
              const isCorr = oi === q.correcta;
              let st = {...S.opt};
              if (modoEx !== "examen" && answered) {
                if (isCorr) st = {...st, ...S.optOK};
                else if (sel && !isCorr) st = {...st, ...S.optBad};
              } else if (sel) st = {...st, ...S.optSel};
              let letraSt = {...S.optLetter};
              if (sel) letraSt = {...letraSt, background:"#f59e0b", color:"#fff"};
              if (modoEx !== "examen" && answered && isCorr) letraSt = {...letraSt, background:"#059669", color:"#fff"};
              if (modoEx !== "examen" && answered && sel && !isCorr) letraSt = {...letraSt, background:"#dc2626", color:"#fff"};
              return (
                <button key={oi} style={st} onClick={() => seleccionar(oi)} disabled={modoEx!=="examen" && answered}>
                  <span style={letraSt}>{modoEx!=="examen" && answered ? (isCorr?"✓":(sel?"✗":letra)) : letra}</span>
                  <span style={S.optText}>{o}</span>
                </button>
              );
            })}
          </div>

          {modoEx !== "examen" && showExpl && (
            <div style={{...S.explBox, borderColor: r===q.correcta ? "#bbf7d0" : "#fecaca"}}>
              <div style={S.explHead}>{r===q.correcta ? "✅ ¡Correcto!" : "❌ Incorrecto"}</div>
              <p style={S.explText}>{q.explicacion}</p>
            </div>
          )}
        </div>

        {/* Nav */}
        <div style={S.navRow}>
          <button onClick={() => { setShowExpl(false); setIdx(Math.max(0, idx-1)); }} disabled={idx===0} style={{...S.navBtn, opacity: idx===0?0.4:1}}>← Ant</button>
          {idx === preguntas.length-1 ? (
            <button onClick={terminar} style={S.finishBtn}>Finalizar</button>
          ) : (
            <button onClick={() => { setShowExpl(false); setIdx(idx+1); }} style={S.navBtnNext}>Sig →</button>
          )}
        </div>
      </div>
    );
  }

  // ═════════════════════════════════════════════════════════════════════
  // VISTA: RESULTADO
  // ═════════════════════════════════════════════════════════════════════
  if (vista === "resultado") {
    const res = calcResult();
    const tiempoUsado = 2700 - timer;
    return (
      <div style={S.app}><style>{CSS}</style>
        <div style={{...S.resBanner, background: res.aprobado ? "linear-gradient(135deg,#059669,#10b981)" : "linear-gradient(135deg,#dc2626,#ef4444)"}}>
          <div style={{fontSize:"3rem"}}>{res.aprobado ? "🎉" : "📚"}</div>
          <h2 style={S.resTitle}>{res.aprobado ? "¡APROBADO!" : "NO APROBADO"}</h2>
          <p style={S.resSub}>{res.aprobado ? "¡Felicidades! Estás listo." : "Sigue practicando."}</p>
        </div>
        <div style={S.resGrid}>
          <div style={S.resCard}><div style={S.resNum}>{res.puntaje}</div><div style={S.resLabel}>Puntaje</div><div style={S.resSm}>de 38</div></div>
          <div style={S.resCard}><div style={S.resNum}>{res.correctas}</div><div style={S.resLabel}>Correctas</div><div style={S.resSm}>de {preguntas.length}</div></div>
          <div style={S.resCard}><div style={S.resNum}>{formatTime(tiempoUsado)}</div><div style={S.resLabel}>Tiempo</div></div>
        </div>
        {/* Por tema */}
        <div style={S.resTemas}>
          <h3 style={{fontSize:"0.9rem",fontWeight:700,marginBottom:14}}>Rendimiento por tema</h3>
          {Object.entries(res.porTema).map(([tema, d]) => {
            const t = TEMARIOS.find(t => t.id === tema);
            const p = Math.round((d.c/d.t)*100);
            return (
              <div key={tema} style={{marginBottom:12}}>
                <div style={{display:"flex",justifyContent:"space-between",marginBottom:3}}>
                  <span style={{fontSize:"0.78rem",fontWeight:600,color:t?.color||"#6b7280"}}>{t?.icono} {t?.titulo||tema}</span>
                  <span style={{fontSize:"0.78rem",fontWeight:600,fontFamily:"'JetBrains Mono',monospace"}}>{d.c}/{d.t}</span>
                </div>
                <div style={{height:5,borderRadius:3,background:"#f1f5f9",overflow:"hidden"}}>
                  <div style={{height:"100%",borderRadius:3,width:`${p}%`,background:p>=80?"#059669":p>=50?"#f59e0b":"#dc2626",transition:"width 0.6s"}}/>
                </div>
              </div>
            );
          })}
        </div>
        {/* Temas débiles */}
        {Object.keys(res.erroresTema).length > 0 && (
          <div style={S.weakAlert}>
            <div style={S.weakAlertHeader}>🎯 Refuerza estos temas:</div>
            <div style={S.weakTopics}>
              {Object.keys(res.erroresTema).map(tema => {
                const t = TEMARIOS.find(t => t.id === tema);
                return <span key={tema} style={{...S.weakChip, borderColor: t?.color}}>{t?.icono} {t?.titulo} ({res.erroresTema[tema].length})</span>;
              })}
            </div>
            <button onClick={() => {
              const weakQs = [];
              Object.entries(res.erroresTema).forEach(([tema, indices]) => {
                indices.forEach(i => weakQs.push(preguntas[i]));
              });
              iniciarExamen("estudio", weakQs);
            }} style={S.refuerzoBtn}>🔄 Practicar solo mis errores</button>
          </div>
        )}
        <div style={S.resActions}>
          <button onClick={() => setVista("revision")} style={S.revBtn}>📋 Revisar respuestas</button>
          <button onClick={() => setVista("inicio")} style={S.newExBtn}>🏠 Inicio</button>
        </div>
      </div>
    );
  }

  // ═════════════════════════════════════════════════════════════════════
  // VISTA: REVISIÓN
  // ═════════════════════════════════════════════════════════════════════
  if (vista === "revision") {
    return (
      <div style={S.app}><style>{CSS}</style>
        <div style={S.topBar}>
          <button onClick={() => setVista("resultado")} style={S.backBtn}>←</button>
          <h2 style={S.topTitle}>📋 Revisión</h2>
        </div>
        <div style={{padding:"0 16px 40px"}}>
          {preguntas.map((q, i) => {
            const r2 = resp[i];
            const ok = r2 === q.correcta;
            const noResp = r2 === undefined;
            const t = TEMARIOS.find(t => t.id === q.tema);
            return (
              <div key={i} style={{...S.revCard, borderLeft: `4px solid ${noResp?"#9ca3af":ok?"#059669":"#dc2626"}`}}>
                <div style={{display:"flex",justifyContent:"space-between",flexWrap:"wrap",gap:6,marginBottom:8}}>
                  <span style={{fontSize:"0.82rem",fontWeight:700}}>{noResp?"⬜":ok?"✅":"❌"} Pregunta {i+1}</span>
                  <div style={{display:"flex",gap:4}}>
                    <span style={{fontSize:"0.65rem",fontWeight:600,padding:"2px 8px",borderRadius:5,background:`${t?.color||"#6b7280"}15`,color:t?.color}}>{t?.icono} {t?.titulo}</span>
                    {q.doble && <span style={{fontSize:"0.65rem",fontWeight:700,padding:"2px 8px",borderRadius:5,background:"#dc2626",color:"#fff"}}>×2</span>}
                  </div>
                </div>
                {q.svg && <div style={{margin:"8px 0",display:"flex",justifyContent:"center"}}><InlineSVG svg={q.svg} size={56}/></div>}
                <p style={{fontSize:"0.88rem",fontWeight:500,lineHeight:1.5,marginBottom:10}}>{q.pregunta}</p>
                {q.opciones.map((o, oi) => {
                  const l = String.fromCharCode(65+oi);
                  const isC = oi===q.correcta;
                  const isS = oi===r2;
                  let bg = "#f8fafc", col = "#475569";
                  if (isC) { bg="#f0fdf4"; col="#065f46"; }
                  if (isS && !isC) { bg="#fef2f2"; col="#991b1b"; }
                  return <div key={oi} style={{display:"flex",gap:8,alignItems:"flex-start",padding:"6px 8px",borderRadius:7,fontSize:"0.8rem",color:col,background:bg,marginBottom:4,textDecoration:isS&&!isC?"line-through":"none",lineHeight:1.4}}>
                    <span style={{minWidth:20,height:20,borderRadius:5,display:"flex",alignItems:"center",justifyContent:"center",fontSize:"0.68rem",fontWeight:700,background:isC?"#059669":isS?"#dc2626":"#e2e8f0",color:isC||isS?"#fff":"#64748b",flexShrink:0}}>{isC?"✓":isS?"✗":l}</span>
                    <span>{o}</span>
                  </div>;
                })}
                <div style={{fontSize:"0.78rem",color:"#475569",lineHeight:1.6,padding:10,background:"#f8fafc",borderRadius:7,borderLeft:"3px solid #f59e0b",marginTop:8}}>
                  <strong>Explicación:</strong> {q.explicacion}
                </div>
              </div>
            );
          })}
          <button onClick={() => setVista("inicio")} style={{...S.newExBtn, margin:"20px auto", display:"block"}}>🏠 Inicio</button>
        </div>
      </div>
    );
  }

  return null;
}

// ═══════════════════════════════════════════════════════════════════════
// CSS
// ═══════════════════════════════════════════════════════════════════════
const CSS = `
@import url('https://fonts.googleapis.com/css2?family=Outfit:wght@300;400;500;600;700;800&family=JetBrains+Mono:wght@400;600&display=swap');
*{box-sizing:border-box;margin:0;padding:0;}
button{cursor:pointer;font-family:'Outfit',sans-serif;}
button:disabled{cursor:not-allowed;opacity:0.5;}
@keyframes fadeIn{from{opacity:0;transform:translateY(6px)}to{opacity:1;transform:translateY(0)}}
@keyframes slideUp{from{opacity:0;transform:translateY(16px)}to{opacity:1;transform:translateY(0)}}
@keyframes pulse{0%,100%{opacity:1}50%{opacity:0.5}}
`;

// ═══════════════════════════════════════════════════════════════════════
// STYLES
// ═══════════════════════════════════════════════════════════════════════
const S = {
  app: { fontFamily:"'Outfit',sans-serif", background:"#f8fafc", minHeight:"100vh", color:"#1e293b", maxWidth:640, margin:"0 auto" },
  loadingScreen: { display:"flex", flexDirection:"column", alignItems:"center", justifyContent:"center", minHeight:"100vh", background:"#f8fafc" },

  // Home
  homeHeader: { display:"flex", alignItems:"center", gap:12, padding:"20px 16px 0" },
  brandTitle: { fontSize:"1.25rem", fontWeight:800, color:"#0f172a", letterSpacing:"-0.02em" },
  brandSub: { fontSize:"0.72rem", color:"#94a3b8", fontWeight:500 },

  // Progress Card
  progressCard: { margin:"16px 16px 0", padding:"18px", borderRadius:16, background:"linear-gradient(135deg,#0f172a,#1e293b)", color:"#fff" },
  progressCardTop: { display:"flex", justifyContent:"space-between", alignItems:"center" },
  progressLabel: { fontSize:"0.72rem", color:"#94a3b8", fontWeight:500 },
  progressPct: { fontSize:"2rem", fontWeight:800, color:"#f59e0b", fontFamily:"'JetBrains Mono',monospace" },
  progressRing: { },
  progressStats: { display:"flex", gap:16, marginTop:14, paddingTop:14, borderTop:"1px solid #334155" },
  progressStat: { display:"flex", flexDirection:"column", alignItems:"center", flex:1 },
  statNum: { fontSize:"1.1rem", fontWeight:700, fontFamily:"'JetBrains Mono',monospace" },
  statLabel: { fontSize:"0.65rem", color:"#94a3b8", marginTop:2 },
  lastExam: { fontSize:"0.72rem", color:"#94a3b8", marginTop:10, textAlign:"center" },

  // Weak topics
  weakAlert: { margin:"14px 16px 0", padding:14, borderRadius:12, background:"#fffbeb", border:"1px solid #fde68a" },
  weakAlertHeader: { fontSize:"0.82rem", fontWeight:700, marginBottom:8 },
  weakTopics: { display:"flex", flexWrap:"wrap", gap:6, marginBottom:10 },
  weakChip: { fontSize:"0.7rem", fontWeight:600, padding:"3px 8px", borderRadius:6, border:"1.5px solid", background:"#fff" },
  refuerzoBtn: { width:"100%", padding:"10px", border:"none", borderRadius:8, background:"#f59e0b", color:"#1e293b", fontSize:"0.8rem", fontWeight:700 },

  // Main Actions
  mainActions: { display:"flex", flexDirection:"column", gap:10, margin:"18px 16px 0" },
  actionBtn: { display:"flex", alignItems:"center", gap:12, padding:"14px 16px", border:"1.5px solid #e2e8f0", borderRadius:14, background:"#fff", textAlign:"left", width:"100%", transition:"all 0.15s" },
  actionBtnExam: { background:"linear-gradient(135deg,#0f172a,#1e293b)", color:"#fff", border:"none", boxShadow:"0 4px 20px rgba(15,23,42,0.25)" },
  actionIcon: { fontSize:"1.5rem" },
  actionDesc: { fontSize:"0.72rem", color:"#94a3b8", marginTop:1 },
  actionArrow: { marginLeft:"auto", fontSize:"1.2rem", color:"#94a3b8" },

  // Info bar
  infoBar: { display:"grid", gridTemplateColumns:"repeat(4,1fr)", gap:8, margin:"18px 16px 0" },
  infoItem: { textAlign:"center", padding:"10px 4px", background:"#fff", borderRadius:10, border:"1px solid #e2e8f0", fontSize:"0.65rem", color:"#94a3b8" },
  infoNum: { display:"block", fontSize:"1.15rem", fontWeight:700, color:"#f59e0b", fontFamily:"'JetBrains Mono',monospace" },

  resetBtn: { display:"block", margin:"18px auto 0", background:"none", border:"none", color:"#94a3b8", fontSize:"0.72rem", textDecoration:"underline" },
  disclaimer: { fontSize:"0.68rem", color:"#cbd5e1", textAlign:"center", margin:"14px 16px 24px", lineHeight:1.5 },

  // Top bar
  topBar: { display:"flex", alignItems:"center", gap:10, padding:"14px 16px", background:"#fff", borderBottom:"1px solid #e2e8f0", position:"sticky", top:0, zIndex:100 },
  backBtn: { background:"none", border:"none", fontSize:"1.2rem", color:"#64748b", padding:"4px 8px", borderRadius:8 },
  topTitle: { fontSize:"1rem", fontWeight:700 },

  // Temarios list
  temIntro: { fontSize:"0.82rem", color:"#64748b", padding:"12px 16px 4px", lineHeight:1.5 },
  temList: { padding:"8px 16px 30px" },
  temCard: { display:"flex", alignItems:"center", gap:12, width:"100%", padding:"14px", border:"1.5px solid #e2e8f0", borderRadius:14, background:"#fff", textAlign:"left", marginBottom:10, animation:"fadeIn 0.4s ease both" },
  temCardIcon: { width:56, height:56, borderRadius:12, display:"flex", alignItems:"center", justifyContent:"center", flexShrink:0 },
  temCardContent: { flex:1, minWidth:0 },
  temCardHeader: { display:"flex", alignItems:"center", gap:6 },
  temCardTitle: { fontSize:"0.88rem", fontWeight:700, color:"#0f172a" },
  temStudied: { fontSize:"0.7rem", background:"#f0fdf4", color:"#059669", borderRadius:5, padding:"1px 6px", fontWeight:700 },
  temCardDesc: { fontSize:"0.72rem", color:"#94a3b8", marginTop:2, lineHeight:1.4 },
  temErrors: { fontSize:"0.65rem", color:"#dc2626", fontWeight:600, marginTop:3, display:"inline-block" },
  temArrow: { fontSize:"1.4rem", color:"#cbd5e1", flexShrink:0 },

  // Temario detail
  temHero: { margin:"0 16px", padding:"24px", borderRadius:16, textAlign:"center", animation:"fadeIn 0.4s ease" },
  temHeroDesc: { fontSize:"0.85rem", fontWeight:500, marginTop:12 },
  temContent: { padding:"8px 16px 0" },
  temSection: { background:"#fff", border:"1px solid #e2e8f0", borderRadius:14, padding:16, marginBottom:12, animation:"slideUp 0.4s ease both" },
  temSecTitle: { fontSize:"0.92rem", fontWeight:700, marginBottom:8 },
  temSecIllust: { display:"flex", justifyContent:"center", margin:"10px 0" },
  temSecText: { fontSize:"0.82rem", color:"#475569", lineHeight:1.65 },
  temActions: { padding:"12px 16px 30px", display:"flex", flexDirection:"column", gap:8 },
  temTestBtn: { padding:14, border:"none", borderRadius:12, color:"#fff", fontSize:"0.88rem", fontWeight:700 },
  temMarkBtn: { padding:12, border:"2px solid #e2e8f0", borderRadius:12, background:"#fff", fontSize:"0.85rem", fontWeight:600, color:"#475569" },

  // Examen
  examTop: { display:"flex", alignItems:"center", justifyContent:"space-between", padding:"10px 16px", background:"#fff", borderBottom:"1px solid #e2e8f0", position:"sticky", top:0, zIndex:100 },
  examLabel: { fontSize:"0.82rem", fontWeight:600, color:"#475569" },
  timerBadge: { padding:"5px 12px", borderRadius:20, background:"#f1f5f9", fontSize:"0.82rem", fontWeight:600, fontFamily:"'JetBrains Mono',monospace", color:"#334155" },
  timerLow: { background:"#fef2f2", color:"#dc2626", animation:"pulse 1s ease infinite" },
  progBarWrap: { height:4, background:"#e2e8f0", margin:"0 16px" },
  progBarFill: { height:"100%", borderRadius:2, background:"linear-gradient(90deg,#f59e0b,#eab308)", transition:"width 0.4s" },
  progText: { fontSize:"0.68rem", color:"#94a3b8", textAlign:"right", padding:"3px 16px 0" },
  dotsToggle: { display:"block", width:"100%", background:"none", border:"none", borderBottom:"1px solid #e2e8f0", color:"#64748b", fontSize:"0.72rem", padding:"6px 16px", textAlign:"center" },
  dotsGrid: { display:"grid", gridTemplateColumns:"repeat(7,1fr)", gap:5, padding:"8px 16px", background:"#fff", borderBottom:"1px solid #e2e8f0", animation:"fadeIn 0.2s" },
  dot: { aspectRatio:"1", borderRadius:7, border:"1.5px solid", fontSize:"0.65rem", fontWeight:600, display:"flex", flexDirection:"column", alignItems:"center", justifyContent:"center", position:"relative", lineHeight:1 },
  dotX2: { position:"absolute", top:-3, right:-3, fontSize:"0.45rem", background:"#dc2626", color:"#fff", borderRadius:3, padding:"1px 2px", fontWeight:700 },

  // Question
  qBox: { padding:"16px", maxWidth:600, margin:"0 auto", animation:"fadeIn 0.3s" },
  qMeta: { display:"flex", alignItems:"center", gap:6, flexWrap:"wrap", marginBottom:10 },
  qTema: { fontSize:"0.68rem", fontWeight:600, padding:"3px 8px", borderRadius:5 },
  qDoble: { fontSize:"0.68rem", fontWeight:700, padding:"3px 8px", borderRadius:5, background:"linear-gradient(135deg,#dc2626,#ef4444)", color:"#fff" },
  qIllust: { display:"flex", justifyContent:"center", margin:"8px 0 12px" },
  qNum: { fontSize:"0.72rem", color:"#94a3b8", marginBottom:4 },
  qText: { fontSize:"1rem", fontWeight:600, lineHeight:1.5, marginBottom:16, color:"#0f172a" },
  optsWrap: { display:"flex", flexDirection:"column", gap:8 },
  opt: { display:"flex", alignItems:"flex-start", gap:10, padding:"12px 14px", border:"2px solid #e2e8f0", borderRadius:11, background:"#fff", textAlign:"left", width:"100%", fontSize:"0.85rem", lineHeight:1.4, color:"#334155", transition:"all 0.15s" },
  optSel: { borderColor:"#f59e0b", background:"#fffbeb" },
  optOK: { borderColor:"#059669", background:"#f0fdf4" },
  optBad: { borderColor:"#dc2626", background:"#fef2f2" },
  optLetter: { minWidth:26, height:26, borderRadius:7, display:"flex", alignItems:"center", justifyContent:"center", fontSize:"0.75rem", fontWeight:700, background:"#f1f5f9", color:"#64748b", flexShrink:0 },
  optText: { paddingTop:2 },
  explBox: { marginTop:16, padding:14, borderRadius:11, background:"#f0fdf4", border:"1px solid", animation:"slideUp 0.3s" },
  explHead: { fontSize:"0.85rem", fontWeight:700, marginBottom:6 },
  explText: { fontSize:"0.8rem", color:"#334155", lineHeight:1.6 },

  // Nav
  navRow: { display:"flex", gap:8, padding:"14px 16px", maxWidth:600, margin:"0 auto" },
  navBtn: { flex:1, padding:11, border:"2px solid #e2e8f0", borderRadius:11, background:"#fff", fontSize:"0.82rem", fontWeight:600, color:"#64748b" },
  navBtnNext: { flex:1, padding:11, border:"none", borderRadius:11, background:"#0f172a", color:"#fff", fontSize:"0.82rem", fontWeight:600 },
  finishBtn: { flex:1, padding:11, border:"none", borderRadius:11, background:"linear-gradient(135deg,#f59e0b,#eab308)", color:"#1e293b", fontSize:"0.82rem", fontWeight:700 },

  // Resultado
  resBanner: { textAlign:"center", padding:"32px 20px", borderRadius:"0 0 20px 20px", color:"#fff" },
  resTitle: { fontSize:"1.6rem", fontWeight:800, letterSpacing:"-0.02em" },
  resSub: { fontSize:"0.85rem", opacity:0.9, marginTop:4 },
  resGrid: { display:"grid", gridTemplateColumns:"repeat(3,1fr)", gap:8, padding:"16px 16px 0" },
  resCard: { textAlign:"center", padding:"14px 6px", background:"#fff", borderRadius:12, border:"1px solid #e2e8f0" },
  resNum: { fontSize:"1.3rem", fontWeight:800, fontFamily:"'JetBrains Mono',monospace" },
  resLabel: { fontSize:"0.7rem", fontWeight:600, color:"#64748b", marginTop:2 },
  resSm: { fontSize:"0.62rem", color:"#94a3b8" },
  resTemas: { margin:"16px 16px 0", background:"#fff", borderRadius:14, border:"1px solid #e2e8f0", padding:16 },
  resActions: { display:"flex", gap:8, padding:"16px" },
  revBtn: { flex:1, padding:12, border:"2px solid #e2e8f0", borderRadius:11, background:"#fff", fontSize:"0.82rem", fontWeight:600, color:"#475569" },
  newExBtn: { flex:1, padding:12, border:"none", borderRadius:11, background:"linear-gradient(135deg,#0f172a,#1e293b)", color:"#fff", fontSize:"0.82rem", fontWeight:600 },

  // Revisión
  revCard: { background:"#fff", borderRadius:13, border:"1px solid #e2e8f0", padding:16, marginBottom:12, animation:"fadeIn 0.3s ease" },
};
