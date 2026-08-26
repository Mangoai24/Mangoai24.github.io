<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Garritas Nails - Agendamiento de Citas</title>
  <style>
    :root {
      --green-primary: #ff85a2;
      --pink-dark: #e05275;
      --green-light: #fff0f3;
      --text-color: #4a4a4a;
      --card-bg: #ffffff;
    }

    * {
      box-sizing: border-box;
      margin: 0;
      padding: 0;
      font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }

    body {
      background-color: var(--pink-light);
      color: var(--text-color);
      display: flex;
      justify-content: center;
      padding: 20px;
    }

    .container {
      width: 100%;
      max-width: 600px;
      background: var(--card-bg);
      border-radius: 16px;
      box-shadow: 0 8px 24px rgba(0,0,0,0.08);
      padding: 24px;
    }

    header {
      text-align: center;
      margin-bottom: 24px;
    }

    header h1 {
      color: var(--pink-dark);
      font-size: 1.8rem;
    }

    header p {
      color: #777;
      font-size: 0.95rem;
    }

    .form-group {
      margin-bottom: 20px;
    }

    label {
      display: block;
      font-weight: 600;
      margin-bottom: 8px;
    }

    select, input[type="date"] {
      width: 100%;
      padding: 12px;
      border: 2px solid #eee;
      border-radius: 8px;
      font-size: 1rem;
      outline: none;
      transition: border-color 0.3s;
    }

    select:focus, input[type="date"]:focus {
      border-color: var(--pink-primary);
    }

    .btn {
      width: 100%;
      padding: 14px;
      border: none;
      border-radius: 8px;
      font-size: 1rem;
      font-weight: bold;
      cursor: pointer;
      transition: background 0.3s;
    }

    .btn-primary {
      background-color: var(--pink-primary);
      color: white;
    }

    .btn-primary:hover {
      background-color: var(--pink-dark);
    }

    .btn-danger {
      background-color: #ff4d4d;
      color: white;
      margin-top: 10px;
    }

    .btn-danger:hover {
      background-color: #cc0000;
    }

    .cita-card {
      background-color: var(--pink-light);
      border: 2px dashed var(--pink-primary);
      border-radius: 8px;
      padding: 16px;
      margin-top: 20px;
    }

    .cita-card h3 {
      color: var(--pink-dark);
      margin-bottom: 10px;
    }

    .cita-detalles p {
      margin-bottom: 6px;
      font-size: 0.95rem;
    }

    .oculto {
      display: none;
    }
  </style>
</head>
<body>

  <div class="container">
    <header>
      <h1>🐾Garritas Nails</h1>
      <p>Reserva tu cita</p>
    </header>

    <div id="seccion-formulario">
      <form id="form-agendar">
        <div class="form-group">
          <label for="servicio">Servicio Especializado:</label>
          <select id="servicio" required>
            <option value="" disabled selected>Selecciona un servicio</option>
            <option value="Soft Gel">Soft Gel (~4 hrs)</option>
            <option value="PressOn">PressOn (~4 hrs)</option>
          </select>
        </div>

        <div class="form-group">
          <label for="fecha">Fecha de la Cita:</label>
          <input type="date" id="fecha" required>
        </div>

        <div class="form-group">
          <label for="horario">Horarios Disponibles (Bloques de 4 hrs):</label>
          <select id="horario" required>
            <option value="" disabled selected>Selecciona un horario</option>
            <option value="09:00 AM - 01:00 PM">09:00 AM - 01:00 PM</option>
            <option value="01:00 PM - 05:00 PM">01:00 PM - 05:00 PM</option>
            <option value="02:00 PM - 06:00 PM">02:00 PM - 06:00 PM</option>
          </select>
        </div>

        <button type="submit" class="btn btn-primary">Confirmar y Agendar Cita</button>
      </form>
    </div>

    <div id="seccion-cita" class="cita-card oculto">
      <h3>📅 Tu Cita Agendada</h3>
      <div class="cita-detalles">
        <p><strong>Servicio:</strong> <span id="det-servicio"></span></p>
        <p><strong>Fecha:</strong> <span id="det-fecha"></span></p>
        <p><strong>Horario:</strong> <span id="det-horario"></span></p>
        <p><strong>Estado:</strong> <span style="color: green; font-weight: bold;">Confirmada</span></p>
      </div>
      <button id="btn-cancelar" class="btn btn-danger">Cancelar Cita</button>
    </div>
  </div>

  <script>
    // Referencias a elementos del DOM
    const formAgendar = document.getElementById('form-agendar');
    const inputFecha = document.getElementById('fecha');
    const selectServicio = document.getElementById('servicio');
    const selectHorario = document.getElementById('horario');
    
    const seccionFormulario = document.getElementById('seccion-formulario');
    const seccionCita = document.getElementById('seccion-cita');
    const btnCancelar = document.getElementById('btn-cancelar');

    const detServicio = document.getElementById('det-servicio');
    const detFecha = document.getElementById('det-fecha');
    const detHorario = document.getElementById('det-horario');

    // Deshabilitar fechas pasadas en el input date
    const hoy = new Date().toISOString().split('T')[0];
    inputFecha.setAttribute('min', hoy);

    // Cargar cita al iniciar la página desde LocalStorage
    document.addEventListener('DOMContentLoaded', cargarCita);

    // Evento de submit del formulario
    formAgendar.addEventListener('submit', function(e) {
      e.preventDefault();

      const citaData = {
        servicio: selectServicio.value,
        fecha: inputFecha.value,
        horario: selectHorario.value
      };

      // Guardar en almacenamiento local
      localStorage.setItem('cita_garritas', JSON.stringify(citaData));
      
      mostrarCita(citaData);
      alert('¡Tu cita ha sido agendada con éxito!');
    });

    // Evento para cancelar la cita
    btnCancelar.addEventListener('click', function() {
      const confirmar = confirm('¿Estás segura de que deseas cancelar tu cita en Garritas Nails?');
      if (confirmar) {
        localStorage.removeItem('cita_garritas');
        ocultarCita();
        formAgendar.reset();
        alert('Tu cita ha sido cancelada.');
      }
    });

    // Función para mostrar los detalles de la cita
    function mostrarCita(cita) {
      detServicio.textContent = cita.servicio;
      detFecha.textContent = cita.fecha;
      detHorario.textContent = cita.horario;

      seccionFormulario.classList.add('oculto');
      seccionCita.classList.remove('oculto');
    }

    // Función para ocultar la cita y mostrar el formulario
    function ocultarCita() {
      seccionCita.classList.add('oculto');
      seccionFormulario.classList.remove('oculto');
    }

    // Función para revisar si existe una cita agendada previamente
    function cargarCita() {
      const citaGuardada = localStorage.getItem('cita_garritas');
      if (citaGuardada) {
        mostrarCita(JSON.parse(citaGuardada));
      }
    }
  </script>
</body>
</html>
