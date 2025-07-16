# malla-enfermeria
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Malla Enfermería - Finis Terrae</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <h1>Malla Curricular Enfermería</h1>
  <div id="filters">
    <label>Filtrar por línea:</label>
    <select id="filterLine">
      <option value="todas">Todas</option>
      <option value="basica">Formación Básica</option>
      <option value="humanista">Formación Humanista</option>
      <option value="disciplinar">Formación Disciplinar</option>
      <option value="investigacion">Investigación</option>
      <option value="gestion">Gestión e Informática</option>
      <option value="general">Formación General</option>
    </select>
  </div>

  <div id="mallaContainer"></div>

  <script src="script.js"></script>
</body>
</html>
body {
  font-family: sans-serif;
  background: #f9f9f9;
  padding: 20px;
}
h1 {
  text-align: center;
  color: #005F73;
}
#mallaContainer {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 12px;
  margin-top: 20px;
}
.semestre {
  background: #fff;
  border: 1px solid #ccc;
  padding: 10px;
  border-radius: 8px;
}
.asignatura {
  background: #cce5ff;
  margin: 5px 0;
  padding: 5px;
  border-radius: 4px;
  font-size: 14px;
}
.basica { background-color: #b3e5fc; }
.humanista { background-color: #dcedc8; }
.disciplinar { background-color: #fff9c4; }
.investigacion { background-color: #ffccbc; }
.gestion { background-color: #e1bee7; }
.general { background-color: #f0f4c3; }
const malla = [
  {
    semestre: "Semestre 1",
    ramos: [
      { nombre: "Anatomía", linea: "basica" },
      { nombre: "Introducción a las Ciencias Básicas", linea: "basica" },
      { nombre: "Bioquímica y Biología Celular", linea: "basica" },
      { nombre: "Antropología Filosófica", linea: "humanista" },
      { nombre: "Psicología del Desarrollo", linea: "humanista" },
      { nombre: "Prevención de Infecciones", linea: "disciplinar" },
      { nombre: "Primeros Auxilios", linea: "disciplinar" },
      { nombre: "Identidad Personal", linea: "general" },
      { nombre: "Inglés I", linea: "general" },
    ]
  },
  {
    semestre: "Semestre 2",
    ramos: [
      { nombre: "Microbiología", linea: "basica" },
      { nombre: "Salud y Sociedad Contemporánea", linea: "humanista" },
      { nombre: "Fundamentos de Enfermería", linea: "disciplinar" },
      { nombre: "Comunicación Efectiva", linea: "general" },
      { nombre: "Introducción al Pensamiento Filosófico", linea: "general" },
    ]
  },
  // Puedes seguir completando todos los semestres igual...
];

function renderMalla(filtro = "todas") {
  const container = document.getElementById("mallaContainer");
  container.innerHTML = "";
  malla.forEach(sem => {
    const box = document.createElement("div");
    box.className = "semestre";
    const title = document.createElement("h3");
    title.textContent = sem.semestre;
    box.appendChild(title);

    sem.ramos.forEach(ramo => {
      if (filtro === "todas" || ramo.linea === filtro) {
        const div = document.createElement("div");
        div.className = `asignatura ${ramo.linea}`;
        div.textContent = ramo.nombre;
        box.appendChild(div);
      }
    });

    container.appendChild(box);
  });
}

document.getElementById("filterLine").addEventListener("change", (e) => {
  renderMalla(e.target.value);
});

renderMalla();
