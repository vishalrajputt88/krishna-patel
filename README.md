
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Krishna Patel - Professional Singer | Bollywood & Sufi</title>
    <style>
        @import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700;800&display=swap');
        
        :root {
            --primary-color: #ff6b35;
            --secondary-color: #f7931e;
            --accent-color: #c5007a;
            --dark-bg: #1a1a1a;
            --darker-bg: #0f0f0f;
            --text-light: #ffffff;
            --text-gray: #a0a0a0;
            --gradient-1: linear-gradient(135deg, #ff6b35 0%, #f7931e 50%, #c5007a 100%);
            --gradient-2: linear-gradient(45deg, #ff6b35, #c5007a);
            --glass-bg: rgba(255, 255, 255, 0.1);
            --glass-border: rgba(255, 255, 255, 0.2);
        }

        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Poppins', sans-serif;
            background: var(--darker-bg);
            color: var(--text-light);
            overflow-x: hidden;
            line-height: 1.6;
        }

        /* Animated Background */
        .animated-bg {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -2;
            background: var(--darker-bg);
        }

        .animated-bg::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: 
                radial-gradient(circle at 20% 50%, rgba(255, 107, 53, 0.3) 0%, transparent 50%),
                radial-gradient(circle at 80% 20%, rgba(247, 147, 30, 0.3) 0%, transparent 50%),
                radial-gradient(circle at 40% 80%, rgba(197, 0, 122, 0.3) 0%, transparent 50%);
            animation: backgroundMove 15s ease-in-out infinite;
        }

        @keyframes backgroundMove {
            0%, 100% { transform: scale(1) rotate(0deg); }
            50% { transform: scale(1.1) rotate(180deg); }
        }

        /* Music Visualizer */
        .music-visualizer {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            z-index: -1;
            opacity: 0.6;
        }

        .bar {
            position: absolute;
            bottom: 0;
            width: 4px;
            background: var(--gradient-1);
            border-radius: 2px 2px 0 0;
            animation: musicBeat 0.8s ease-in-out infinite alternate;
        }

        .bar:nth-child(1) { left: 5%; animation-delay: 0s; }
        .bar:nth-child(2) { left: 10%; animation-delay: 0.1s; }
        .bar:nth-child(3) { left: 15%; animation-delay: 0.2s; }
        .bar:nth-child(4) { left: 20%; animation-delay: 0.3s; }
        .bar:nth-child(5) { right: 20%; animation-delay: 0.4s; }
        .bar:nth-child(6) { right: 15%; animation-delay: 0.5s; }
        .bar:nth-child(7) { right: 10%; animation-delay: 0.6s; }
        .bar:nth-child(8) { right: 5%; animation-delay: 0.7s; }

        @keyframes musicBeat {
            0% { height: 10px; }
            100% { height: 100px; }
        }

        /* Navigation */
        nav {
            position: fixed;
            top: 0;
            left: 0px;
            width: 100%;
            padding: 1rem 2rem;
            background: rgba(15, 15, 15, 0.9);
            backdrop-filter: blur(20px);
            border-bottom: 1px solid var(--glass-border);
            z-index: 1000;
            transition: all 0.3s ease;
        }

        .nav-container {
            display: flex;
            justify-content: space-between;
            align-items: center;
            max-width: 1200px;
            margin: 0 auto;
        }

        .logo {
            font-size: 2rem;
            font-weight: 800;
            background: var(--gradient-1);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .nav-links {
            display: flex;
            list-style: none;
            gap: 2rem;
        }

        .nav-links a {
            color: var(--text-light);
            text-decoration: none;
            font-weight: 500;
            position: relative;
            transition: all 0.3s ease;
        }

        .nav-links a::before {
            content: '';
            position: absolute;
            bottom: -5px;
            left: 0;
            width: 0;
            height: 2px;
            background: var(--gradient-1);
            transition: width 0.3s ease;
        }

        .nav-links a:hover::before {
            width: 100%;
        }

        .nav-links a:hover {
            color: var(--primary-color);
        }

        /* Hero Section */
        .hero {
            height: 100vh;
            display: flex;
            align-items: center;
            justify-content: center;
            text-align: center;
            position: relative;
            padding: 0 2rem;
        }

        .hero-content {
            max-width: 800px;
            animation: fadeInUp 1s ease-out;
        }

        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(50px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }

        .hero-title {
            font-size: clamp(3rem, 8vw, 6rem);
            font-weight: 800;
            margin-bottom: 1rem;
            background: var(--gradient-1);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            line-height: 1.2;
            animation: glow 2s ease-in-out infinite alternate;
        }

        @keyframes glow {
            from { filter: drop-shadow(0 0 10px rgba(255, 107, 53, 0.5)); }
            to { filter: drop-shadow(0 0 20px rgba(255, 107, 53, 0.8)); }
        }

        .hero-subtitle {
            font-size: 1.5rem;
            color: var(--text-gray);
            margin-bottom: 2rem;
            font-weight: 400;
        }

        .hero-description {
            font-size: 1.1rem;
            color: var(--text-gray);
            margin-bottom: 3rem;
            line-height: 1.8;
        }

        .cta-buttons {
            display: flex;
            gap: 1.5rem;
            justify-content: center;
            flex-wrap: wrap;
        }

        .cta-button {
            padding: 1rem 2.5rem;
            border: none;
            border-radius: 50px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            text-decoration: none;
            display: inline-flex;
            align-items: center;
            gap: 0.5rem;
        }

        .cta-primary {
            background: var(--gradient-1);
            color: white;
            box-shadow: 0 10px 30px rgba(255, 107, 53, 0.4);
        }

        .cta-primary:hover {
            transform: translateY(-3px);
            box-shadow: 0 15px 40px rgba(255, 107, 53, 0.6);
        }

        .cta-secondary {
            background: transparent;
            color: var(--text-light);
            border: 2px solid var(--glass-border);
            backdrop-filter: blur(10px);
        }

        .cta-secondary:hover {
            background: var(--glass-bg);
            border-color: var(--primary-color);
            transform: translateY(-3px);
        }

        /* Stats Section */
        .stats {
            padding: 6rem 2rem;
            background: var(--glass-bg);
            backdrop-filter: blur(20px);
            border-top: 1px solid var(--glass-border);
            border-bottom: 1px solid var(--glass-border);
        }

        .stats-container {
            max-width: 1000px;
            margin: 0 auto;
        }

        .stats-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 2rem;
        }

        .stat-card {
            text-align: center;
            padding: 2rem;
            background: rgba(255, 255, 255, 0.05);
            border-radius: 20px;
            border: 1px solid var(--glass-border);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .stat-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255, 107, 53, 0.1), transparent);
            transition: left 0.6s ease;
        }

        .stat-card:hover::before {
            left: 100%;
        }

        .stat-card:hover {
            transform: translateY(-10px);
            border-color: var(--primary-color);
            box-shadow: 0 20px 40px rgba(255, 107, 53, 0.2);
        }

        .stat-number {
            font-size: 3.5rem;
            font-weight: 800;
            background: var(--gradient-1);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
            line-height: 1;
        }

        .stat-label {
            font-size: 1.1rem;
            color: var(--text-gray);
            margin-top: 0.5rem;
        }

        /* About Section */
        .about {
            padding: 8rem 2rem;
            background: var(--dark-bg);
        }

        .about-container {
            max-width: 1200px;
            margin: 0 auto;
            display: grid;
            grid-template-columns: 1fr 1.5fr;
            gap: 4rem;
            align-items: center;
        }

        .about-image {
            position: relative;
        }

        .profile-circle {
            width: 350px;
            height: 350px;
            border-radius: 50%;
            background: var(--gradient-1);
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 8rem;
            position: relative;
            margin: 0 auto;
            animation: float 6s ease-in-out infinite;
        }

        @keyframes float {
            0%, 100% { transform: translateY(0px); }
            50% { transform: translateY(-20px); }
        }

        .profile-circle::before {
            content: '';
            position: absolute;
            top: -20px;
            left: -20px;
            right: -20px;
            bottom: -20px;
            border-radius: 50%;
            background: var(--gradient-1);
            opacity: 0.3;
            animation: pulse 2s ease-in-out infinite;
        }

        @keyframes pulse {
            0% { transform: scale(1); opacity: 0.3; }
            50% { transform: scale(1.1); opacity: 0.1; }
            100% { transform: scale(1); opacity: 0.3; }
        }

        .about-content h2 {
            font-size: 3rem;
            font-weight: 800;
            margin-bottom: 2rem;
            background: var(--gradient-1);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .about-content p {
            font-size: 1.1rem;
            color: var(--text-gray);
            margin-bottom: 1.5rem;
            line-height: 1.8;
        }

        .specialties {
            display: flex;
            gap: 1rem;
            margin-top: 2rem;
            flex-wrap: wrap;
        }

        .specialty-tag {
            padding: 0.5rem 1.5rem;
            background: var(--glass-bg);
            border: 1px solid var(--glass-border);
            border-radius: 25px;
            font-size: 0.9rem;
            color: var(--text-light);
            backdrop-filter: blur(10px);
        }

        /* Services Section */
        .services {
            padding: 8rem 2rem;
            background: var(--darker-bg);
        }

        .services-container {
            max-width: 1200px;
            margin: 0 auto;
        }

        .section-title {
            text-align: center;
            font-size: 3rem;
            font-weight: 800;
            margin-bottom: 4rem;
            background: var(--gradient-1);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
            background-clip: text;
        }

        .services-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
            gap: 2rem;
        }

        .service-card {
            background: var(--glass-bg);
            border: 1px solid var(--glass-border);
            border-radius: 20px;
            padding: 2.5rem;
            backdrop-filter: blur(20px);
            transition: all 0.3s ease;
            position: relative;
            overflow: hidden;
        }

        .service-card::before {
            content: '';
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 4px;
            background: var(--gradient-1);
            transform: scaleX(0);
            transition: transform 0.3s ease;
        }

        .service-card:hover::before {
            transform: scaleX(1);
        }

        .service-card:hover {
            transform: translateY(-10px);
            border-color: var(--primary-color);
            box-shadow: 0 25px 50px rgba(255, 107, 53, 0.2);
        }

        .service-icon {
            font-size: 3rem;
            margin-bottom: 1.5rem;
            display: block;
        }

        .service-card h3 {
            font-size: 1.5rem;
            font-weight: 700;
            margin-bottom: 1rem;
            color: var(--text-light);
        }

        .service-card p {
            color: var(--text-gray);
            line-height: 1.6;
        }

        /* Contact Section */
        .contact {
            padding: 8rem 2rem;
            background: var(--dark-bg);
        }

        .contact-container {
            max-width: 1000px;
            margin: 0 auto;
            text-align: center;
        }

        .contact-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
            gap: 2rem;
            margin-top: 4rem;
        }

        .contact-card {
            background: var(--glass-bg);
            border: 1px solid var(--glass-border);
            border-radius: 20px;
            padding: 2rem;
            backdrop-filter: blur(20px);
            transition: all 0.3s ease;
        }

        .contact-card:hover {
            transform: translateY(-10px);
            border-color: var(--primary-color);
            box-shadow: 0 20px 40px rgba(255, 107, 53, 0.2);
        }

        .contact-icon {
            font-size: 2.5rem;
            margin-bottom: 1rem;
        }

        .contact-card h3 {
            font-size: 1.3rem;
            font-weight: 600;
            margin-bottom: 0.5rem;
            color: var(--text-light);
        }

        .contact-card p {
            color: var(--text-gray);
            font-size: 0.95rem;
        }

        .contact-card a {
            color: var(--primary-color);
            text-decoration: none;
            transition: color 0.3s ease;
        }

        .contact-card a:hover {
            color: var(--secondary-color);
        }

        /* Footer */
        footer {
            background: var(--darker-bg);
            border-top: 1px solid var(--glass-border);
            padding: 2rem;
            text-align: center;
            color: var(--text-gray);
        }

        /* Mobile Responsive */
        @media (max-width: 768px) {
            .nav-links {
                display: none;
            }

            .hero-title {
                font-size: 3rem;
            }

            .hero-subtitle {
                font-size: 1.2rem;
            }

            .cta-buttons {
                flex-direction: column;
                align-items: center;
            }

            .about-container {
                grid-template-columns: 1fr;
                text-align: center;
            }

            .profile-circle {
                width: 250px;
                height: 250px;
                font-size: 5rem;
            }

            .services-grid {
                grid-template-columns: 1fr;
            }

            .stats-grid {
                grid-template-columns: repeat(2, 1fr);
            }
        }

        /* Scroll Animations */
        .fade-in {
            
            transform: translateY(30px);
            transition: all 0.6s ease;
        }

        .fade-in.visible {
            opacity: 1;
            transform: translateY(0);
        }

        @media (max-width: 767px) {
            .nav-links {     display: flex
;
    align-items: center;
    justify-content: center;
    padding-left: 0px; margin: 0px; }
    .logo { display: none;  }

        
        }
    </style>
</head>
<body>
    <div class="animated-bg"></div>
    
    <div class="music-visualizer">
        <div class="bar"></div>
        <div class="bar"></div>
        <div class="bar"></div>
        <div class="bar"></div>
        <div class="bar"></div>
        <div class="bar"></div>
        <div class="bar"></div>
        <div class="bar"></div>
    </div>

    <nav>
        <div class="nav-container">
            <div class="logo">Krishna Patel</div>
            <ul class="nav-links">
                <li><a href="#home">Home</a></li>
                <li><a href="#videos">Videos</a></li>
                <li><a href="#services">Services</a></li>
                <li><a href="#contact">Contact</a></li>
            </ul>
        </div>
    </nav>

    <main>
        <section id="home" class="hero">
            <div class="hero-content">
                <h1 class="hero-title">Krishna Patel</h1>
                <p class="hero-subtitle">🎤 Professional Singer & Performer</p>
                <p class="hero-description">
                    Bringing the magic of Bollywood & Sufi music to your special moments. 
                    With 200+ live performances across India, I create unforgettable musical experiences 
                    that touch hearts and celebrate life.
                </p>
                <div class="cta-buttons">
                    <a href="#contact" class="cta-button cta-primary">
                        🎵 Book Performance
                    </a>
                    <a href="#about" class="cta-button cta-secondary">
                        👤 Know More
                    </a>
                </div>
            </div>
        </section>

        <section class="stats">
            <div class="stats-container">
                <div class="stats-grid fade-in">
                    <div class="stat-card">
                        <div class="stat-number">200+</div>
                        <div class="stat-label">Live Performances</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">6+</div>
                        <div class="stat-label">Years Experience</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">15K+</div>
                        <div class="stat-label">Happy Audience</div>
                    </div>
                    <div class="stat-card">
                        <div class="stat-number">100+</div>
                        <div class="stat-label">Songs Mastered</div>
                    </div>
                </div>
            </div>
        </section>

        <section id="about" class="about">
            <div class="about-container fade-in">
                <div class="about-image">
                    <div class="profile-circle">
                        🎤
                    </div>
                </div>
                <div class="about-content">
                    <h2>About Krishna</h2>
                    <p>
                        Namaste! I'm Krishna Patel, a passionate singer from Indore with a deep love for 
                        Bollywood and Sufi music. My journey began with a fascination for the emotional 
                        depth that music brings to our lives.
                    </p>
                    <p>
                        Over 6+ years, I've had the privilege of performing at 200+ shows across different 
                        venues - from intimate wedding celebrations to grand cultural events. Each performance 
                        is a new opportunity to connect with hearts through the universal language of music.
                    </p>
                    <p>
                        My specialty lies in bringing the soulful essence of Bollywood classics and the 
                        spiritual depth of Sufi compositions to create magical moments that stay with 
                        you forever.
                    </p>
                    <div class="specialties">
                        <span class="specialty-tag">🎵 Bollywood Hits</span>
                        <span class="specialty-tag">🕌 Sufi Music</span>
                        <span class="specialty-tag">🎭 Live Performances</span>
                        <span class="specialty-tag">🎼 Studio Recording</span>
                    </div>
                </div>
            </div>
        </section>

        <section id="services" class="services">
            <div class="services-container">
                <h2 class="section-title">My Services</h2>
                <div class="services-grid fade-in">
                    <div class="service-card">
                        <div class="service-icon">💒</div>
                        <h3>Wedding Celebrations</h3>
                        <p>Make your special day magical with soulful Bollywood and Sufi performances that create unforgettable memories for you and your guests.</p>
                    </div>
                    <div class="service-card">
                        <div class="service-icon">🏢</div>
                        <h3>Corporate Events</h3>
                        <p>Professional entertainment for corporate gatherings, conferences, and company celebrations with carefully curated music selection.</p>
                    </div>
                    <div class="service-card">
                        <div class="service-icon">🎉</div>
                        <h3>Private Parties</h3>
                        <p>Intimate musical experiences for birthdays, anniversaries, and personal celebrations with customized playlists and dedications.</p>
                    </div>
                    <div class="service-card">
                        <div class="service-icon">🎭</div>
                        <h3>Cultural Programs</h3>
                        <p>Traditional and contemporary performances for festivals, community events, and cultural celebrations across Madhya Pradesh.</p>
                    </div>
                    <div class="service-card">
                        <div class="service-icon">🎼</div>
                        <h3>Studio Recording</h3>
                        <p>Professional vocal recording services for songs, albums, jingles, and audio productions with high-quality output.</p>
                    </div>
                    <div class="service-card">
                        <div class="service-icon">🎸</div>
                        <h3>Music Concerts</h3>
                        <p>Live concert performances with full band setup for larger audiences, music festivals, and entertainment venues.</p>
                    </div>
                </div>
            </div>
        </section>

        <section id="contact" class="contact">
            <div class="contact-container">
                <h2 class="section-title">Let's Create Musical Magic</h2>
                <p>Ready to add the perfect soundtrack to your special moment? Let's discuss how we can make your event unforgettable!</p>
                
                <div class="contact-grid fade-in">
                    <div class="contact-card">
                        <div class="contact-icon">📱</div>
                        <h3>Call Me</h3>
                        <p><a href="tel:+916265110659">+91 62651 10659</a></p>
                        <p>Available 9 AM - 9 PM</p>
                    </div>
                    <div class="contact-card">
                        <div class="contact-icon">📧</div>
                        <h3>Email</h3>
                        <p><a href="mailto:krishna.singer@gmail.com">krishna.singer@gmail.com</a></p>
                        <p>Quick response guaranteed</p>
                    </div>
                    <div class="contact-card">
                        <div class="contact-icon">📍</div>
                        <h3>Location</h3>
                        <p>Indore, Madhya Pradesh</p>
                        <p>Available for travel across India</p>
                    </div>
                    <div class="contact-card">
                        <div class="contact-icon">📷</div>
                        <h3>Instagram</h3>
                        <p><a href="https://instagram.com/it's.your.krish" target="_blank">@it's.your.krish</a></p>
                        <p>Latest updates & performances</p>
                    </div>
                </div>
            </div>
        </section>
    </main>

    <footer>
        <p>&copy; 2025 Krishna Patel. All rights reserved. | Professional Singer from Indore | Bollywood & Sufi Specialist</p>
    </footer>

    <script>
        // Smooth scrolling
        document.querySelectorAll('a[href^="#"]').forEach(anchor => {
            anchor.addEventListener('click', function (e) {
                e.preventDefault();
                const target = document.querySelector(this.getAttribute('href'));
                if (target) {
                    target.scrollIntoView({
                        behavior: 'smooth',
                        block: 'start'
                    });
                }
            });
        });

        // Navbar background on scroll
        window.addEventListener('scroll', function() {
            const nav = document.querySelector('nav');
            if (window.scrollY > 100) {
                nav.style.background = 'rgba(15, 15, 15, 0.95)';
            } else {
                nav.style.background = 'rgba(15, 15, 15, 0.9)';
            }
        });

        // Fade in animation on scroll
        const observerOptions = {
            threshold: 0.1,
            rootMargin: '0px 0px -50px 0px'
        };

        const observer = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    entry.target.classList.add('visible');
                }
            });
        }, observerOptions);

        document.querySelectorAll('.fade-in').forEach(el => {
            observer.observe(el);
        });

        // Counter animation
        function animateCounters() {
            const counters = document.querySelectorAll('.stat-number');
            counters.forEach(counter => {
                const target = parseInt(counter.innerText.replace(/\D/g, ''));
                const duration = 2000;
                const step = target / (duration / 16);
                let current = 0;
                
                const timer = setInterval(() => {
                    current += step;
                    if (current >= target) {
                        counter.innerText = target + (counter.innerText.includes('+') ? '+' : '');
                        clearInterval(timer);
                    } else {
                        counter.innerText = Math.floor(current) + (counter.innerText.includes('+') ? '+' : '');
                    }
                }, 16);
            });
        }

        // Trigger counter animation when stats section is visible
        const statsObserver = new IntersectionObserver((entries) => {
            entries.forEach(entry => {
                if (entry.isIntersecting) {
                    animateCounters();
                    statsObserver.unobserve(entry.target);
                }
            });
        });

        statsObserver.observe(document.querySelector('.stats'));

        // Dynamic music visualizer
        const bars = document.querySelectorAll('.bar');
        setInterval(() => {
            bars.forEach(bar => {
                const height = Math.random() * 150 + 20;
                bar.style.height = height + 'px';
            });
        }, 300);

        // Page load animation
        window.addEventListener('load', ()
