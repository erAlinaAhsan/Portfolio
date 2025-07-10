<script setup>
import { ref, reactive, onMounted } from 'vue';
import alinaPhoto from './assets/alina.png';

// Contact form data
const form = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
});

const isSubmitting = ref(false);

// Form submission
const submitForm = async () => {
  isSubmitting.value = true;
  
  try {
    // Using EmailJS or Netlify Forms for email functionality
    const response = await fetch('/', {
      method: 'POST',
      headers: { 'Content-Type': 'application/x-www-form-urlencoded' },
      body: new URLSearchParams({
        'form-name': 'contact',
        name: form.name,
        email: form.email,
        subject: form.subject,
        message: form.message
      }).toString()
    });

    if (response.ok) {
      alert('Message sent successfully! I\'ll get back to you soon.');
      // Reset form
      form.name = '';
      form.email = '';
      form.subject = '';
      form.message = '';
    } else {
      throw new Error('Failed to send message');
    }
  } catch (error) {
    alert('Sorry, there was an error sending your message. Please try emailing me directly.');
  } finally {
    isSubmitting.value = false;
  }
};

// Smooth scrolling
const scrollTo = (elementId) => {
  const element = document.getElementById(elementId);
  if (element) {
    element.scrollIntoView({ behavior: 'smooth' });
  }
};

// Mobile menu toggle
const toggleMobileMenu = () => {
  const navLinks = document.querySelector('.nav-links');
  navLinks.classList.toggle('active');
};

// Scroll animations and navigation
onMounted(() => {
  // Intersection Observer for scroll animations
  const observerOptions = {
    threshold: 0.1,
    rootMargin: '0px 0px -50px 0px'
  };

  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry) => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible');
      }
    });
  }, observerOptions);

  // Observe all sections
  const sections = document.querySelectorAll('.section');
  sections.forEach((section) => {
    observer.observe(section);
  });

  // Update navigation on scroll
  window.addEventListener('scroll', () => {
    const sections = document.querySelectorAll('section');
    const navLinks = document.querySelectorAll('.nav-links a');
    
    let current = '';
    sections.forEach((section) => {
      const sectionTop = section.getBoundingClientRect().top;
      if (sectionTop <= 100) {
        current = section.getAttribute('id');
      }
    });

    navLinks.forEach((link) => {
      link.classList.remove('active');
      if (link.getAttribute('href') === `#${current}`) {
        link.classList.add('active');
      }
    });
  });

  // Add Netlify form detection
  const form = document.querySelector('.contact-form');
  form.setAttribute('netlify', '');
  form.setAttribute('name', 'contact');
});
</script>

<template>
  <div id="app">
    <!-- Navigation -->
    <nav class="navbar">
      <div class="container">
        <div class="nav-brand">
          <span class="logo">Alina</span>
        </div>
        <ul class="nav-links">
          <li><a href="#home" @click="scrollTo('home')">Home</a></li>
          <li><a href="#about" @click="scrollTo('about')">About</a></li>
          <li><a href="#journey" @click="scrollTo('journey')">Journey</a></li>
          <li><a href="#skills" @click="scrollTo('skills')">Skills</a></li>
          <li><a href="#projects" @click="scrollTo('projects')">Projects</a></li>
          <li><a href="#contact" @click="scrollTo('contact')">Contact</a></li>
        </ul>
        <div class="nav-toggle" @click="toggleMobileMenu">
          <span></span>
          <span></span>
          <span></span>
        </div>
      </div>
    </nav>

    <!-- Hero Section -->
    <section id="home" class="hero">
      <div class="container">
        <div class="hero-content">
          <div class="hero-text">
            <h1 class="hero-title">
              Hi, I'm <span class="gradient-text">Alina Ahsan</span>
            </h1>
            <h2 class="hero-subtitle">Full Stack Developer</h2>
            <p class="hero-description">
              I craft digital experiences with Vue.js, Node.js, and modern web technologies. 
              Passionate about creating efficient, scalable solutions that make a difference.
            </p>
            <div class="hero-buttons">
              <a href="#projects" @click="scrollTo('projects')" class="btn btn-primary">
                View My Work
              </a>
              <a href="#contact" @click="scrollTo('contact')" class="btn btn-outline">
                Get In Touch
              </a>
            </div>
            <div class="hero-social">
              <a href="mailto:alina.ahsan13@gmail.com" class="social-link">
                <i class="icon">📧</i>
              </a>
              <a href="tel:+916386821493" class="social-link">
                <i class="icon">📞</i>
              </a>
              <a href="#" class="social-link">
                <i class="icon">💼</i>
              </a>
            </div>
          </div>
          <div class="hero-image">
            <div class="image-container">
              <img :src="alinaPhoto" alt="Alina Ahsan" class="profile-img" />
              <div class="image-decoration"></div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- About Section -->
    <section id="about" class="section about-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">About Me</h2>
          <p class="section-subtitle">Passionate about creating digital solutions</p>
        </div>
        <div class="about-content">
          <div class="about-text">
            <h3>Building the Future, One Line of Code at a Time</h3>
            <p>
              I'm a dedicated Full Stack Developer at Hyperzod Technologies, where I turn complex problems 
              into elegant digital solutions. My journey in tech began with curiosity and has evolved into 
              a passion for creating impactful applications.
            </p>
            <p>
              I specialize in modern web development using Vue.js, Node.js, and cutting-edge technologies. 
              I believe in writing clean, maintainable code and creating user experiences that truly matter.
            </p>
            <p>
              When I'm not coding, you'll find me exploring new technologies, contributing to open source 
              projects, or enjoying a perfect cup of coffee while planning my next big project.
            </p>
            <div class="stats">
              <div class="stat-item">
                <span class="stat-number">2+</span>
                <span class="stat-label">Years Experience</span>
              </div>
              <div class="stat-item">
                <span class="stat-number">10+</span>
                <span class="stat-label">Projects Completed</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Journey Section -->
    <section id="journey" class="section journey-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">My Journey</h2>
          <p class="section-subtitle">Professional growth and achievements</p>
        </div>
        <div class="timeline">
          <div class="timeline-item">
            <div class="timeline-marker">
              <div class="timeline-icon">💼</div>
            </div>
            <div class="timeline-content">
              <h3 class="timeline-title">Software Developer</h3>
              <h4 class="timeline-company">Hyperzod Technologies</h4>
              <span class="timeline-period">Sep 2023 - Present</span>
              <ul class="timeline-achievements">
                <li>Developed responsive web applications using Vue.js</li>
                <li>Implemented cost-effective solutions reducing project expenses by 20%</li>
                <li>Streamlined development workflows improving team efficiency by 25%</li>
                <li>Collaborated with cross-functional teams on multiple client projects</li>
              </ul>
            </div>
          </div>

          <div class="timeline-item">
            <div class="timeline-marker">
              <div class="timeline-icon">🎓</div>
            </div>
            <div class="timeline-content">
              <h3 class="timeline-title">Freelance Developer</h3>
              <h4 class="timeline-company">Independent</h4>
              <span class="timeline-period">2022 - 2023</span>
              <ul class="timeline-achievements">
                <li>Built custom e-commerce platforms for local businesses</li>
                <li>Created responsive websites with modern UI/UX design</li>
                <li>Gained expertise in full-stack development</li>
                <li>Developed strong client communication skills</li>
              </ul>
            </div>
          </div>

          <div class="timeline-item">
            <div class="timeline-marker">
              <div class="timeline-icon">🚀</div>
            </div>
            <div class="timeline-content">
              <h3 class="timeline-title">Started Coding Journey</h3>
              <h4 class="timeline-company">Self-Taught</h4>
              <span class="timeline-period">2021 - 2022</span>
              <ul class="timeline-achievements">
                <li>Mastered HTML, CSS, and JavaScript fundamentals</li>
                <li>Learned Vue.js and modern web development</li>
                <li>Built personal projects and portfolio</li>
                <li>Completed multiple online courses and certifications</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Skills Section -->
    <section id="skills" class="section skills-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Skills & Technologies</h2>
          <p class="section-subtitle">Tools I use to bring ideas to life</p>
        </div>
        <div class="skills-grid">
          <div class="skill-category">
            <div class="skill-icon">🎨</div>
            <h3>Frontend Development</h3>
            <div class="skill-items">
              <span class="skill-tag">Vue.js</span>
              <span class="skill-tag">JavaScript</span>
              <span class="skill-tag">HTML5</span>
              <span class="skill-tag">CSS3</span>
              <span class="skill-tag">SASS</span>
              <span class="skill-tag">Bootstrap</span>
              <span class="skill-tag">Responsive Design</span>
            </div>
          </div>

          <div class="skill-category">
            <div class="skill-icon">⚙️</div>
            <h3>Backend Development</h3>
            <div class="skill-items">
              <span class="skill-tag">Node.js</span>
              <span class="skill-tag">Express.js</span>
              <span class="skill-tag">Python</span>
              <span class="skill-tag">MongoDB</span>
              <span class="skill-tag">MySQL</span>
              <span class="skill-tag">REST APIs</span>
              <span class="skill-tag">Authentication</span>
            </div>
          </div>

          <div class="skill-category">
            <div class="skill-icon">🛠️</div>
            <h3>Tools & Technologies</h3>
            <div class="skill-items">
              <span class="skill-tag">Git</span>
              <span class="skill-tag">Vite</span>
              <span class="skill-tag">Webpack</span>
              <span class="skill-tag">NPM</span>
              <span class="skill-tag">Postman</span>
              <span class="skill-tag">VS Code</span>
              <span class="skill-tag">Linux</span>
            </div>
          </div>

          <div class="skill-category">
            <div class="skill-icon">☁️</div>
            <h3>Deployment & Cloud</h3>
            <div class="skill-items">
              <span class="skill-tag">Netlify</span>
              <span class="skill-tag">Vercel</span>
              <span class="skill-tag">Heroku</span>
              <span class="skill-tag">AWS</span>
              <span class="skill-tag">Docker</span>
              <span class="skill-tag">CI/CD</span>
              <span class="skill-tag">Domain Management</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Projects Section -->
    <section id="projects" class="section projects-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Featured Projects</h2>
          <p class="section-subtitle">Some of my recent work</p>
        </div>
        <div class="projects-grid">
          
          <!-- Project 1: M.A.Electricals -->
          <div class="project-card">
            <div class="project-image">
              <div class="project-demo">
                <div class="demo-browser">
                  <div class="browser-header">
                    <div class="browser-buttons">
                      <span></span>
                      <span></span>
                      <span></span>
                    </div>
                    <div class="browser-url">maelectricals.com</div>
                  </div>
                  <div class="browser-content">
                    <div class="demo-content electrical-demo">
                      <div class="demo-header">⚡ M.A.Electricals</div>
                      <div class="demo-products">
                        <div class="product-card">LED Lights</div>
                        <div class="product-card">Switches</div>
                        <div class="product-card">Cables</div>
                      </div>
                      <div class="demo-cart">🛒 Add to Cart</div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="project-content">
              <h3 class="project-title">M.A.Electricals</h3>
              <p class="project-description">
                Modern e-commerce platform for electrical equipment with advanced inventory management, 
                customer portal, and seamless shopping experience.
              </p>
              <div class="project-tech">
                <span class="tech-tag">Vue.js</span>
                <span class="tech-tag">Node.js</span>
                <span class="tech-tag">MongoDB</span>
                <span class="tech-tag">Express</span>
              </div>
              <div class="project-links">
                <a href="https://maelectricals-demo.netlify.app" class="project-link" target="_blank">
                  <i class="icon">🌐</i> Live Demo
                </a>
                <a href="https://github.com/erAlinaAhsan/ma-electricals" class="project-link" target="_blank">
                  <i class="icon">💻</i> GitHub
                </a>
              </div>
            </div>
          </div>

          <!-- Project 2: Hirfat -->
          <div class="project-card">
            <div class="project-image">
              <div class="project-demo">
                <div class="demo-browser">
                  <div class="browser-header">
                    <div class="browser-buttons">
                      <span></span>
                      <span></span>
                      <span></span>
                    </div>
                    <div class="browser-url">hirfat.com</div>
                  </div>
                  <div class="browser-content">
                    <div class="demo-content hirfat-demo">
                      <div class="demo-header">🎨 Hirfat Chikankari</div>
                      <div class="demo-gallery">
                        <div class="gallery-item">Kurta</div>
                        <div class="gallery-item">Dupatta</div>
                        <div class="gallery-item">Saree</div>
                      </div>
                      <div class="demo-artisan">👗 Handcrafted Beauty</div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="project-content">
              <h3 class="project-title">Hirfat - Chikankari Boutique</h3>
              <p class="project-description">
                Elegant e-commerce platform showcasing traditional Chikankari embroidery with beautiful 
                galleries, artisan stories, and celebration of Indian heritage.
              </p>
              <div class="project-tech">
                <span class="tech-tag">Vue.js</span>
                <span class="tech-tag">Vite</span>
                <span class="tech-tag">CSS3</span>
                <span class="tech-tag">Responsive</span>
              </div>
              <div class="project-links">
                <a href="https://hirfat-demo.netlify.app" class="project-link" target="_blank">
                  <i class="icon">🌐</i> Live Demo
                </a>
                <a href="https://github.com/erAlinaAhsan/hirfat" class="project-link" target="_blank">
                  <i class="icon">💻</i> GitHub
                </a>
              </div>
            </div>
          </div>

          <!-- Project 3: Advanced Todo List -->
          <div class="project-card">
            <div class="project-image">
              <div class="project-demo">
                <div class="demo-browser">
                  <div class="browser-header">
                    <div class="browser-buttons">
                      <span></span>
                      <span></span>
                      <span></span>
                    </div>
                    <div class="browser-url">advanced-todo-alina.netlify.app</div>
                  </div>
                  <div class="browser-content">
                    <div class="demo-content todo-demo">
                      <div class="demo-header">📝 Smart Todo</div>
                      <div class="demo-todo-list">
                        <div class="todo-item completed">✅ Learn Vue.js</div>
                        <div class="todo-item">⏳ Build Portfolio</div>
                        <div class="todo-item">📅 Meeting at 3 PM</div>
                      </div>
                      <div class="demo-stats">📊 Progress: 67%</div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="project-content">
              <h3 class="project-title">Advanced Todo List</h3>
              <p class="project-description">
                Feature-rich task management app with categories, priorities, due dates, progress tracking, 
                and local storage for a complete productivity solution.
              </p>
              <div class="project-tech">
                <span class="tech-tag">Vue.js</span>
                <span class="tech-tag">JavaScript</span>
                <span class="tech-tag">LocalStorage</span>
                <span class="tech-tag">CSS3</span>
              </div>
              <div class="project-links">
                <a href="https://advanced-todo-alina.netlify.app" class="project-link" target="_blank">
                  <i class="icon">🌐</i> Live Demo
                </a>
                <a href="https://github.com/erAlinaAhsan/advanced-todo" class="project-link" target="_blank">
                  <i class="icon">💻</i> GitHub
                </a>
              </div>
            </div>
          </div>

          <!-- Project 4: Company Dashboard -->
          <div class="project-card">
            <div class="project-image">
              <div class="project-demo">
                <div class="demo-browser">
                  <div class="browser-header">
                    <div class="browser-buttons">
                      <span></span>
                      <span></span>
                      <span></span>
                    </div>
                    <div class="browser-url">euphonious-bavarois-b78304.netlify.app</div>
                  </div>
                  <div class="browser-content">
                    <div class="demo-content dashboard-demo">
                      <div class="demo-header">📊 Company Dashboard</div>
                      <div class="demo-metrics">
                        <div class="metric-card">Users: 1,234</div>
                        <div class="metric-card">Sales: $45K</div>
                        <div class="metric-card">Growth: +12%</div>
                      </div>
                      <div class="demo-chart">📈 Analytics Chart</div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="project-content">
              <h3 class="project-title">Company Dashboard</h3>
              <p class="project-description">
                Comprehensive business dashboard with real-time analytics, user management, and performance 
                metrics. Features interactive charts and responsive design for data visualization.
              </p>
              <div class="project-tech">
                <span class="tech-tag">Vue.js</span>
                <span class="tech-tag">JavaScript</span>
                <span class="tech-tag">Charts.js</span>
                <span class="tech-tag">CSS3</span>
              </div>
              <div class="project-links">
                <a href="https://euphonious-bavarois-b78304.netlify.app/" class="project-link" target="_blank">
                  <i class="icon">🌐</i> Live Demo
                </a>
                <a href="https://github.com/erAlinaAhsan/company-dashboard" class="project-link" target="_blank">
                  <i class="icon">💻</i> GitHub
                </a>
              </div>
            </div>
          </div>

          <!-- Project 5: Register/Login Page -->
          <div class="project-card">
            <div class="project-image">
              <div class="project-demo">
                <div class="demo-browser">
                  <div class="browser-header">
                    <div class="browser-buttons">
                      <span></span>
                      <span></span>
                      <span></span>
                    </div>
                    <div class="browser-url">zingy-gumption-9df105.netlify.app</div>
                  </div>
                  <div class="browser-content">
                    <div class="demo-content auth-demo">
                      <div class="demo-header">🔐 User Authentication</div>
                      <div class="demo-form">
                        <div class="form-field">📧 Email</div>
                        <div class="form-field">🔒 Password</div>
                        <div class="auth-button">Login</div>
                      </div>
                      <div class="demo-toggle">Register → Login</div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="project-content">
              <h3 class="project-title">User Authentication System</h3>
              <p class="project-description">
                Modern register and login page with form validation, responsive design, and smooth 
                transitions. Features secure authentication flow and user-friendly interface.
              </p>
              <div class="project-tech">
                <span class="tech-tag">HTML5</span>
                <span class="tech-tag">CSS3</span>
                <span class="tech-tag">JavaScript</span>
                <span class="tech-tag">Form Validation</span>
              </div>
              <div class="project-links">
                <a href="https://zingy-gumption-9df105.netlify.app/" class="project-link" target="_blank">
                  <i class="icon">🌐</i> Live Demo
                </a>
                <a href="https://github.com/erAlinaAhsan/user-auth" class="project-link" target="_blank">
                  <i class="icon">💻</i> GitHub
                </a>
              </div>
            </div>
          </div>

          <!-- Project 6: E-commerce Website -->
          <div class="project-card">
            <div class="project-image">
              <div class="project-demo">
                <div class="demo-browser">
                  <div class="browser-header">
                    <div class="browser-buttons">
                      <span></span>
                      <span></span>
                      <span></span>
                    </div>
                    <div class="browser-url">leafy-sawine-0fe40b.netlify.app</div>
                  </div>
                  <div class="browser-content">
                    <div class="demo-content ecommerce-demo">
                      <div class="demo-header">🛍️ E-commerce Store</div>
                      <div class="demo-products">
                        <div class="product-item">Product 1</div>
                        <div class="product-item">Product 2</div>
                        <div class="product-item">Product 3</div>
                      </div>
                      <div class="demo-actions">Add to Cart 🛒</div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="project-content">
              <h3 class="project-title">E-commerce Website</h3>
              <p class="project-description">
                Full-featured online shopping platform with product catalog, shopping cart, and checkout 
                process. Responsive design with modern UI and smooth user experience.
              </p>
              <div class="project-tech">
                <span class="tech-tag">Vue.js</span>
                <span class="tech-tag">JavaScript</span>
                <span class="tech-tag">CSS3</span>
                <span class="tech-tag">Responsive</span>
              </div>
              <div class="project-links">
                <a href="https://leafy-sawine-0fe40b.netlify.app/" class="project-link" target="_blank">
                  <i class="icon">🌐</i> Live Demo
                </a>
                <a href="https://github.com/erAlinaAhsan/ecommerce-website" class="project-link" target="_blank">
                  <i class="icon">💻</i> GitHub
                </a>
              </div>
            </div>
          </div>

          <!-- Project 7: Portfolio Website -->
          <div class="project-card">
            <div class="project-image">
              <div class="project-demo">
                <div class="demo-browser">
                  <div class="browser-header">
                    <div class="browser-buttons">
                      <span></span>
                      <span></span>
                      <span></span>
                    </div>
                    <div class="browser-url">erportfolio.netlify.app</div>
                  </div>
                  <div class="browser-content">
                    <div class="demo-content portfolio-demo">
                      <div class="demo-header">👩‍💻 Portfolio</div>
                      <div class="demo-sections">
                        <div class="section-tab active">About</div>
                        <div class="section-tab">Projects</div>
                        <div class="section-tab">Contact</div>
                      </div>
                      <div class="demo-showcase">🎨 Modern Design</div>
                    </div>
                  </div>
                </div>
              </div>
            </div>
            <div class="project-content">
              <h3 class="project-title">Portfolio Website</h3>
              <p class="project-description">
                Modern, responsive portfolio website with smooth animations, contact form, and clean design 
                showcasing development skills and projects.
              </p>
              <div class="project-tech">
                <span class="tech-tag">Vue.js</span>
                <span class="tech-tag">CSS3</span>
                <span class="tech-tag">Animations</span>
                <span class="tech-tag">Responsive</span>
              </div>
              <div class="project-links">
                <a href="https://erportfolio.netlify.app/" class="project-link" target="_blank">
                  <i class="icon">🌐</i> Live Demo
                </a>
                <a href="https://github.com/erAlinaAhsan/portfolio" class="project-link" target="_blank">
                  <i class="icon">💻</i> GitHub
                </a>
              </div>
            </div>
          </div>

        </div>
      </div>
    </section>

    <!-- Contact Section -->
    <section id="contact" class="section contact-section">
      <div class="container">
        <div class="section-header">
          <h2 class="section-title">Let's Work Together</h2>
          <p class="section-subtitle">Have a project in mind? Let's discuss!</p>
        </div>
        <div class="contact-content">
          <div class="contact-info">
            <h3>Get In Touch</h3>
            <p>
              I'm always excited to work on new projects and collaborate with amazing people. 
              Whether you need a website, web application, or just want to say hello, I'd love to hear from you!
            </p>
            <div class="contact-methods">
              <div class="contact-method">
                <div class="contact-icon">📧</div>
                <div class="contact-details">
                  <span class="contact-label">Email</span>
                  <span class="contact-value">alina.ahsan13@gmail.com</span>
                </div>
              </div>
              <div class="contact-method">
                <div class="contact-icon">📞</div>
                <div class="contact-details">
                  <span class="contact-label">Phone</span>
                  <span class="contact-value">+91-6386821493</span>
                </div>
              </div>
              <div class="contact-method">
                <div class="contact-icon">📍</div>
                <div class="contact-details">
                  <span class="contact-label">Location</span>
                  <span class="contact-value">Lucknow, India</span>
                </div>
              </div>
            </div>
          </div>
          
          <div class="contact-form-container">
            <form class="contact-form" @submit.prevent="submitForm">
              <div class="form-group">
                <label for="name">Full Name</label>
                <input 
                  type="text" 
                  id="name" 
                  v-model="form.name" 
                  required 
                  placeholder="Your full name"
                />
              </div>
              
              <div class="form-group">
                <label for="email">Email Address</label>
                <input 
                  type="email" 
                  id="email" 
                  v-model="form.email" 
                  required 
                  placeholder="your.email@example.com"
                />
              </div>
              
              <div class="form-group">
                <label for="subject">Subject</label>
                <input 
                  type="text" 
                  id="subject" 
                  v-model="form.subject" 
                  required 
                  placeholder="What's this about?"
                />
              </div>
              
              <div class="form-group">
                <label for="message">Message</label>
                <textarea 
                  id="message" 
                  v-model="form.message" 
                  required 
                  rows="5" 
                  placeholder="Tell me about your project..."
                ></textarea>
              </div>
              
              <button type="submit" class="btn btn-primary" :disabled="isSubmitting">
                <span v-if="!isSubmitting">Send Message</span>
                <span v-else>Sending...</span>
              </button>
            </form>
          </div>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer class="footer">
      <div class="container">
        <div class="footer-content">
          <div class="footer-text">
            <p>© 2025 Alina Ahsan. Crafted with ❤️ and lots of ☕</p>
          </div>
          <div class="footer-links">
            <a href="mailto:alina.ahsan13@gmail.com">Email</a>
            <a href="tel:+916386821493">Phone</a>
            <a href="#home" @click="scrollTo('home')">Back to Top</a>
          </div>
        </div>
      </div>
    </footer>

  </div>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
</style>
