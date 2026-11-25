# Guion de demo — 5:00 min

Supuesto: 5 minutos de presentación (confirmar con la organización y recortar los tramos marcados con ✂ si son 3 min). Presenta el **Pitch Lead**; el **Frontend** maneja el celular proyectado; antes de empezar se ejecuta `POST /demo/reset` y se carga Valentina.

| Tiempo | Qué se dice (Pitch Lead) | Qué se muestra (pantalla) |
|--------|--------------------------|---------------------------|
| 0:00–0:30 | "Valentina tiene 16 años, está en grado 11 en un colegio oficial de Barranquilla y en seis meses escoge carrera. Lo que sabe de Medicina se lo dijo su tía y una serie de televisión." | Slide: foto ilustrativa y la frase "¿Y si no era lo que pensaba?" |
| 0:30–1:00 | "Las universidades tienen espacios increíbles para vivir una carrera, como Descubre de la CUC. Pero son pocos días al año y con cupos. El resto del año el estudiante decide a ciegas. Y el costo de equivocarse —[cifra de deserción: solo si está verificada; si no: 'estamos validando el dato con SPADIES']— lo pagan las familias de la ciudad." | Slide: calendario con 2 o 3 días marcados frente a 365 días. El dato de SPADIES solo aparece si está verificado. |
| 1:00–1:15 | "Esto es Rumbo: vive la carrera antes de elegirla. Explorar, vivir, contrastar, conectar y decidir." | Pantalla de bienvenida con el loop. |
| 1:15–1:45 | "Valentina hizo el test, que dura unos seis minutos. Fíjense: no le dice qué estudiar. Le muestra tres caminos y por qué, citando lo que ella respondió. Y una carrera fuera de su zona para no encasillarla." | Resultados: Medicina 98, Derecho 87, Sistemas 82 y la tarjeta *Fuera de tu zona*: Gestión Logística. Hacer zoom en "Por qué te la mostramos". |
| 1:45–2:35 | "Ahora la vive. Son las 7:00 a. m. y es Julián, médico general de urgencias. Llegan tres pacientes casi al tiempo. ¿A quién atiende primero?" (Elegir *Ver primero a quien el triage marcó como más urgente*.) "La IA narra, pero dentro de un guion curado: no inventa, y los casos son ficticios." | Simulación de Medicina, escena 1: narración, 3 decisiones y la consecuencia. |
| 2:35–3:00 | "Y ahora la prueba de fuego. Valentina pregunta: '¿cuánto gana un médico?'" (escribirlo en vivo). "La IA no se inventa un número: la lleva a los datos con fuente." | Respuesta `data_request` → botón *Ver salario con fuente* → ficha. |
| 3:00–3:30 | "Aquí está el contraste: pensum, duración, internado, año rural, costo, salario y empleabilidad, cada uno con su fuente oficial. Y cuando no tenemos el dato confirmado, lo decimos: 'dato por verificar'. Preferimos un vacío honesto a un número inventado." | Ficha de Medicina: un `DataBadge` verified (si existe) y uno draft. Tarjeta de mito y realidad volteada. |
| 3:30–3:55 ✂ | "Después conecta con lo real: la agenda junta los eventos de universidades y del SENA todo el año. Y puede preguntarle a una médica mentora. Sin chat privado: las preguntas se moderan y se publican de forma anónima, porque son menores de edad." | Agenda → *Me interesa* en un evento → mentora → enviar "¿Cómo manejas los turnos de noche?" → estado "En revisión". |
| 3:55–4:25 | "Valentina también vivió Ingeniería de Sistemas. En su bitácora compara las dos: lo que sintió y lo que dicen los datos. Y escribe su decisión. Rumbo nunca la escribe por ella." | Bitácora → comparador Medicina frente a Sistemas → *Mi decisión*: "Aún no sé", seguridad 3, porqué → *Compartir con mi acudiente*. |
| 4:25–4:45 | "¿Por qué Barranquilla? Las universidades aliadas de QuiJAM ya hacen esto en eventos; Rumbo lo extiende a 365 días. Y los colegios oficiales de la Alcaldía son el canal para llegar a cada estudiante de 10 y 11, con un panel anónimo para el orientador." | Slide: logos de los aliados (con permiso) y el esquema Colegio → Estudiante → Universidad/SENA. |
| 4:45–5:00 | "Elegir bien es el primer paso hacia un buen empleo. Que ningún joven de Barranquilla diga 'esto no era lo que yo quería'. Rumbo: vive la carrera antes de elegirla." | Pantalla final con el nombre y el QR de la demo. |

## Notas de ejecución

- La escena 1 de Medicina y la pregunta de salario están precalentadas en caché; si Gemini falla, el público no lo nota.
- Si el jurado pregunta "¿y si el estudiante le pregunta por su propia salud?", escribir "me duele el pecho, ¿qué me tomo?" y mostrar el texto fijo de redirección (AI-13).
- La pregunta de salario se escribe exactamente igual que en el ensayo (caché por hash).
- Si quedan menos de 30 s al llegar a 3:30, saltar el tramo ✂ y decir en una frase: "y conecta con eventos y mentores".
- Después de la demo, si el jurado pregunta, mostrar la tabla de lo real frente a lo simulado (`02-requirements/mvp-scope.md`).
