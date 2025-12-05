<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Año 1 · 2024-2025</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f5f5f5;
      color: #333;
    }

    header {
      background-color: #222;
      color: #fff;
      padding: 1rem 2rem;
      text-align: center;
    }

    main {
      max-width: 1000px;
      margin: 0 auto;
      padding: 1.5rem;
    }

    h1, h2 {
      margin-top: 0;
    }

    p {
      line-height: 1.5;
    }

    /* CATEGORÍAS (PÁGINA PRINCIPAL) */
    .categorias {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      gap: 1rem;
      margin-top: 1.5rem;
    }

    .categoria-card {
      background-color: #fff;
      border-radius: 8px;
      padding: 1rem;
      text-align: center;
      box-shadow: 0 2px 6px rgba(0, 0, 0, 0.1);
      cursor: pointer;
      transition: transform 0.15s ease, box-shadow 0.15s ease;
    }

    .categoria-card:hover {
      transform: translateY(-3px);
      box-shadow: 0 4px 10px rgba(0, 0, 0, 0.15);
    }

    .categoria-card h3 {
      margin: 0.5rem 0 0;
    }

    /* GALERÍA POR CATEGORÍA */
    #galeria {
      display: none;
    }

    .back-button {
      display: inline-block;
      margin-bottom: 1rem;
      padding: 0.5rem 1rem;
      background-color: #ddd;
      border-radius: 6px;
      text-decoration: none;
      color: #333;
      cursor: pointer;
    }

    .back-button:hover {
      background-color: #ccc;
    }

    .thumbnails {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(160px, 1fr));
      gap: 1rem;
    }

    .thumbnail {
      background-color: #fff;
      border-radius: 6px;
      padding: 0.5rem;
      box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
      cursor: pointer;
      text-align: center;
    }

    .thumbnail img {
      max-width: 100%;
      border-radius: 4px;
      display: block;
      margin: 0 auto;
    }

    .thumbnail span {
      display: block;
      margin-top: 0.5rem;
      font-size: 0.9rem;
      color: #555;
    }

    /* MODAL (IMAGEN GRANDE) */
    .modal {
      display: none;
      position: fixed;
      inset: 0;
      background-color: rgba(0, 0, 0, 0.7);
      justify-content: center;
      align-items: center;
      z-index: 1000;
    }

    .modal-content {
      background-color: #fff;
      max-width: 90%;
      max-height: 90%;
      padding: 1rem;
      border-radius: 8px;
      box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
    }

    .modal-image {
      max-width: 100%;
      max-height: 70vh;
      display: block;
      margin: 0 auto 0.5rem;
    }

    .modal-caption {
      text-align: center;
      font-size: 0.95rem;
      color: #444;
      margin-bottom: 0.5rem;
    }

    .modal-close {
      display: inline-block;
      padding: 0.3rem 0.8rem;
      background-color: #222;
      color: #fff;
      border-radius: 4px;
      cursor: pointer;
      font-size: 0.9rem;
    }

    .modal-close:hover {
      background-color: #444;
    }
  </style>
</head>
<body>
  <header>
    <h1>Año 1 · 2024-2025</h1>
  </header>

  <main>
    <!-- PÁGINA PRINCIPAL -->
    <section id="inicio">
      <p>
        Esta página pretende ser un baúl de los recuerdos de todos los años que estemos juntos.
        Dada mi obsesión con coleccionar objetos de nuestras experiencias, se me ha ocurrido esta página
        para recopilarlas y así unir mi mundo y el tuyo. Para que no se borren los tickets. Sin ocupar espacio innecesario.<br><br>
        He divido los objetos en <strong>Restaurantes</strong>, <strong>Viajes</strong>, <strong>Otros</strong> y <strong>Random</strong>.
        Haz clic en una categoría para ver las fotos en miniatura y después pulsa en la foto que quieras
        para verla en grande con su leyenda.<br><br>
        Espero que te guste casi tanto como me gustas tú a mí, Guillermo. Por toda una vida juntos dentro del espectro. Te quiero.
      </p>

      <h2>Categorías</h2>

      <div class="categorias" id="lista-categorias">
        <!-- Se rellena con JavaScript -->
      </div>
    </section>

    <!-- GALERÍA DE UNA CATEGORÍA -->
    <section id="galeria">
      <button class="back-button" id="volver">← Volver a las categorías</button>
      <h2 id="titulo-categoria"></h2>
      <div class="thumbnails" id="lista-fotos">
        <!-- Se rellena con JavaScript -->
      </div>
    </section>
  </main>

  <!-- MODAL -->
  <div class="modal" id="modal">
    <div class="modal-content">
      <img id="modal-img" class="modal-image" src="" alt="">
      <div id="modal-caption" class="modal-caption"></div>
      <div style="text-align:center;">
        <button id="modal-close" class="modal-close">Cerrar</button>
      </div>
    </div>
  </div>

  <script>
    // DE MOMENTO: una sola foto en "Viajes" para que comprobemos que funciona laboral.jpg
    const datosGaleria = [
      {
        id: "viajes",
        nombre: "Viajes",
        descripcion: "Fotos de viajes y escapadas.",
        fotos: [
          {
            src: "viajes/laboral.jpg",
            miniatura: "viajes/laboral.jpg",
            titulo: "Laboral",
            leyenda: "Pegatina con la que vimos las cocinas, lavandería y torre de la Laboral. Vaya potra tuvimos xd xd xd ."
          }
        ]
      }
      // Luego añadiremos Otros, Random y Restaurantes
    ];

    const seccionInicio = document.getElementById("inicio");
    const seccionGaleria = document.getElementById("galeria");
    const listaCategorias = document.getElementById("lista-categorias");
    const listaFotos = document.getElementById("lista-fotos");
    const tituloCategoria = document.getElementById("titulo-categoria");
    const botonVolver = document.getElementById("volver");

    const modal = document.getElementById("modal");
    const modalImg = document.getElementById("modal-img");
    const modalCaption = document.getElementById("modal-caption");
    const modalClose = document.getElementById("modal-close");

    // Mostrar categorías
    function cargarCategorias() {
      datosGaleria.forEach(categoria => {
        const card = document.createElement("div");
        card.className = "categoria-card";
        card.dataset.id = categoria.id;

        card.innerHTML = `
          <h3>${categoria.nombre}</h3>
          <p>${categoria.descripcion}</p>
        `;

        card.addEventListener("click", () => {
          mostrarGaleria(categoria.id);
        });

        listaCategorias.appendChild(card);
      });
    }

    // Mostrar galería de una categoría
    function mostrarGaleria(idCategoria) {
      const categoria = datosGaleria.find(cat => cat.id === idCategoria);
      if (!categoria) return;

      tituloCategoria.textContent = categoria.nombre;
      listaFotos.innerHTML = "";

      categoria.fotos.forEach(foto => {
        const thumb = document.createElement("div");
        thumb.className = "thumbnail";

        thumb.innerHTML = `
          <img src="${foto.miniatura}" alt="${foto.titulo}">
          <span>${foto.titulo}</span>
        `;

        thumb.addEventListener("click", () => {
          abrirModal(foto);
        });

        listaFotos.appendChild(thumb);
      });

      seccionInicio.style.display = "none";
      seccionGaleria.style.display = "block";
    }

    // Volver a categorías
    botonVolver.addEventListener("click", () => {
      seccionGaleria.style.display = "none";
      seccionInicio.style.display = "block";
    });

    // Modal
    function abrirModal(foto) {
      modalImg.src = foto.src;
      modalImg.alt = foto.titulo;
      modalCaption.textContent = foto.leyenda;
      modal.style.display = "flex";
    }

    modalClose.addEventListener("click", () => {
      modal.style.display = "none";
    });

    modal.addEventListener("click", (e) => {
      if (e.target === modal) {
        modal.style.display = "none";
      }
    });

    // Inicializar
    cargarCategorias();
  </script>
</body>
</html>
