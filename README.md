 CODIGO EN HTML


 /// Codigo html
 <!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Calculadora ABC de Construcción</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="container">
    <h1>Calculadora ABC - Construcción</h1>
    
    <form id="formulario">
      <label for="presupuesto">Presupuesto (COP):</label>
      <input type="number" id="presupuesto" required>
      
      <label for="tipo">Tipo de construcción:</label>
      <select id="tipo" required>
        <option value="casa">Casa</option>
        <option value="edificio">Edificio</option>
        <option value="puente">Puente</option>
      </select>
      
      <button type="submit">Calcular</button>
    </form>

    <div id="resultado" class="resultado">
      <!-- Aquí aparece la tabla generada -->
    </div>
  </div>

  <script src="script.js"></script>
</body>
</html>

 
