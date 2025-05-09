<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Diyora's Assignment Portal</title>
  <link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;500;600;700&display=swap" rel="stylesheet" />
  <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600&display=swap" rel="stylesheet" />
  <style>
    * {
      margin: 0;
      padding: 0;
      box-sizing: border-box;
    }
    
    :root {
      --primary: #a770ff;
      --primary-hover: #cf8fff;
      --bg-dark: #0f0f1e;
      --text-light: rgba(255, 255, 255, 0.8);
      --text-mid: rgba(255, 255, 255, 0.6);
      --card-bg: rgba(15, 15, 30, 0.5);
    }
    
    body {
      font-family: 'Montserrat', sans-serif;
      background: var(--bg-dark);
      background-image: 
          radial-gradient(circle at 20% 30%, rgba(76, 0, 255, 0.15) 0%, transparent 50%),
          radial-gradient(circle at 80% 70%, rgba(255, 0, 128, 0.15) 0%, transparent 50%);
      color: white;
      text-align: center;
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      overflow-x: hidden;
      position: relative;
    }

    /* Animated background */
    .animated-bg {
      position: fixed;
      top: 0;
      left: 0;
      width: 100vw;
      height: 100vh;
      z-index: -2;
      overflow: hidden;
    }

    .animated-bg .bubble {
      position: absolute;
      border-radius: 50%;
      opacity: 0.1;
      filter: blur(20px);
      animation: float 15s infinite linear;
    }
    
    @keyframes float {
      0% { transform: translateY(0) rotate(0deg); }
      25% { transform: translateY(-50px) rotate(90deg); }
      50% { transform: translateY(0) rotate(180deg); }
      75% { transform: translateY(50px) rotate(270deg); }
      100% { transform: translateY(0) rotate(360deg); }
    }
    
    /* Login Portal Styles */
    #login-section {
      margin: 50px auto;
      background-color: rgba(255, 255, 255, 0.05);
      padding: 30px;
      border-radius: 10px;
      box-shadow: 0 4px 20px rgba(0, 0, 0, 0.4);
      max-width: 400px;
      backdrop-filter: blur(10px);
      border: 1px solid rgba(255, 255, 255, 0.05);
      position: relative;
      z-index: 10;
      transition: all 0.5s ease;
    }
    
    #login-form {
      display: flex;
      flex-direction: column;
      gap: 15px;
    }
    
    .form-header {
      font-family: 'Syne', sans-serif;
      font-size: 28px;
      letter-spacing: 2px;
      font-weight: 600;
      margin-bottom: 20px;
      background: linear-gradient(90deg, #f0f0f0, var(--primary));
      background-clip: text;
      -webkit-background-clip: text;
      color: transparent;
      position: relative;
    }
    
    .form-header:after {
      content: "";
      position: absolute;
      bottom: -5px;
      left: 25%;
      width: 50%;
      height: 2px;
      background: linear-gradient(90deg, transparent, var(--primary), transparent);
    }
    
    input {
      padding: 12px;
      border-radius: 8px;
      border: 1px solid rgba(255, 255, 255, 0.1);
      font-size: 16px;
      background-color: rgba(255, 255, 255, 0.05);
      color: white;
      transition: all 0.3s ease;
      font-family: 'Montserrat', sans-serif;
    }
    
    input:focus {
      outline: none;
      border-color: var(--primary);
      box-shadow: 0 0 10px rgba(167, 112, 255, 0.3);
    }
    
    input::placeholder {
      color: rgba(255, 255, 255, 0.5);
    }
    
    button {
      padding: 12px;
      background-color: var(--primary);
      border: none;
      border-radius: 8px;
      color: white;
      font-size: 16px;
      cursor: pointer;
      transition: all 0.3s ease;
      font-weight: 600;
      letter-spacing: 1px;
      text-transform: uppercase;
      font-family: 'Syne', sans-serif;
    }
    
    button:hover {
      background-color: var(--primary-hover);
      transform: translateY(-2px);
      box-shadow: 0 5px 15px rgba(167, 112, 255, 0.4);
    }
    
    #login-status {
      margin-top: 15px;
      color: #f77;
      min-height: 20px;
    }
    
    /* Main Portal Content Styles (Hidden Initially) */
    #main-content {
      display: none;
      opacity: 0;
      transition: opacity 1s ease;
    }
    
    .navbar {
      display: flex;
      justify-content: center;
      align-items: center;
      padding: 25px;
      background: rgba(255, 255, 255, 0.03);
      backdrop-filter: blur(12px);
      box-shadow: 0 8px 32px rgba(0, 0, 0, 0.1);
      position: relative;
      z-index: 10;
      border-bottom: 1px solid rgba(255, 255, 255, 0.05);
    }
    
    .navbar h1 {
      font-family: 'Syne', sans-serif;
      font-size: 28px;
      letter-spacing: 2px;
      font-weight: 600;
      text-transform: uppercase;
      background: linear-gradient(90deg, #f0f0f0, var(--primary));
      background-clip: text;
      -webkit-background-clip: text;
      color: transparent;
      position: relative;
    }

    .navbar h1:after {
      content: "";
      position: absolute;
      bottom: -5px;
      left: 25%;
      width: 50%;
      height: 2px;
      background: linear-gradient(90deg, transparent, var(--primary), transparent);
    }
    
    .container {
      max-width: 1100px;
      margin: 60px auto;
      display: flex;
      flex-direction: column;
      gap: 40px;
      padding: 0 30px;
      flex-grow: 1;
      position: relative;
    }
    
    .card {
      background: var(--card-bg);
      border-radius: 20px;
      overflow: hidden;
      box-shadow: 0 15px 35px rgba(0, 0, 0, 0.25);
      transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
      border: 1px solid rgba(255, 255, 255, 0.05);
      backdrop-filter: blur(10px);
      position: relative;
    }
    
    .card::before {
      content: '';
      position: absolute;
      top: -2px;
      left: -2px;
      right: -2px;
      bottom: -2px;
      background: linear-gradient(45deg, #ff00cc, #3333ff, #00ffff, #ff00cc);
      z-index: -1;
      border-radius: 21px;
      background-size: 400%;
      opacity: 0;
      transition: opacity 0.4s ease;
    }
    
    .card:hover {
      transform: translateY(-10px);
    }
    
    .card:hover::before {
      opacity: 0.5;
      animation: glowingBorder 8s linear infinite;
    }
    
    @keyframes glowingBorder {
      0% { background-position: 0 0; }
      50% { background-position: 400% 0; }
      100% { background-position: 0 0; }
    }
    
    .card-header {
      background: rgba(0, 0, 0, 0.2);
      color: white;
      padding: 25px 30px;
      font-size: 22px;
      font-weight: 700;
      letter-spacing: 1px;
      position: relative;
      overflow: hidden;
      display: flex;
      align-items: center;
      justify-content: center;
      font-family: 'Syne', sans-serif;
    }
    
    .card-header::after {
      content: '';
      position: absolute;
      bottom: 0;
      left: 0;
      right: 0;
      height: 1px;
      background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.3), transparent);
    }
    
    .card-body {
      padding: 35px;
      color: var(--text-light);
    }
    
    /* Assignment Section Styles */
    .assignment-list {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 30px;
      margin-top: 25px;
    }
    
    .assignment-item {
      background: rgba(255, 255, 255, 0.03);
      border-radius: 16px;
      padding: 15px;
      transition: all 0.5s cubic-bezier(0.19, 1, 0.22, 1);
      position: relative;
      overflow: hidden;
      display: flex;
      justify-content: center;
      align-items: center;
      height: 120px;
      border: 1px solid rgba(255, 255, 255, 0.02);
      box-shadow: 0 7px 20px rgba(0, 0, 0, 0.1);
    }
    
    .assignment-item::before {
      content: '';
      position: absolute;
      top: 0;
      left: 0;
      width: 4px;
      height: 0;
      background: linear-gradient(to bottom, #ff00cc, #3333ff);
      transition: height 0.5s ease;
    }
    
    .assignment-item:hover {
      background: rgba(255, 255, 255, 0.05);
      transform: translateY(-5px) scale(1.02);
      box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2);
    }
    
    .assignment-item:hover::before {
      height: 100%;
    }
    
    .assignment-link {
      color: var(--primary);
      text-decoration: none;
      font-size: 18px;
      font-weight: 600;
      position: relative;
      transition: all 0.3s ease;
      padding-bottom: 3px;
      letter-spacing: 0.5px;
      background: linear-gradient(90deg, #fff, var(--primary));
      background-clip: text;
      -webkit-background-clip: text;
      color: transparent;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      height: 100%;
      font-family: 'Syne', sans-serif;
    }
    
    .assignment-link .assignment-date {
      font-size: 12px;
      margin-top: 8px;
      opacity: 0.7;
      font-weight: normal;
    }
    
    .assignment-link::after {
      content: '';
      position: absolute;
      width: 0;
      height: 2px;
      bottom: 0;
      left: 50%;
      transform: translateX(-50%);
      background: linear-gradient(90deg, var(--primary), var(--primary-hover));
      transition: width 0.3s ease;
    }
    
    .assignment-link:hover {
      text-shadow: 0 0 8px rgba(167, 112, 255, 0.5);
    }
    
    .assignment-link:hover::after,
    .assignment-link.uploaded::after {
      width: 80%;
    }
    
    .assignment-item.active {
      border-color: rgba(167, 112, 255, 0.5);
      background: rgba(167, 112, 255, 0.1);
    }
    
    .assignment-item.active::before {
      height: 100%;
    }
    
    /* Profile Section */
    .profile-section {
      padding: 20px;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 20px;
    }
    
    .profile-info {
      text-align: center;
    }
    
    .profile-info h2 {
      color: white;
      font-size: 24px;
      margin-bottom: 10px;
      font-family: 'Syne', sans-serif;
    }
    
    .profile-info p {
      color: var(--text-mid);
      font-size: 16px;
      max-width: 600px;
      margin: 0 auto;
      line-height: 1.6;
    }
    
    .profile-stats {
      display: flex;
      justify-content: center;
      gap: 30px;
      margin-top: 20px;
    }
    
    .stat {
      display: flex;
      flex-direction: column;
      align-items: center;
    }
    
    .stat-value {
      font-size: 24px;
      font-weight: bold;
      color: var(--primary);
      font-family: 'Syne', sans-serif;
    }
    
    .stat-label {
      font-size: 14px;
      color: var(--text-mid);
    }
    
    /* Progress bar */
    .progress-container {
      width: 100%;
      max-width: 600px;
      margin: 20px auto;
    }
    
    .progress-label {
      display: flex;
      justify-content: space-between;
      margin-bottom: 8px;
    }
    
    .progress-track {
      width: 100%;
      height: 8px;
      background: rgba(255, 255, 255, 0.1);
      border-radius: 10px;
      overflow: hidden;
    }
    
    .progress-bar {
      height: 100%;
      background: linear-gradient(90deg, var(--primary), var(--primary-hover));
      border-radius: 10px;
      width: 0;
      transition: width 1.5s ease;
    }
    
    footer {
      background: rgba(0, 0, 0, 0.3);
      padding: 25px;
      text-align: center;
      margin-top: auto;
      font-size: 14px;
      letter-spacing: 1px;
      color: var(--text-mid);
      backdrop-filter: blur(10px);
      border-top: 1px solid rgba(255, 255, 255, 0.03);
      display: flex;
      flex-direction: column;
      gap: 10px;
    }
    
    .social-links {
      display: flex;
      justify-content: center;
      gap: 20px;
      margin-top: 10px;
    }
    
    .social-links a {
      color: var(--text-mid);
      font-size: 20px;
      transition: all 0.3s ease;
    }
    
    .social-links a:hover {
      color: var(--primary);
      transform: translateY(-3px);
    }
    
    /* Fixed Grade Summary Box */
    #grade-summary-box {
      position: fixed;
      top: 20px;
      right: 20px;
      background: rgba(0, 0, 0, 0.7);
      padding: 15px;
      border: 2px solid var(--primary);
      border-radius: 8px;
      box-shadow: 0 0 15px rgba(167, 112, 255, 0.5);
      cursor: pointer;
      z-index: 1000;
      color: white;
      font-family: 'Syne', sans-serif;
      transition: all 0.3s ease;
      min-width: 150px;
      text-align: center;
      backdrop-filter: blur(10px);
      opacity: 0;
      visibility: hidden;
      transition: opacity 0.5s ease, visibility 0.5s;
    }
    
    #grade-summary-box:hover {
      transform: translateY(-3px);
      box-shadow: 0 0 20px rgba(167, 112, 255, 0.8);
      background: rgba(15, 15, 30, 0.9);
    }
    
    #grade-summary-box .grade-percentage {
      font-size: 20px;
      font-weight: bold;
      color: var(--primary);
      margin-top: 5px;
    }
    
    /* Custom scrollbar */
    ::-webkit-scrollbar {
      width: 8px;
    }
    
    ::-webkit-scrollbar-track {
      background: rgba(255, 255, 255, 0.05);
    }
    
    ::-webkit-scrollbar-thumb {
      background: var(--primary);
      border-radius: 10px;
    }
    
    ::-webkit-scrollbar-thumb:hover {
      background: var(--primary-hover);
    }
    
    /* Welcome Animation */
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }
    
    .fade-in {
      animation: fadeIn 1s forwards;
    }
    
    /* Logout button */
    .logout-btn {
      position: fixed;
      top: 20px;
      left: 20px;
      background: rgba(0, 0, 0, 0.7);
      padding: 10px 15px;
      border: 1px solid rgba(255, 255, 255, 0.1);
      border-radius: 8px;
      color: white;
      font-family: 'Syne', sans-serif;
      font-size: 14px;
      cursor: pointer;
      z-index: 1000;
      transition: all 0.3s ease;
      backdrop-filter: blur(10px);
    }
    
    .logout-btn:hover {
      background: rgba(167, 112, 255, 0.2);
      border-color: var(--primary);
    }
    
    /* Responsive styles */
    @media (max-width: 768px) {
      #login-section {
        margin: 30px 20px;
        padding: 20px;
      }
      
      .profile-stats {
        flex-direction: column;
        gap: 15px;
      }
      
      .stat {
        flex-direction: row;
        gap: 10px;
        width: 100%;
        justify-content: center;
      }
      
      .card-body {
        padding: 20px;
      }
    }
  </style>
</head>
<body>
  <div class="animated-bg">
    <!-- Background bubbles will be added by JavaScript -->
  </div>
  
  <!-- Login Section (shown first) -->
  <div id="login-section">
    <h2 class="form-header">Login to Assignment Portal</h2>
    <form id="login-form">
      <input type="email" id="email" placeholder="Email" required />
      <input type="password" id="password" placeholder="Password" required />
      <button type="submit">Login</button>
    </form>
    <div id="login-status"></div>
  </div>

  <!-- Main Content (hidden initially) -->
  <div id="main-content">
    <!-- Fixed Grade Summary Box -->
    <div id="grade-summary-box">
      <strong>Grade Summary</strong>
      <div class="grade-percentage">Loading...</div>
    </div>

    <!-- Logout Button -->
    <button class="logout-btn" id="logout-btn">Logout</button>
    
    <div class="navbar">
      <h1>Diyora's Assignment Portal</h1>
    </div>
    
    <div class="container">
      <!-- Profile Section -->
      <div class="card">
        <div class="card-header">Student Profile</div>
        <div class="card-body">
          <div class="profile-section">
            <div class="profile-info">
              <h2>Diyora - Student No: 2417494</h2>
              <p>IBM student at Dong-A University. Passionate about web development and creative coding.</p>
              
              <div class="profile-stats">
                <div class="stat">
                  <div class="stat-value">12</div>
                  <div class="stat-label">Assignments</div>
                </div>
                <div class="stat">
                  <div class="stat-value">4</div>
                  <div class="stat-label">Completed</div>
                </div>
                <div class="stat">
                  <div class="stat-value">8</div>
                  <div class="stat-label">Upcoming</div>
                </div>
              </div>

              <div class="progress-container">
                <div class="progress-label">
                  <span>Course Progress</span>
                  <span>25%</span>
                </div>
                <div class="progress-track">
                  <div class="progress-bar"></div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      
      <!-- Assignment Collection Section -->
      <div class="card">
        <div class="card-header">Assignment Collection</div>
        <div class="card-body">
          <p>Track your assignment progress throughout the semester</p>
          
          <div class="assignment-list">
            <div class="assignment-item active">
              <a href="https://docs.google.com/document/d/1z1v-lLQ0GKyZsSDASf-bf2dJ2qaiNxGvPdjN58VEEm0/edit?usp=drive_link" class="assignment-link uploaded">
                Assignment 1 (Week 2)
                <span class="assignment-date">Due: Feb 15, 2025</span>
              </a>
            </div>
            
            <div class="assignment-item active">
              <a href="https://dioram8.github.io/assignment2/" class="assignment-link uploaded">
                Assignment 2 (Week 3)
                <span class="assignment-date">Due: Mar 1, 2025</span>
              </a>
            </div>
            
            <div class="assignment-item active">
              <a href="https://dioram8.github.io/assignment3/" class="assignment-link uploaded">
                Assignment 3 (Week 4)
                <span class="assignment-date">Due: Mar 15, 2025</span>
              </a>
            </div>
            
            <div class="assignment-item active">
              <a href="https://dioram8.github.io/week7/" class="assignment-link uploaded">
                Assignment 4 (Week 7)
                <span class="assignment-date">Due: Apr 1, 2025</span>
              </a>
            </div>
            
            <div class="assignment-item">
              <a href="https://diiwonee.github.io/Cookies-Cryptography-Tool/" class="assignment-link uploaded">
                Project (Week 6)
                <span class="assignment-date">Due: Apr 15, 2025</span>
              </a>
            </div>

            <div class="assignment-item">
              <a href="https://docs.google.com/document/d/19N2wdE0nuxms3SkNt9UcfTG3mjIN1FXmlT0nssgHWAs/edit?usp=drive_link" class="assignment-link uploaded">
                Assignment 5 (Week 6)
                <span class="assignment-date">Due: May 1, 2025</span>
              </a>
            </div>
            
            <div class="assignment-item">
              <a href="#" class="assignment-link">
                Assignment 6
                <span class="assignment-date">Due: May 1, 2025</span>
              </a>
            </div>
            
            <div class="assignment-item">
              <a href="#" class="assignment-link">
                Assignment 7
                <span class="assignment-date">Due: May 15, 2025</span>
              </a>
            </div>
            
            <div class="assignment-item">
              <a href="#" class="assignment-link">
                Assignment 8
                <span class="assignment-date">Due: Jun 1, 2025</span>
              </a>
            </div>
            
            <div class="assignment-item">
              <a href="#" class="assignment-link">
                Assignment 9
                <span class="assignment-date">Due: Jun 15, 2025</span>
              </a>
            </div>
            
            <div class="assignment-item">
              <a href="#" class="assignment-link">
                Assignment 10
                <span class="assignment-date">Due: Jul 1, 2025</span>
              </a>
            </div>
            
            <div class="assignment-item">
              <a href="#" class="assignment-link">
                Assignment 11
                <span class="assignment-date">Due: Jul 15, 2025</span>
              </a>
            </div>
            
            <div class="assignment-item">
              <a href="#" class="assignment-link">
                Assignment 12
                <span class="assignment-date">Due: Aug 1, 2025</span>
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
    
    <footer>
      <div>
        &copy; 2025 Diyora | Dong-A University
      </div>
      <div class="social-links">
        <a href="https://github.com/DioraM8" title="GitHub">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M9 19c-5 1.5-5-2.5-7-3m14 6v-3.87a3.37 3.37 0 0 0-.94-2.61c3.14-.35 6.44-1.54 6.44-7A5.44 5.44 0 0 0 20 4.77 5.07 5.07 0 0 0 19.91 1S18.73.65 16 2.48a13.38 13.38 0 0 0-7 0C6.27.65 5.09 1 5.09 1A5.07 5.07 0 0 0 5 4.77a5.44 5.44 0 0 0-1.5 3.78c0 5.42 3.3 6.61 6.44 7A3.37 3.37 0 0 0 9 18.13V22"></path>
          </svg>
        </a>
        <a href="mailto:diyoramuslimova7@gmail.com" title="Email">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
            <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path>
            <polyline points="22,6 12,13 2,6"></polyline>
          </svg>
        </a>
      </div>
    </footer>
  </div>
  
  <script>
    document.addEventListener("DOMContentLoaded", function() {
      // Create animated background bubbles
      const animatedBg = document.querySelector('.animated-bg');
      const colors = ['#a770ff', '#ff00cc', '#3333ff', '#00ffff'];
      
      for (let i = 0; i < 20; i++) {
        const bubble = document.createElement('div');
        bubble.classList.add('bubble');
        
        const size = Math.random() * 200 + 50;
        const color = colors[Math.floor(Math.random() * colors.length)];
        
        bubble.style.width = `${size}px`;
        bubble.style.height = `${size}px`;
        bubble.style.left = `${Math.random() * 100}%`;
        bubble.style.top = `${Math.random() * 100}%`;
        bubble.style.backgroundColor = color;
        bubble.style.animationDelay = `${Math.random() * 15}s`;
        bubble.style.animationDuration = `${Math.random() * 10 + 10}s`;
    
    animatedBg.appendChild(bubble);
  }
  
  // Login functionality
  const loginForm = document.getElementById('login-form');
  const loginStatus = document.getElementById('login-status');
  const mainContent = document.getElementById('main-content');
  const loginSection = document.getElementById('login-section');
  const gradeSummaryBox = document.getElementById('grade-summary-box');
  const logoutBtn = document.getElementById('logout-btn');
  
  // Check if user is already logged in
  if (localStorage.getItem('isLoggedIn') === 'true') {
    showMainContent();
  }
  
  loginForm.addEventListener('submit', function(e) {
    e.preventDefault();
    
    const email = document.getElementById('email').value;
    const password = document.getElementById('password').value;
    
    // Simple validation - in a real app, this would connect to a backend
    if (email === 'diyora@example.com' && password === 'password123') {
      localStorage.setItem('isLoggedIn', 'true');
      showMainContent();
    } else {
      loginStatus.textContent = 'Invalid email or password. Please try again.';
    }
  });
  
  logoutBtn.addEventListener('click', function() {
    localStorage.removeItem('isLoggedIn');
    hideMainContent();
  });
  
  function showMainContent() {
    loginSection.style.display = 'none';
    mainContent.style.display = 'block';
    
    // Add small delay for animation
    setTimeout(() => {
      mainContent.style.opacity = '1';
      
      // Animate progress bar
      document.querySelector('.progress-bar').style.width = '25%';
      
      // Show grade summary box with delay
      setTimeout(() => {
        gradeSummaryBox.style.opacity = '1';
        gradeSummaryBox.style.visibility = 'visible';
        gradeSummaryBox.querySelector('.grade-percentage').textContent = '85%';
      }, 1000);
    }, 100);
  }
  
  function hideMainContent() {
    mainContent.style.opacity = '0';
    
    setTimeout(() => {
      mainContent.style.display = 'none';
      loginSection.style.display = 'block';
      document.getElementById('email').value = '';
      document.getElementById('password').value = '';
      loginStatus.textContent = '';
    }, 500);
  }
  
  // Grade summary box click action
  gradeSummaryBox.addEventListener('click', function() {
    alert('Current Grade: 85% (A-)\nAssignments completed: 4/12\nAttendance: 95%');
  });
});
