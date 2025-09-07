<!DOCTYPE html>
<html lang="es" class="scroll-smooth">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Grupo Mortiz S.A. - Soluciones Logísticas</title>
    
    <!-- Tailwind CSS CDN -->
    <script src="https://cdn.tailwindcss.com"></script>
    
    <!-- Google Fonts: Roboto -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap" rel="stylesheet">
    
    <!-- Font Awesome for Icons -->
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css">

    <!-- Configuración de Tailwind para Modo Oscuro -->
    <script>
        tailwind.config = {
            darkMode: 'class',
        }
    </script>

    <!-- Estilos Personalizados -->
    <style>
        body {
            font-family: 'Roboto', sans-serif;
            transition: background-color 0.5s ease, color 0.5s ease;
        }
        :root {
            --primary-blue: #003366;
            --secondary-blue: #00509E;
            --light-gray: #f8f9fa;
        }
        
        /* --- Fondos Animados --- */
        #background-canvas {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            transition: opacity 0.5s ease-in-out;
        }

        /* --- Estilos Generales y Modo Claro --- */
        .text-primary { color: var(--primary-blue); }
        .bg-primary { background-color: var(--primary-blue); }
        .btn-primary {
            background-color: var(--primary-blue);
            color: white;
            transition: all 0.3s ease;
            border: 2px solid transparent;
        }
        .btn-primary:hover { 
            background-color: var(--secondary-blue);
            transform: translateY(-3px);
            box-shadow: 0 6px 15px rgba(0, 80, 158, 0.25);
        }
        .nav-link { transition: color 0.3s ease; }
        .nav-link:hover, .nav-link.active { color: var(--primary-blue); }

        .title-gradient {
            background: linear-gradient(90deg, var(--secondary-blue), var(--primary-blue));
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .info-card {
            transition: transform 0.3s ease, box-shadow 0.3s ease;
            background-color: rgba(255, 255, 255, 0.8);
            backdrop-filter: blur(5px);
        }
        .info-card:hover {
            transform: translateY(-8px);
            box-shadow: 0 15px 30px rgba(0,0,0,0.1);
        }

        .logo-text {
            color: #c00; /* Un rojo corporativo fuerte */
            text-shadow: 1px 1px 2px rgba(0,0,0,0.1);
            transition: transform 0.3s ease;
        }
        .logo-text:hover {
            transform: scale(1.05);
        }
        
        /* --- Estilos Modo Oscuro "Galaxia" --- */
        .dark .text-primary { color: #60a5fa; }
        .dark .nav-link:hover, .dark .nav-link.active { color: #93c5fd; }

        .dark .title-gradient {
             background: linear-gradient(90deg, #93c5fd, #60a5fa);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        .dark .info-card {
            background: rgba(17, 24, 39, 0.6); /* bg-gray-900 con alpha */
            border: 1px solid rgba(255, 255, 255, 0.1);
            backdrop-filter: blur(10px);
            position: relative;
            overflow: hidden;
        }
        .dark .info-card:hover {
             box-shadow: 0 10px 30px rgba(0, 80, 158, 0.3);
        }
        .dark .logo-text {
            color: #ef4444; /* Rojo 500 para mejor visibilidad */
            text-shadow: 1px 1px 4px rgba(255, 255, 255, 0.1);
        }
        /* Efecto Aurora */
        .dark .info-card::before {
            content: '';
            position: absolute;
            top: 0; left: 0;
            width: 100%; height: 100%;
            background: radial-gradient(800px circle at var(--mouse-x) var(--mouse-y), rgba(96, 165, 250, 0.15), transparent 40%);
            z-index: 0;
            opacity: 0;
            transition: opacity 0.5s;
        }
        .dark .info-card:hover::before {
            opacity: 1;
        }
        .dark .info-card > * {
            position: relative;
            z-index: 1;
        }

        /* --- Estilos para "Otros Servicios" --- */
        @property --angle { syntax: '<angle>'; inherits: false; initial-value: 0deg; }
        @keyframes rotate { to { --angle: 360deg; } }
        .cta-card {
            --angle: 0deg;
            border: 4px solid;
            border-image: conic-gradient(from var(--angle), #003366, #00509E, #003366) 1;
            animation: rotate 5s linear infinite;
        }
        .dark .cta-card {
             border-image: conic-gradient(from var(--angle), #60a5fa, #93c5fd, #60a5fa) 1;
        }
        .cta-button {
            background: linear-gradient(90deg, var(--secondary-blue), var(--primary-blue));
            animation: pulse 2s infinite;
        }
        .dark .cta-button {
            background: linear-gradient(90deg, #93c5fd, #60a5fa);
            box-shadow: 0 0 20px #60a5fa;
        }
        @keyframes pulse { 0%, 100% { transform: scale(1); box-shadow: 0 0 10px transparent; } 50% { transform: scale(1.05); box-shadow: 0 0 20px var(--secondary-blue); } }
        
        /* Animaciones y Menú Móvil */
        main > section:not(.hidden) { animation: fadeIn 0.6s ease-in-out; }
        @keyframes fadeIn { from { opacity: 0; transform: translateY(15px); } to { opacity: 1; transform: translateY(0); } }
        #mobile-menu { transition: transform 0.3s ease-in-out; }
        .body-no-scroll { overflow: hidden; }
    </style>
</head>
<body class="bg-white text-gray-800 dark:bg-gray-900 dark:text-gray-300">
    
    <canvas id="background-canvas"></canvas>

    <!-- Barra Superior -->
    <div class="bg-gray-100/80 dark:bg-gray-800/80 backdrop-blur-sm text-center py-2 text-sm text-gray-600 dark:text-gray-400">
        <p>¡Llámanos! +507 64018721</p>
    </div>

    <!-- Encabezado y Navegación -->
    <header class="sticky top-0 bg-white/80 dark:bg-gray-900/80 backdrop-blur-sm shadow-md z-50">
        <div class="container mx-auto px-6 py-4 flex justify-between items-center">
            <a href="#inicio" class="text-3xl font-extrabold tracking-wider logo-text">
                GMSA
            </a>
            <div class="flex items-center space-x-4 md:space-x-6">
                <nav class="hidden md:flex space-x-8 items-center">
                    <a href="#inicio" class="nav-link active font-medium text-gray-600 dark:text-gray-300">Inicio</a>
                    <a href="#nosotros" class="nav-link font-medium text-gray-600 dark:text-gray-300">Nosotros</a>
                    <a href="#servicios" class="nav-link font-medium text-gray-600 dark:text-gray-300">Servicios</a>
                    <a href="#otros-servicios" class="nav-link font-medium text-gray-600 dark:text-gray-300">Otros Servicios</a>
                    <a href="#contacto" class="nav-link font-medium text-gray-600 dark:text-gray-300">Contacto</a>
                </nav>
                <button id="theme-toggle" class="text-gray-500 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-gray-700 focus:outline-none rounded-lg text-sm p-2.5">
                    <i id="theme-toggle-dark-icon" class="fas fa-moon fa-lg hidden"></i>
                    <i id="theme-toggle-light-icon" class="fas fa-sun fa-lg hidden"></i>
                </button>
                <div class="md:hidden">
                    <button id="menu-btn" class="text-primary dark:text-blue-400 focus:outline-none z-50">
                        <i class="fas fa-bars fa-lg"></i>
                    </button>
                </div>
            </div>
        </div>
    </header>
    
    <!-- Menú Móvil -->
    <div id="mobile-menu" class="md:hidden fixed top-0 left-0 w-full h-full bg-white/95 dark:bg-gray-900/95 backdrop-blur-sm transform -translate-x-full z-50">
         <div class="container mx-auto px-6 py-4 flex justify-end">
             <button id="close-btn" class="text-primary dark:text-blue-400 focus:outline-none">
                 <i class="fas fa-times fa-lg"></i>
             </button>
         </div>
        <nav class="flex flex-col items-center justify-center h-full space-y-8 -mt-16">
            <a href="#inicio" class="text-2xl text-gray-700 dark:text-gray-300 mobile-nav-link">Inicio</a>
            <a href="#nosotros" class="text-2xl text-gray-700 dark:text-gray-300 mobile-nav-link">Nosotros</a>
            <a href="#servicios" class="text-2xl text-gray-700 dark:text-gray-300 mobile-nav-link">Servicios</a>
            <a href="#otros-servicios" class="text-2xl text-gray-700 dark:text-gray-300 mobile-nav-link">Otros Servicios</a>
            <a href="#contacto" class="text-2xl text-gray-700 dark:text-gray-300 mobile-nav-link">Contacto</a>
        </nav>
    </div>

    <main>
        <!-- Sección de Inicio -->
        <section id="inicio">
            <div class="h-[80vh] flex items-center justify-center text-center relative">
                <div class="relative z-10 px-4">
                    <h1 class="text-4xl md:text-6xl font-bold mb-4 title-gradient">Tu Beneficio es Nuestro Punto de Partida</h1>
                     <p class="max-w-3xl mx-auto text-gray-600 dark:text-gray-300 mb-8 text-lg">
                        Suministro e instalación de equipos para almacenamientos, estanterías pesadas (racks) y mobiliario de oficina.
                    </p>
                    <a href="#contacto" class="btn-primary py-3 px-8 rounded-md font-medium text-lg">Solicitar Información</a>
                </div>
            </div>
             <div class="container mx-auto px-6 py-16 text-center">
                <h2 class="text-3xl md:text-4xl font-bold title-gradient mb-4">BIENVENIDOS A GRUPO MORTIZ S.A.</h2>
                <p class="max-w-3xl mx-auto text-gray-600 dark:text-gray-400">
                    Nuestro compromiso es proporcionar un servicio eficiente y confiable para ayudar a su negocio a crecer. Explore nuestros servicios y descubra cómo podemos facilitar su operación.
                </p>
            </div>
        </section>

        <!-- Sección Nosotros -->
        <section id="nosotros" class="py-20 bg-light-gray dark:bg-primary dark:text-white hidden">
            <div class="container mx-auto px-6 max-w-5xl text-center">
                <h2 class="text-3xl md:text-4xl font-bold mb-12 title-gradient dark:text-white">Nuestra Identidad</h2>
                 <div class="grid md:grid-cols-2 gap-12 text-left">
                     <div class="info-card p-6 border border-gray-200 dark:border-gray-700 rounded-lg">
                        <h3 class="text-2xl font-bold mb-4 text-primary dark:text-white">Misión</h3>
                        <p class="text-gray-600 dark:text-gray-300">Ofrecer soluciones integrales de almacenamiento y gestión logística que optimicen la cadena de suministro de nuestros clientes.</p>
                     </div>
                     <div class="info-card p-6 border border-gray-200 dark:border-gray-700 rounded-lg">
                        <h3 class="text-2xl font-bold mb-4 text-primary dark:text-white">Visión</h3>
                        <p class="text-gray-600 dark:text-gray-300">Ser el aliado estratégico líder en soluciones logísticas de almacenamiento en América Latina.</p>
                     </div>
                 </div>
                 <div class="mt-12">
                     <h3 class="text-2xl font-bold mb-4 text-center text-primary dark:text-white">Valores</h3>
                     <div class="flex flex-wrap justify-center gap-4 text-sm">
                         <span class="bg-primary/10 dark:bg-white/10 text-primary dark:text-white rounded-full px-5 py-2">Innovación</span>
                         <span class="bg-primary/10 dark:bg-white/10 text-primary dark:text-white rounded-full px-5 py-2">Servicio</span>
                         <span class="bg-primary/10 dark:bg-white/10 text-primary dark:text-white rounded-full px-5 py-2">Calidad</span>
                         <span class="bg-primary/10 dark:bg-white/10 text-primary dark:text-white rounded-full px-5 py-2">Puntualidad</span>
                         <span class="bg-primary/10 dark:bg-white/10 text-primary dark:text-white rounded-full px-5 py-2">Responsabilidad</span>
                     </div>
                 </div>
            </div>
        </section>

        <!-- Sección Servicios -->
        <section id="servicios" class="py-20 hidden">
            <div class="container mx-auto px-6 text-center">
                <h2 class="text-3xl md:text-4xl font-bold title-gradient mb-12">Expertos en Estanterías y Racks</h2>
                <div class="max-w-3xl mx-auto info-card p-8 rounded-lg border border-gray-200 dark:border-gray-700 text-left">
                    <ul class="space-y-4 text-gray-700 dark:text-gray-300">
                        <li><i class="fas fa-check-circle text-primary mr-3"></i>Estanterías para carga pesada, mediana y carga ligera.</li>
                        <li><i class="fas fa-check-circle text-primary mr-3"></i>Parrillas electro soldadas</li>
                        <li><i class="fas fa-check-circle text-primary mr-3"></i>Lockers metálicos y de madera</li>
                        <li><i class="fas fa-check-circle text-primary mr-3"></i>Puertas seccionales, enrollables y corredizas</li>
                        <li><i class="fas fa-check-circle text-primary mr-3"></i>Archivos rodantes y estanterías</li>
                        <li><i class="fas fa-check-circle text-primary mr-3"></i>Extractores industriales</li>
                        <li><i class="fas fa-check-circle text-primary mr-3"></i>Equipos de seguridad</li>
                    </ul>
                </div>
            </div>
        </section>

        <!-- Otros Servicios Section -->
        <section id="otros-servicios" class="py-20 hidden">
            <div class="container mx-auto px-6 text-center">
                 <div class="max-w-3xl mx-auto info-card cta-card p-8 md:p-12 rounded-lg">
                    <h2 class="text-3xl md:text-4xl font-bold title-gradient mb-4">Explore Nuestros Servicios Creativos</h2>
                    <p class="text-gray-600 dark:text-gray-300 mb-8 max-w-xl mx-auto">
                        Además de nuestras soluciones logísticas, nuestro equipo asociado en SlideStrateck se especializa en diseño de presentaciones y desarrollo web a medida. Descubra un mundo de creatividad.
                    </p>
                    <a href="https://slidestrateck-sudo.github.io/SlideStrateck-sitio/#Servicios" target="_blank" class="cta-button inline-block text-white font-bold py-4 px-10 rounded-lg text-lg">
                        Ver Servicios Creativos
                    </a>
                </div>
            </div>
        </section>
        
        <!-- Sección Contacto -->
        <section id="contacto" class="py-20 hidden">
            <div class="container mx-auto px-6 max-w-2xl">
                <div class="info-card p-8 md:p-12 rounded-lg border border-gray-200 dark:border-gray-700">
                    <div class="text-center">
                        <h2 class="text-3xl md:text-4xl font-bold title-gradient mb-2">Cuéntanos qué necesitas</h2>
                        <p class="text-gray-600 dark:text-gray-400 mb-8">Comunícate con nosotros.</p>
                    </div>
                     <form id="contact-form" action="https://api.web3forms.com/submit" method="POST" class="space-y-4">
                        <input type="hidden" name="access_key" value="b52bef7e-3d3b-4e1a-831b-e491c5f133a5">
                        <input type="text" name="name" placeholder="Nombre" class="w-full p-3 border border-gray-300 bg-gray-50 dark:border-gray-600 dark:bg-gray-800 rounded-md focus:outline-none focus:ring-2 focus:ring-primary focus:border-primary" required>
                        <input type="email" name="email" placeholder="Correo electrónico*" class="w-full p-3 border border-gray-300 bg-gray-50 dark:border-gray-600 dark:bg-gray-800 rounded-md focus:outline-none focus:ring-2 focus:ring-primary focus:border-primary" required>
                        <input type="tel" name="phone" placeholder="Teléfono" class="w-full p-3 border border-gray-300 bg-gray-50 dark:border-gray-600 dark:bg-gray-800 rounded-md focus:outline-none focus:ring-2 focus:ring-primary focus:border-primary">
                        <textarea name="message" placeholder="Otras notas" rows="4" class="w-full p-3 border border-gray-300 bg-gray-50 dark:border-gray-600 dark:bg-gray-800 rounded-md focus:outline-none focus:ring-2 focus:ring-primary focus:border-primary"></textarea>
                        <div class="text-center">
                            <button type="submit" class="btn-primary py-3 px-12 rounded-md font-medium text-lg">Enviar</button>
                        </div>
                     </form>
                     <div id="form-result" class="mt-4 text-center text-lg"></div>
                </div>
            </div>
        </section>
    </main>

    <!-- Pie de Página -->
    <footer class="bg-primary text-white">
        <div class="container mx-auto px-6 py-12">
            <div class="grid md:grid-cols-3 gap-8 text-center md:text-left">
                <div>
                    <h4 class="font-bold text-lg mb-2">GRUPO MORTIZ S.A.</h4>
                    <p class="text-gray-300">Panamá, República de Panamá</p>
                </div>
                <div>
                     <h4 class="font-bold text-lg mb-2">Contacto</h4>
                     <p class="text-gray-300">¡Llámanos! +507 64018721</p>
                     <p class="text-gray-300">ventas@grupomortiz.net</p>
                </div>
                <div class="text-center">
                    <h4 class="font-bold text-lg mb-2">Síguenos</h4>
                    <div class="flex justify-center md:justify-start space-x-4">
                        <a href="https://www.facebook.com/p/Estanter%C3%ADas-GMSA-100076173377051/?locale=es_LA" target="_blank" class="text-gray-300 hover:text-white"><i class="fab fa-facebook-f fa-lg"></i></a>
                        <a href="https://www.instagram.com/estanterias.gmsa/" target="_blank" class="text-gray-300 hover:text-white"><i class="fab fa-instagram fa-lg"></i></a>
                        <a href="https://www.tiktok.com/@estanterias.gmsa" target="_blank" class="text-gray-300 hover:text-white"><i class="fab fa-tiktok fa-lg"></i></a>
                    </div>
                </div>
            </div>
             <div class="border-t border-blue-800 mt-8 pt-6 text-center text-gray-400 text-sm">
                 <div class="flex flex-wrap justify-center space-x-6 mb-4">
                     <a href="#inicio" class="hover:text-white">Inicio</a>
                     <a href="#nosotros" class="hover:text-white">Nosotros</a>
                     <a href="#servicios" class="hover:text-white">Servicios</a>
                     <a href="#otros-servicios" class="hover:text-white">Otros Servicios</a>
                     <a href="#contacto" class="hover:text-white">Contacto</a>
                 </div>
                <p>COPYRIGHT © 2025 GRUPO MORTIZ S.A. - TODOS LOS DERECHOS RESERVADOS.</p>
            </div>
        </div>
    </footer>

    <!-- Botón Flotante de WhatsApp -->
    <a href="https://wa.me/50764018721" target="_blank" class="fixed bottom-6 right-6 bg-green-500 text-white w-14 h-14 rounded-full flex items-center justify-center shadow-lg hover:bg-green-600 transition-all duration-300 z-40">
        <i class="fab fa-whatsapp fa-2x"></i>
    </a>
    
    <!-- Scripts -->
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const canvas = document.getElementById('background-canvas');
            const ctx = canvas.getContext('2d');
            let animationFrameId;

            // --- LÓGICA DE ANIMACIÓN DE FONDOS ---
            const setupCanvas = () => {
                canvas.width = window.innerWidth;
                canvas.height = window.innerHeight;
            };

            // Animación Galaxia (Modo Oscuro)
            let stars = [];
            const createGalaxy = () => {
                stars = [];
                const starCount = window.innerWidth / 4;
                for (let i = 0; i < starCount; i++) {
                    stars.push({
                        x: Math.random() * canvas.width,
                        y: Math.random() * canvas.height,
                        radius: Math.random() * 1.2,
                        vx: Math.floor(Math.random() * 50) - 25,
                        vy: Math.floor(Math.random() * 50) - 25
                    });
                }
            };
            const drawGalaxy = () => {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                ctx.globalCompositeOperation = "lighter";
                for (let i = 0; i < stars.length; i++) {
                    const s = stars[i];
                    ctx.fillStyle = "#fff";
                    ctx.beginPath();
                    ctx.arc(s.x, s.y, s.radius, 0, 2 * Math.PI);
                    ctx.fill();
                    s.x += s.vx / 500;
                    s.y += s.vy / 500;
                    if (s.x < 0 || s.x > canvas.width) s.vx = -s.vx;
                    if (s.y < 0 || s.y > canvas.height) s.vy = -s.vy;
                }
                animationFrameId = requestAnimationFrame(drawGalaxy);
            };
            
            // Animación Blueprint (Modo Claro)
            let lines = [];
            const createBlueprint = () => {
                lines = [];
                const lineCount = 30;
                for (let i = 0; i < lineCount; i++) {
                    lines.push({
                        x: Math.random() * canvas.width,
                        y: Math.random() * canvas.height,
                        length: Math.random() * 200 + 50,
                        speed: Math.random() * 0.3 + 0.1,
                        angle: Math.random() * 2 * Math.PI,
                        width: Math.random() > 0.9 ? 2 : 1,
                        direction: Math.random() > 0.5 ? 1 : -1
                    });
                }
            };
            const drawBlueprint = () => {
                ctx.clearRect(0,0,canvas.width, canvas.height);
                ctx.strokeStyle = 'rgba(0, 80, 158, 0.15)';
                lines.forEach(line => {
                    ctx.lineWidth = line.width;
                    ctx.beginPath();
                    ctx.moveTo(line.x, line.y);
                    line.x += Math.cos(line.angle) * line.speed;
                    line.y += Math.sin(line.angle) * line.speed;
                    line.angle += line.direction * 0.002;
                    if (line.x < 0 || line.x > canvas.width || line.y < 0 || line.y > canvas.height) {
                         Object.assign(line, { x: Math.random() * canvas.width, y: Math.random() * canvas.height });
                    }
                    ctx.lineTo(line.x + Math.cos(line.angle) * line.length, line.y + Math.sin(line.angle) * line.length);
                    ctx.stroke();
                });
                animationFrameId = requestAnimationFrame(drawBlueprint);
            };

            // --- LÓGICA PARA CAMBIAR DE TEMA ---
            const themeToggleBtn = document.getElementById('theme-toggle');
            const darkIcon = document.getElementById('theme-toggle-dark-icon');
            const lightIcon = document.getElementById('theme-toggle-light-icon');
            const htmlEl = document.documentElement;

            const applyTheme = (theme) => {
                cancelAnimationFrame(animationFrameId);
                if (theme === 'dark') {
                    htmlEl.classList.add('dark');
                    darkIcon.classList.remove('hidden');
                    lightIcon.classList.add('hidden');
                    createGalaxy();
                    drawGalaxy();
                } else {
                    htmlEl.classList.remove('dark');
                    darkIcon.classList.add('hidden');
                    lightIcon.classList.remove('hidden');
                    createBlueprint();
                    drawBlueprint();
                }
            };
            
            setupCanvas();
            const savedTheme = localStorage.getItem('theme') || (window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light');
            applyTheme(savedTheme);

            themeToggleBtn.addEventListener('click', () => {
                const newTheme = htmlEl.classList.contains('dark') ? 'light' : 'dark';
                localStorage.setItem('theme', newTheme);
                applyTheme(newTheme);
            });
            window.addEventListener('resize', () => {
                setupCanvas();
                const currentTheme = htmlEl.classList.contains('dark') ? 'dark' : 'light';
                if(currentTheme === 'dark') createGalaxy(); else createBlueprint();
            });

            // --- LÓGICA DEL MENÚ MÓVIL ---
            const menuBtn = document.getElementById('menu-btn');
            const closeBtn = document.getElementById('close-btn');
            const mobileMenu = document.getElementById('mobile-menu');
            const mobileNavLinks = document.querySelectorAll('.mobile-nav-link');
            const body = document.body;
            function openMenu() { mobileMenu.classList.remove('-translate-x-full'); body.classList.add('body-no-scroll'); }
            function closeMenu() { mobileMenu.classList.add('-translate-x-full'); body.classList.remove('body-no-scroll'); }
            menuBtn.addEventListener('click', openMenu);
            closeBtn.addEventListener('click', closeMenu);
            mobileNavLinks.forEach(link => link.addEventListener('click', closeMenu));
            
            // --- LÓGICA DE NAVEGACIÓN (SPA) ---
            const pageSections = document.querySelectorAll('main > section');
            const allNavLinks = document.querySelectorAll('header nav a, footer a');
            function showPage(pageId) {
                const targetId = (pageId && document.getElementById(pageId)) ? pageId : 'inicio';
                pageSections.forEach(section => section.classList.toggle('hidden', section.id !== targetId));
                allNavLinks.forEach(link => link.classList.toggle('active', link.getAttribute('href') === `#${targetId}`));
            }
            function handleNavigation() { const hash = window.location.hash.substring(1); showPage(hash); }
            window.addEventListener('hashchange', handleNavigation);
            handleNavigation();

            // --- LÓGICA DEL FORMULARIO DE CONTACTO ---
            const form = document.getElementById('contact-form');
            const result = document.getElementById('form-result');
            form.addEventListener('submit', function(e) {
                e.preventDefault();
                const formData = new FormData(form);
                const object = {};
                formData.forEach((value, key) => object[key] = value);
                const json = JSON.stringify(object);
                result.innerHTML = "Enviando...";
                fetch('https://api.web3forms.com/submit', { method: 'POST', headers: {'Content-Type': 'application/json', 'Accept': 'application/json'}, body: json })
                    .then(async (response) => {
                        let jsonResponse = await response.json();
                        result.innerHTML = jsonResponse.message;
                        if (response.status == 200) result.classList.add('text-green-600');
                        else result.classList.add('text-red-600');
                    })
                    .catch(error => { result.innerHTML = "Algo salió mal. Inténtalo de nuevo."; result.classList.add('text-red-600'); })
                    .then(() => {
                        form.reset();
                        setTimeout(() => { result.innerHTML = ''; result.classList.remove('text-green-600', 'text-red-600'); }, 5000);
                    });
            });

            // Efecto Aurora para las tarjetas
            document.querySelectorAll(".info-card").forEach(card => {
                card.addEventListener("mousemove", e => {
                    const rect = card.getBoundingClientRect();
                    const x = e.clientX - rect.left;
                    const y = e.clientY - rect.top;
                    card.style.setProperty("--mouse-x", `${x}px`);
                    card.style.setProperty("--mouse-y", `${y}px`);
                });
            });
        });
    </script>

</body>
</html>

