Nuestra pagina web tiene como colores principales el blanco, el naranja y el azul, a continuacion se hizo una tabla con el codigo de los colores y en donde se presentan
   
   Elemento                       Codigo color      Color                       
//////////////////////////////////////////////////////////////////////////////

    Fondo general                  `#f2f2f2`        Gris claro, suave y neutro          
    Fondo contenedor               `#ffffff`        Blanco puro                        
    Título y encabezados de tabla  `#004080`        Azul oscuro                         
    Botón principal                `#ff8000`        Naranja brillante, destaca          
    Botón hover                    `#e67300`        Naranja más oscuro, efecto dinámico 
    Bordes de campos y celdas      `#ccc` / `#ddd`  Grises claros                       


 dejamos el codigo completo de la estructuracion, diseño y funcionalidad de la pagina web del modulo de priorizacion en construcción
 
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


////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////


CODIGO CSS 


body {
  font-family: Arial, sans-serif;
  background: #f2f2f2;
  margin: 0;
  padding: 0;
}

.container {
  width: 90%;
  max-width: 900px;
  margin: 30px auto;
  background: white;
  padding: 20px;
  border-radius: 12px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

h1 {
  text-align: center;
  color: #004080;
}

form {
  display: flex;
  gap: 15px;
  justify-content: center;
  margin-bottom: 20px;
  flex-wrap: wrap;
}

form label {
  font-weight: bold;
}

form input, form select, form button {
  padding: 8px;
  border-radius: 6px;
  border: 1px solid #ccc;
}

form button {
  background: #ff8000;
  color: white;
  cursor: pointer;
  border: none;
}

form button:hover {
  background: #e67300;
}

.resultado {
  margin-top: 20px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

table th, table td {
  border: 1px solid #ddd;
  padding: 10px;
  text-align: center;
}

table th {
  background: #004080;
  color: white;
}

.resumen {
  margin-top: 15px;


///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

JAVASCRIPT FUNCIONAMIENTO


// Datos de elementos (seguridad + construcción)



const elementos = {
  seguridad: [
  
    { name: "Arnés", cls: "A", cost: 150000 },
    { name: "Cascos de seguridad", cls: "A", cost: 30000 },
    { name: "Chalecos de seguridad", cls: "A", cost: 30000 },
    { name: "Gafas de seguridad", cls: "A", cost: 10000 },
    { name: "Guantes de seguridad", cls: "A", cost: 10000 },
    { name: "Cintas de demarcación", cls: "A", cost: 35000 }
  ],
  casa: {
    bajo: [
      { name: "Excavadora", cls: "A", cost: 430000 },
      { name: "Mezcladora de concreto", cls: "A", cost: 87000 },
      { name: "Andamios y componentes", cls: "A", cost: 237000 }
    ],
    intermedio: [
      { name: "Excavadora rodillo", cls: "A", cost: 704000 },
      { name: "Volquetas", cls: "A", cost: 700000 },
      { name: "Pluma grúa", cls: "B", cost: 87000 }
    ],
    alto: [
      { name: "Camiones mixer", cls: "A", cost: 293000000 },
      { name: "Montacargas", cls: "B", cost: 500000 },
      { name: "Camioneta doble cabina", cls: "B", cost: 600000 }
    ]
  },
  edificio: {
    bajo: [
      { name: "Excavadora rodillo", cls: "A", cost: 704000 },
      { name: "Andamios y componentes", cls: "A", cost: 237000 }
    ],
    intermedio: [
      { name: "Grúa torre", cls: "A", cost: 2500000 },
      { name: "Andamios y componentes", cls: "A", cost: 475800 }
    ],
    alto: [
      { name: "Grúa torre", cls: "A", cost: 5000000 },
      { name: "Excavadora rodillo", cls: "A", cost: 704000 },
      { name: "Andamios y componentes", cls: "A", cost: 475800 }
    ]
  },
  puente: {
    bajo: [
      { name: "Piloteadora pequeña", cls: "A", cost: 1000000 }
    ],
    intermedio: [
      { name: "Piloteadora mediana", cls: "A", cost: 2000000 },
      { name: "Carros de avance", cls: "A", cost: 1744186 }
    ],
    alto: [
      { name: "Piloteadora grande", cls: "A", cost: 4000000 },
      { name: "Grúas móviles", cls: "A", cost: 1479000 }
    ]
  }
};

// Formato dinero
function formatMoney(num) {
  return num.toLocaleString("es-CO", { style: "currency", currency: "COP" });
}

// Renderizar tabla
function renderTable(items) {
  return items.map(it => `
    <tr>
      <td>${it.name}</td>
      <td>${it.cls}</td>
      <td>${formatMoney(it.cost)}</td>
    </tr>
  `).join("");
}

// Manejo de formulario
document.getElementById("formulario").addEventListener("submit", e => {
  e.preventDefault();
  
  const presupuesto = parseInt(document.getElementById("presupuesto").value);
  const tipo = document.getElementById("tipo").value;
  let seleccion = null;
  let nivel = "";

  // Siempre seguridad
  let items = [...elementos.seguridad];
  let costoSeguridad = items.reduce((s, x) => s + x.cost, 0);

  if (presupuesto < costoSeguridad) {
    document.getElementById("resultado").innerHTML = `
      <div class="resumen">
        El presupuesto ingresado es insuficiente incluso para seguridad básica.
      </div>`;
    return;
  }

  // Decidir nivel
  if (presupuesto < 10000000) {
    seleccion = elementos[tipo].bajo;
    nivel = "BAJO";
  } else if (presupuesto < 50000000) {
    seleccion = elementos[tipo].intermedio;
    nivel = "INTERMEDIO";
  } else {
    seleccion = elementos[tipo].alto;
    nivel = "ALTO";
  }

  items = items.concat(seleccion);

  let total = items.reduce((s, x) => s + x.cost, 0);

  if (total > presupuesto) {
    document.getElementById("resultado").innerHTML = `
      <div class="resumen">
        El presupuesto ingresado es insuficiente para cubrir el nivel mínimo de esta construcción.
      </div>`;
    return;
  }

  document.getElementById("resultado").innerHTML = `
    <h2>${tipo.charAt(0).toUpperCase() + tipo.slice(1)}</h2>
    <p>Nivel seleccionado por presupuesto: <b>${nivel}</b></p>
    <table>
      <thead>
        <tr>
          <th>Elemento</th>
          <th>Clasificación</th>
          <th>Costo (COP)</th>
        </tr>
      </thead>
      <tbody>
        ${renderTable(items)}
      </tbody>
    </table>
    <div class="resumen">
      <p><b>Presupuesto:</b> ${formatMoney(presupuesto)}</p>
      <p><b>Total utilizado:</b> ${formatMoney(total)}</p>
      <p><b>Disponible:</b> ${formatMoney(presupuesto - total)}</p>
    </div>
  `;
});

  
  padding: 10px;
  background: #eef;
  border-left: 4px solid #004080;
}

 
