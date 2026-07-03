# perfilemprendedor
Tets
/**							
* Calcula el perfil de personalidad emprendedora basado en el Entrepreneur DNA del FI.							
* @param {Array<string>} respuestas - Un arreglo de 50 strings con las letras elegidas ('A', 'B', 'C', 'D')							
* @returns {Object} Un objeto con el desglose de porcentajes, el perfil dominante y la lógica de enganche para Navi.							
*/							
function calcularPerfilEmprendedor(respuestas) {							
// Validar que se hayan respondido las 50 preguntas							
if (!Array.isArray(respuestas) || respuestas.length !== 50) {							
throw new Error("El cuestionario debe contener exactamente 50 respuestas.");							
}							
// Inicializar contadores para los 4 perfiles							
let conteo = {							
visionary: 0,   // Corresponde a la opción A							
operator: 0,    // Corresponde a la opción B							
hustler: 0,     // Corresponde a la opción C							
productMaverick: 0 // Corresponde a la opción D							
};							
// Procesar las respuestas de elección forzada							
respuestas.forEach((respuesta) => {							
const opcion = respuesta.toUpperCase();							
if (opcion === 'A') conteo.visionary++;							
else if (opcion === 'B') conteo.operator++;							
else if (opcion === 'C') conteo.hustler++;							
else if (opcion === 'D') conteo.productMaverick++;							
});							
const totalPreguntas = 50;							
// Calcular los porcentajes reales correspondientes a cada perfil							
let porcentajes = {							
visionary: Math.round((conteo.visionary / totalPreguntas) * 100),							
operator: Math.round((conteo.operator / totalPreguntas) * 100),							
hustler: Math.round((conteo.hustler / totalPreguntas) * 100),							
productMaverick: Math.round((conteo.productMaverick / totalPreguntas) * 100)							
};							
// Determinar el perfil dominante mediante ordenamiento lineal							
let maxPuntos = -1;							
let perfilesDominantes = [];							
for (let perfil in conteo) {							
if (conteo[perfil] > maxPuntos) {							
maxPuntos = conteo[perfil];							
perfilesDominantes = [perfil]; // Reinicia con el nuevo máximo absoluto							
} else if (conteo[perfil] === maxPuntos) {							
perfilesDominantes.push(perfil); // Manejo de empates técnicos (Perfiles Híbridos)							
}							
}							
// Mapeo estético de nombres de los arquetipos oficiales del Founder Institute							
const nombresPerfiles = {							
visionary: "The Visionary (El Visionario)",							
operator: "The Operator (El Ejecutor)",							
hustler: "The Marketer/Hustler (El Negociador)",							
productMaverick: "The Product Maverick (El Innovador Técnico)"							
};							
// Definición de la lógica de enganche automatizada para ofrecer Navi según el dolor del perfil							
const ganchosNavi = {							
visionary: "Tu mente está en el futuro y odias la fricción operativa. El peligro real es tomar decisiones basadas en intuición, perdiendo de vista la realidad financiera. Navi traduce el caos de tus datos operativos y financieros en un tablero visual ultra simple para que lideres la estrategia con certezas, no con corazonadas.",							
operator: "Buscas el control absoluto, pero centralizar datos manualmente te consume el día y te convierte en el cuello de botella de tu propia empresa. Navi automatiza e integra tus fuentes de datos de forma híbrida y en tiempo real, dándote el control absoluto de tus KPI sin planillas manuales lentas.",							
hustler: "Eres un imán de ventas, pero tu punto ciego es confundir la facturación o métricas de vanidad con la rentabilidad real. Navi ordena tus datos financieros y de flujo de caja en paneles estéticos y listos para presentar, ayudándote a blindar tus alianzas con data real e incuestionable.",							
productMaverick: "Buscas la perfección técnica, pero corres el riesgo de sufrir parálisis por análisis o construir soluciones que el mercado no valida rápido por falta de métricas comerciales. Navi te ofrece analítica de negocios limpia mediante plantillas optimizadas para conectar tu producto con la realidad comercial sin alterar tu arquitectura."							
};							
// Construcción del resultado final estructurado							
let resultadoFinal = {							
desglosePorcentajes: porcentajes,							
esHibrido: perfilesDominantes.length > 1,							
perfilPrincipal: perfilesDominantes.map(p => nombresPerfiles[p]).join(" + "),							
diagnosticoGanchoNavi: perfilesDominantes.map(p => ganchosNavi[p]).join(" Adicionalmente, al balancear tu perfil híbrido: ")							
};							
return resultadoFinal;							
}							
// ==========================================							
// EJEMPLO DE USO PRÁCTICO EN TU WEB:							
// ==========================================							
/*							
const respuestasSimuladasUsuario = [							
A','A','A','B','C','D','A','B','A','A', // 1-10							
C','D','A','A','B','A','C','A','A','B', // 11-20							
A','A','A','A','B','A','A','A','C','A', // 21-30							
A','B','A','A','D','A','A','C','A','A', // 31-40							
A','A','A','A','B','A','D','A','A','A'  // 41-50							
];							
const resultadoTest = calcularPerfilEmprendedor(respuestasSimuladasUsuario);							
console.log(resultadoTest);							
*/							
