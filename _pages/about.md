---
layout: page
title: Acerca de nosotros
permalink: /about/
image: about.png
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

<!-- Acerca de Nosotros -->
<section class="py-5" id="acerca" style="background: linear-gradient(135deg, #f8f9fa, #e9ecef);">
  <div class="container">
    <div class="row align-items-center g-5">
      
      <!-- Imagen -->
      <div class="col-md-6" data-aos="fade-right">
        <div class="card border-0 shadow-lg rounded-4 overflow-hidden">
          <img src="{{site.baseurl}}/images/banner_about.png" alt="SAM TECH" 
               class="img-fluid about-img">
        </div>
      </div>

      <!-- Texto -->
      <div class="col-md-6" data-aos="fade-left">
        <div class="card border-0 shadow p-4 rounded-4 bg-white">
          <h2 class="fw-bold mb-3 text-center">
            Sobre <span class="text-primary">SAM TECH</span>
          </h2>
          <p class="text-muted mb-3 text-justify">
            En <strong>SAM TECH</strong>, fundada por <strong>Samuel Calderón Aguirre</strong>, 
            nos especializamos en brindar soluciones integrales en 
            <em>soporte técnico, mantenimiento, reparación de computadores y respaldo de datos</em>.  
            Nuestro compromiso es ofrecer un servicio profesional, confiable y adaptado a las necesidades 
            tecnológicas de cada cliente.
          </p>
          <p class="text-muted text-justify">
            Con experiencia en el área de TI, buscamos ser tu aliado estratégico para que tu equipo y tus sistemas 
            funcionen siempre al más alto nivel. Nos destacamos por la atención personalizada, la eficiencia en 
            la resolución de problemas y la pasión por la innovación tecnológica.
          </p>

          <!-- Sección de Contacto -->
          <h4 class="fw-bold text-center mt-4 mb-3">Contáctame</h4>
          <div class="d-flex flex-wrap justify-content-center gap-3">
            <a href="mailto:samcalderonaguirre1996@gmail.com" 
               class="btn btn-outline-primary rounded-pill px-3 shadow-sm">
              <i class="bi bi-envelope-fill me-2"></i> Email
            </a>
            <a href="https://wa.me/593985834795" target="_blank" 
               class="btn btn-success rounded-pill px-3 shadow-sm">
              <i class="bi bi-whatsapp me-2"></i> WhatsApp
            </a>
            <a href="https://facebook.com/sam.tech.ecuador" target="_blank" 
               class="btn rounded-pill px-3 shadow-sm" style="background:#1877f2; color:#fff;">
              <i class="bi bi-facebook me-2"></i> Facebook
            </a>
            <a href="https://instagram.com/samtechec" target="_blank" 
               class="btn rounded-pill px-3 shadow-sm" style="background:#e4405f; color:#fff;">
              <i class="bi bi-instagram me-2"></i> Instagram
            </a>
            <a href="https://x.com/samcalderonag23" target="_blank" 
               class="btn rounded-pill px-3 shadow-sm" style="background:#000; color:#fff;">
              <i class="bi bi-twitter-x me-2"></i> X
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- Estilos adicionales -->
<style>
  .about-img {
    transition: transform 0.4s ease, box-shadow 0.4s ease;
  }
  .about-img:hover {
    transform: scale(1.05);
    box-shadow: 0 8px 25px rgba(0,0,0,0.2);
  }
  .btn {
    transition: transform 0.2s ease-in-out;
  }
  .btn:hover {
    transform: translateY(-3px);
  }
  #acerca p {
    text-align: justify;
  }
</style>

<!-- Bootstrap Icons (añadir en <head> si no los tienes ya) -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap-icons@1.11.1/font/bootstrap-icons.css">
