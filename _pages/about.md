---
layout: page
title: Sobre Nosotros
permalink: /about/
image: profile8.png
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
      background: #ff6600;
      color: #fff;
      padding: 12px 24px;
      border-radius: 5px;
      font-weight: bold;
      transition: background 0.3s;
    }

    .btn:hover {
      background: #e65c00;
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
      background: #ff6600;
      color: #fff;
      padding: 12px;
      border: none;
      border-radius: 5px;
      font-size: 1rem;
      cursor: pointer;
    }

    .contact button:hover {
      background: #e65c00;
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


 <!-- SOBRE -->
  <section class="about">
    <h2>Sobre Nosotros</h2>
    <p>En <b>SAM TECH</b> contamos con experiencia en reparación de equipos, soporte técnico y soluciones TI. 
    Nuestro compromiso es ayudarte a mantener tus sistemas funcionando al máximo rendimiento con un servicio confiable y profesional.</p>
  </section> 

  <!-- TESTIMONIOS -->
  <section class="testimonials">
    <h2>Testimonios</h2>
    <p class="testimonial">"Gracias a SAM TECH recuperé mi laptop en menos de 24 horas, servicio excelente y rápido."</p>
    <p class="testimonial">"Muy profesionales, solucionaron mis problemas de red en la oficina. 100% recomendados."</p>
  </section>

 <!-- CONTACTO -->
  <section class="contact" id="contact">
    <h2 style="text-align:center; margin-bottom:30px;">Contáctanos por WhatsApp</h2>
    <form>
      <input type="text" placeholder="Tu Nombre" required />
      <input type="email" placeholder="Tu Correo" required />
      <textarea rows="5" placeholder="Escribe tu mensaje..." required></textarea>
      <button type="submit">Enviar Mensaje</button>
    </form>
    <div style="text-align:center; margin-top:20px;">
      <a class="btn" href="https://wa.me/593999999999" target="_blank">📱 Escríbenos por WhatsApp</a>
    </div>
  </section>