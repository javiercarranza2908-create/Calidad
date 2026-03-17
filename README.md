<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Examen de Gestión de Calidad</title>
    <style>
        body { font-family: Arial, sans-serif; background-color: #f4f4f9; margin: 20px; color: #333; }
        .container { max-width: 700px; background: white; padding: 30px; border-radius: 8px; box-shadow: 0 2px 10px rgba(0,0,0,0.1); margin: auto; }
        h1 { text-align: center; color: #2c3e50; }
        .section-title { border-bottom: 2px solid #3498db; margin-bottom: 20px; padding-bottom: 5px; color: #3498db; }
        .grid-inputs { display: grid; grid-template-columns: 1fr 1fr; gap: 15px; margin-bottom: 25px; }
        label { display: block; margin-bottom: 5px; font-weight: bold; font-size: 0.9em; }
        input, select { width: 100%; padding: 10px; border: 1px solid #ccc; border-radius: 4px; box-sizing: border-box; }
        .question { margin-bottom: 20px; padding: 15px; border-left: 5px solid #e0e0e0; background: #fafafa; }
        .options { margin-top: 10px; }
        .options label { font-weight: normal; cursor: pointer; display: flex; align-items: center; gap: 10px; margin-bottom: 8px; }
        button { width: 100%; padding: 15px; background: #27ae60; color: white; border: none; border-radius: 4px; font-size: 1.1em; cursor: pointer; transition: background 0.3s; }
        button:hover { background: #219150; }
    </style>
</head>
<body>

<div class="container">
    <h1>Examen de Calidad</h1>

    <form id="examenForm">
        <!-- Datos del Estudiante -->
        <div class="section-title">Datos del Estudiante</div>
        <div class="grid-inputs">
            <div>
                <label>Nombre</label>
                <input type="text" required placeholder="Ej: Juan">
            </div>
            <div>
                <label>Apellido</label>
                <input type="text" required placeholder="Ej: Pérez">
            </div>
            <div>
                <label>Cédula</label>
                <input type="text" required placeholder="V-00.000.000">
            </div>
            <div>
                <label>Sección</label>
                <input type="text" required placeholder="Ej: 101">
            </div>
            <div style="grid-column: span 2;">
                <label>Mención de su Carrera</label>
                <input type="text" required placeholder="Ej: Ingeniería Industrial">
            </div>
            <div style="grid-column: span 2;">
                <label>Nombre de la Universidad</label>
                <input type="text" required placeholder="Ej: Universidad Central">
            </div>
        </div>

        <!-- Preguntas de Selección -->
        <div class="section-title">Preguntas de Selección</div>

        <!-- Pregunta 1 -->
        <div class="question">
            <label>1. ¿Quiénes son considerados los principales fundadores y padres de la calidad moderna?</label>
            <div class="options">
                <label><input type="radio" name="q1" value="a" required> a) Henry Ford y Frederick Taylor</label>
                <label><input type="radio" name="q1" value="b"> b) W. Edwards Deming, Joseph Juran y Kaoru Ishikawa</label>
                <label><input type="radio" name="q1" value="c"> c) Steve Jobs y Bill Gates</label>
            </div>
        </div>

        <!-- Pregunta 2 -->
        <div class="question">
            <label>2. ¿En qué periodo o año se considera que inicia el movimiento de la Calidad Total (postguerra)?</label>
            <div class="options">
                <label><input type="radio" name="q2" value="a" required> a) 1950 (Década de los 50)</label>
                <label><input type="radio" name="q2" value="b"> b) 1800 (Revolución Industrial)</label>
                <label><input type="radio" name="q2" value="c"> c) 1990 (Era Digital)</label>
            </div>
        </div>

        <button type="submit">Finalizar Examen</button>
    </form>
</div>

<script>
    document.getElementById('examenForm').onsubmit = function(e) {
        e.preventDefault();
        alert('¡Examen enviado con éxito! Los datos han sido registrados en el sistema escolar.');
    };
</script>

</body>
</html>

