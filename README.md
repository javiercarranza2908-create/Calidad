<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Examen de Gestión de Calidad</title>
    
    <!-- Librerías Externas -->
    <script src="https://cdnjs.cloudflare.com"></script>
    <script type="text/javascript" src="https://cdn.jsdelivr.net"></script>

    <style>
        :root { --primary: #1a73e8; --success: #27ae60; --bg: #f4f7f6; }
        body { font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; background-color: var(--bg); margin: 0; padding: 20px; display: flex; justify-content: center; }
        .container { max-width: 800px; width: 100%; background: white; padding: 40px; border-radius: 12px; box-shadow: 0 10px 25px rgba(0,0,0,0.1); }
        h1 { text-align: center; color: var(--primary); margin-bottom: 30px; border-bottom: 2px solid #eee; padding-bottom: 10px; }
        h3 { color: #2c3e50; margin-top: 25px; border-left: 4px solid var(--primary); padding-left: 10px; }
        
        /* Formulario de Datos */
        .grid-inputs { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; margin-bottom: 30px; }
        .field { display: flex; flex-direction: column; }
        label { font-weight: 600; margin-bottom: 8px; font-size: 14px; color: #555; }
        input[type="text"] { padding: 12px; border: 1px solid #ddd; border-radius: 6px; transition: border 0.3s; }
        input:focus { border-color: var(--primary); outline: none; box-shadow: 0 0 5px rgba(26,115,232,0.2); }

        /* Preguntas */
        .question-box { background: #fcfcfc; padding: 20px; border: 1px solid #eee; border-radius: 8px; margin-bottom: 20px; }
        .options { margin-top: 10px; }
        .option-item { display: flex; align-items: center; margin-bottom: 10px; cursor: pointer; padding: 8px; border-radius: 4px; transition: background 0.2s; }
        .option-item:hover { background: #f0f7ff; }
        .option-item input { margin-right: 12px; transform: scale(1.2); }

        /* Botón */
        #btn-enviar { width: 100%; padding: 18px; background: var(--success); color: white; border: none; border-radius: 8px; font-size: 18px; font-weight: bold; cursor: pointer; transition: transform 0.2s, background 0.3s; margin-top: 20px; }
        #btn-enviar:hover { background: #219150; transform: translateY(-2px); }
        #btn-enviar:disabled { background: #bdc3c7; cursor: not-allowed; }
    </style>
</head>
<body>

<div class="container">
    <h1>Examen de Calidad Total</h1>
    
    <form id="quiz-form">
        <!-- SECCIÓN: DATOS -->
        <h3>Datos del Estudiante</h3>
        <div class="grid-inputs">
            <div class="field"><label>Nombre</label><input type="text" id="nombre" required></div>
            <div class="field"><label>Apellido</label><input type="text" id="apellido" required></div>
            <div class="field"><label>Cédula</label><input type="text" id="cedula" required></div>
            <div class="field"><label>Sección</label><input type="text" id="seccion" required></div>
            <div class="field" style="grid-column: span 2;"><label>Mención de su Carrera</label><input type="text" id="carrera" required></div>
            <div class="field" style="grid-column: span 2;"><label>Nombre de la Universidad</label><input type="text" id="universidad" required></div>
        </div>

        <!-- SECCIÓN: PREGUNTAS -->
        <h3>Evaluación</h3>

        <div class="question-box">
            <label>1. ¿Quiénes son considerados los fundadores de la calidad moderna?</label>
            <div class="options">
                <label class="option-item"><input type="radio" name="p1" value="Henry Ford y Frederick Taylor" required> a) Henry Ford y Frederick Taylor</label>
                <label class="option-item"><input type="radio" name="p1" value="Deming, Juran e Ishikawa"> b) W. Edwards Deming, Joseph Juran y Kaoru Ishikawa</label>
                <label class="option-item"><input type="radio" name="p1" value="Steve Jobs y Bill Gates"> c) Steve Jobs y Bill Gates</label>
            </div>
        </div>

        <div class="question-box">
            <label>2. ¿En qué año se inicia formalmente el movimiento de la calidad (postguerra)?</label>
            <div class="options">
                <label class="option-item"><input type="radio" name="p2" value="1950 (A)" required> a) En el año 1950</label>
                <label class="option-item"><input type="radio" name="p2" value="1800 (B)"> b) En el año 1800</label>
                <label class="option-item"><input type="radio" name="p2" value="1990 (C)"> c) En el año 1990</label>
            </div>
        </div>

        <button type="submit" id="btn-enviar">Finalizar y Enviar Examen (PDF)</button>
    </form>
</div>

<script>
    // 1. CONFIGURACIÓN: Reemplaza con tus llaves de EmailJS
    const PUBLIC_KEY = "TU_PUBLIC_KEY";
    const SERVICE_ID = "TU_SERVICE_ID";
    const TEMPLATE_ID = "TU_TEMPLATE_ID";

    emailjs.init(PUBLIC_KEY);

    document.getElementById('quiz-form').addEventListener('submit', function(event) {
        event.preventDefault();
        const btn = document.getElementById('btn-enviar');
        btn.disabled = true;
        btn.innerText = 'Generando archivo y enviando...';

        const { jsPDF } = window.jspdf;
        const doc = new jsPDF();

        // Obtener valores
        const datos = {
            nombre: document.getElementById('nombre').value,
            apellido: document.getElementById('apellido').value,
            cedula: document.getElementById('cedula').value,
            carrera: document.getElementById('carrera').value,
            universidad: document.getElementById('universidad').value,
            seccion: document.getElementById('seccion').value,
            p1: document.querySelector('input[name="p1"]:checked').value,
            p2: document.querySelector('input[name="p2"]:checked').value,
            fecha: new Date().toLocaleString()
        };

        // Crear el PDF
        doc.setFontSize(20);
        doc.text("EXAMEN DE CALIDAD - RESULTADOS", 20, 20);
        
        doc.setFontSize(12);
        doc.text(`Fecha de entrega: ${datos.fecha}`, 20, 35);
        doc.text("---------------------------------------------------------", 20, 40);
        doc.text(`Estudiante: ${datos.nombre} ${datos.apellido}`, 20, 50);
        doc.text(`Cédula: ${datos.cedula}`, 20, 60);
        doc.text(`Carrera: ${datos.carrera}`, 20, 70);
        doc.text(`Universidad: ${datos.universidad}`, 20, 80);
        doc.text(`Sección: ${datos.seccion}`, 20, 90);
        
        doc.setFontSize(14);
        doc.text("Respuestas:", 20, 110);
        doc.setFontSize(12);
        doc.text(`P1. Fundadores: ${datos.p1}`, 20, 120);
        doc.text(`P2. Año de inicio: ${datos.p2}`, 20, 130);

        // Convertir PDF a Base64
        const pdfBase64 = doc.output('datauristring');

        // Enviar vía EmailJS
        const templateParams = {
            ...datos,
            my_attachment: pdfBase64 // El PDF adjunto
        };

        emailjs.send(SERVICE_ID, TEMPLATE_ID, templateParams)
            .then(() => {
                alert('¡Éxito! Tu examen ha sido enviado en formato PDF al profesor.');
                btn.innerText = 'Examen Enviado';
            }, (error) => {
                alert('Error al enviar: ' + JSON.stringify(error));
                btn.disabled = false;
                btn.innerText = 'Reintentar Envío';
            });
    });
</script>

</body>
</html>

