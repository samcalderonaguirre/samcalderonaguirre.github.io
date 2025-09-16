---
layout: page
title: Portafolio
permalink: /portafolio/
image: portafolio.jpg
---
  <style>
    /* ------------------- ESTILOS GENERALES ------------------- */
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
      font-family: "Roboto", Arial, sans-serif;
    }

    body {
      background-color: #f4f6f9;
      color: #333;
      line-height: 1.6;
    }

    h1, h2, h3 {
      font-weight: bold;
    }

    a {
      text-decoration: none;
      color: inherit;
    }

    section {
      padding: 60px 20px;
      max-width: 1200px;
      margin: auto;
    }

    .btn {
      display: inline-block;
      background: #462cbb;
      color: #fff;
      padding: 12px 24px;
      border-radius: 5px;
      font-weight: bold;
      transition: background 0.3s;
    }

    .btn:hover {
      background: #433688;
    }

    /* ------------------- HERO ------------------- */
    .hero {
      background: linear-gradient(rgba(0,0,0,0.6), rgba(0,0,0,0.6)),
        url("https://www.nvidia.com/content/dam/en-zz/Solutions/ai-data-science/workstations/gtc/rtx-ai-workstation-bm-l580-d.jpg") no-repeat center/cover;
      color: #fff;
      text-align: center;
      padding: 100px 20px;
    }

    .hero h1 {
      font-size: 3rem;
      margin-bottom: 15px;
    }

    .hero p {
      font-size: 1.2rem;
      margin-bottom: 30px;
    }

    /* ------------------- SERVICIOS ------------------- */
    .services {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
      text-align: center;
    }

    .service {
      background: #fff;
      padding: 20px;
      border-radius: 10px;
      box-shadow: 0 4px 8px rgba(0,0,0,0.1);
      transition: transform 0.3s;
    }

    .service:hover {
      transform: translateY(-5px);
    }

    .service h3 {
      margin: 15px 0;
      color: #003366;
    }

    /* ------------------- SOBRE ------------------- */
    .about {
      text-align: center;
    }

    .about p {
      max-width: 800px;
      margin: 20px auto;
    }

    /* ------------------- TESTIMONIOS ------------------- */
    .testimonials {
      background: #003366;
      color: #fff;
      text-align: center;
    }

    .testimonial {
      max-width: 700px;
      margin: 20px auto;
      font-style: italic;
    }

    /* ------------------- CONTACTO ------------------- */
    .contact form {
      display: grid;
      gap: 15px;
      max-width: 600px;
      margin: auto;
    }

    .contact input, .contact textarea {
      padding: 12px;
      border: 1px solid #ccc;
      border-radius: 5px;
      font-size: 1rem;
    }

    .contact button {
      background: #400f6d;
      color: #fff;
      padding: 12px;
      border: none;
      border-radius: 5px;
      font-size: 1rem;
      cursor: pointer;
    }

    .contact button:hover {
      background: #55568f;
    }

    /* ------------------- FOOTER ------------------- */
    footer {
      background: #222;
      color: #aaa;
      text-align: center;
      padding: 20px;
      margin-top: 40px;
    }

    footer a {
      color: #ff6600;
    }
  </style>

  <!-- Portafolio -->
  <section>
    <h2 style="text-align:center; margin-bottom:30px;">Nuestros Servicios</h2>
    <div class="services">
      <div class="service">
        <h3>🖥️ Optimización de Laptops</h3>
        <p>Actualización de hardware y mejora de rendimiento en equipos antiguos.</p>
        <img src="{{site.baseurl}}/images/portafolio1.jpg"" alt="">
      </div>
      <div class="service">
        <h3>🔒 Recuperación de Datos</h3>
        <p>Rescate exitoso de información en discos dañados</p>
        <img src="{{site.baseurl}}/images/recovery.png"" alt="">
      </div>
      <div class="service">
        <h3>🖥️ Instalación de Software</h3>
        <p>Instalación de sistemas operativos, programas y configuraciones.</p>
        <img src="{{site.baseurl}}/images/portafolio2.jpg"" alt="">
      </div>
      <div class="service">
        <h3>🌐 Soporte Remoto y Presencial</h3>
        <p>Atención rápida vía online o visita técnica</p>
        <img src="{{site.baseurl}}/images/soporte.jpg"" alt="">
      </div>
    </div>
  </section>



