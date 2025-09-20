<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>RISC-V SoC Tapeout Program | VSD</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        :root {
            --primary: #0a192f;
            --secondary: #112240;
            --accent: #64ffda;
            --text-primary: #e6f1ff;
            --text-secondary: #8892b0;
        }
        
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        }
        
        body {
            background: var(--primary);
            color: var(--text-primary);
            line-height: 1.6;
            overflow-x: hidden;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 2rem;
        }
        
        header {
            text-align: center;
            margin-bottom: 3rem;
            padding: 2rem 0;
            background: var(--secondary);
            border-radius: 16px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }
        
        h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
            background: linear-gradient(45deg, var(--accent), #3a86ff);
            -webkit-background-clip: text;
            -webkit-text-fill-color: transparent;
        }
        
        .tagline {
            font-size: 1.2rem;
            color: var(--text-secondary);
            max-width: 800px;
            margin: 0 auto 2rem;
        }
        
        .badges {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 1rem;
            margin-bottom: 2rem;
        }
        
        .badge {
            background: rgba(100, 255, 218, 0.1);
            border: 1px solid var(--accent);
            border-radius: 50px;
            padding: 0.5rem 1.5rem;
            font-weight: 600;
            color: var(--accent);
        }
        
        .progress-container {
            background: var(--secondary);
            border-radius: 16px;
            padding: 2rem;
            margin-bottom: 3rem;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }
        
        .progress-title {
            text-align: center;
            margin-bottom: 1.5rem;
            color: var(--accent);
            font-size: 1.5rem;
        }
        
        .progress-steps {
            display: flex;
            justify-content: space-between;
            position: relative;
            margin: 2rem 0;
        }
        
        .progress-steps::before {
            content: "";
            position: absolute;
            top: 50%;
            left: 0;
            transform: translateY(-50%);
            width: 100%;
            height: 4px;
            background: rgba(100, 255, 218, 0.2);
            z-index: 1;
        }
        
        .progress-bar {
            position: absolute;
            top: 50%;
            left: 0;
            transform: translateY(-50%);
            width: 75%;
            height: 4px;
            background: var(--accent);
            z-index: 2;
            transition: width 1s ease;
        }
        
        .step {
            width: 40px;
            height: 40px;
            border-radius: 50%;
            background: var(--secondary);
            border: 4px solid rgba(100, 255, 218, 0.2);
            display: flex;
            align-items: center;
            justify-content: center;
            font-weight: bold;
            position: relative;
            z-index: 3;
            transition: all 0.3s ease;
        }
        
        .step.active {
            background: var(--accent);
            border-color: var(--accent);
            color: var(--primary);
        }
        
        .step-label {
            position: absolute;
            top: 100%;
            left: 50%;
            transform: translateX(-50%);
            margin-top: 0.5rem;
            white-space: nowrap;
            font-size: 0.9rem;
            color: var(--text-secondary);
        }
        
        .step.active .step-label {
            color: var(--accent);
            font-weight: 600;
        }
        
        .program-info {
            background: var(--secondary);
            border-radius: 16px;
            padding: 2rem;
            margin-bottom: 3rem;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }
        
        .program-info h2 {
            color: var(--accent);
            margin-bottom: 1.5rem;
            text-align: center;
            font-size: 1.8rem;
        }
        
        .info-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
            gap: 1.5rem;
        }
        
        .info-card {
            background: rgba(10, 25, 47, 0.6);
            border-radius: 12px;
            padding: 1.5rem;
            border-left: 4px solid var(--accent);
        }
        
        .info-card h3 {
            color: var(--accent);
            margin-bottom: 1rem;
            display: flex;
            align-items: center;
            gap: 0.5rem;
        }
        
        .weeks-container {
            background: var(--secondary);
            border-radius: 16px;
            padding: 2rem;
            margin-bottom: 3rem;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }
        
        .weeks-title {
            color: var(--accent);
            margin-bottom: 1.5rem;
            text-align: center;
            font-size: 1.8rem;
        }
        
        .week {
            background: rgba(10, 25, 47, 0.6);
            border-radius: 12px;
            padding: 1.5rem;
            margin-bottom: 1rem;
            border-left: 4px solid var(--accent);
            transition: transform 0.3s ease;
        }
        
        .week:hover {
            transform: translateY(-5px);
        }
        
        .week h3 {
            display: flex;
            align-items: center;
            gap: 0.5rem;
            margin-bottom: 0.5rem;
        }
        
        .week-number {
            display: inline-block;
            width: 30px;
            height: 30px;
            background: var(--accent);
            color: var(--primary);
            border-radius: 50%;
            text-align: center;
            line-height: 30px;
            font-weight: bold;
            margin-right: 0.5rem;
        }
        
        .stats {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            justify-content: center;
            margin: 3rem 0;
        }
        
        .stat-card {
            background: var(--secondary);
            border-radius: 12px;
            padding: 1.5rem;
            text-align: center;
            flex: 1;
            min-width: 200px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }
        
        .stat-number {
            font-size: 2.5rem;
            font-weight: bold;
            color: var(--accent);
            margin-bottom: 0.5rem;
        }
        
        .stat-label {
            color: var(--text-secondary);
        }
        
        .acknowledgment {
            background: var(--secondary);
            border-radius: 16px;
            padding: 2rem;
            margin-bottom: 3rem;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
        }
        
        .acknowledgment h2 {
            color: var(--accent);
            margin-bottom: 1.5rem;
            text-align: center;
            font-size: 1.8rem;
        }
        
        .acknowledgment-content {
            background: rgba(10, 25, 47, 0.6);
            border-radius: 12px;
            padding: 1.5rem;
            border-left: 4px solid var(--accent);
        }
        
        .tracker {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
            gap: 1rem;
            margin: 1.5rem 0;
        }
        
        .tracker-item {
            background: rgba(100, 255, 218, 0.1);
            border-radius: 8px;
            padding: 1rem;
            text-align: center;
            border: 1px solid var(--accent);
        }
        
        .tracker-item.completed {
            background: rgba(100, 255, 218, 0.2);
        }
        
        .tracker-item i {
            display: block;
            font-size: 1.5rem;
            margin-bottom: 0.5rem;
            color: var(--accent);
        }
        
        .program-links {
            display: flex;
            flex-wrap: wrap;
            gap: 1rem;
            justify-content: center;
            margin: 2rem 0;
        }
        
        .program-link {
            background: rgba(100, 255, 218, 0.1);
            border: 1px solid var(--accent);
            border-radius: 50px;
            padding: 0.5rem 1.5rem;
            color: var(--accent);
            text-decoration: none;
            transition: all 0.3s ease;
        }
        
        .program-link:hover {
            background: var(--accent);
            color: var(--primary);
        }
        
        .participant {
            text-align: center;
            margin-top: 2rem;
            padding: 1rem;
            background: rgba(100, 255, 218, 0.1);
            border-radius: 50px;
            border: 1px solid var(--accent);
        }
        
        footer {
            text-align: center;
            padding: 2rem 0;
            color: var(--text-secondary);
            font-size: 0.9rem;
        }
        
        @media (max-width: 768px) {
            h1 {
                font-size: 2.2rem;
            }
            
            .progress-steps {
                flex-direction: column;
                align-items: flex-start;
                gap: 2rem;
            }
            
            .progress-steps::before {
                width: 4px;
                height: 100%;
                top: 0;
                left: 18px;
                transform: none;
            }
            
            .progress-bar {
                width: 4px;
                height: 75%;
                top: 0;
                left: 18px;
                transform: none;
            }
            
            .step {
                margin-left: 0;
            }
            
            .step-label {
                top: 50%;
                left: calc(100% + 1rem);
                transform: translateY(-50%);
                margin-top: 0;
            }
            
            .tracker {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <header>
            <h1>RISC-V SoC Tapeout Program</h1>
            <p class="tagline">Welcome to my journey through the SoC Tapeout Program VSD!</p>
            
            <div class="badges">
                <div class="badge">RISC-V</div>
                <div class="badge">SOC TAPEOUT</div>
                <div class="badge">VSD</div>
                <div class="badge">PROGRAM</div>
                <div class="badge">PARTICIPANTS</div>
                <div class="badge">3500+</div>
                <div class="badge">MADE IN INDIA</div>
            </div>
            
            <p>This repository documents my <strong>week-by-week progress</strong> with tasks inside each week.</p>
        </header>
        
        <div class="progress-container">
            <h2 class="progress-title">Design Progress</h2>
            <div class="progress-steps">
                <div class="progress-bar"></div>
                <div class="step active">
                    <i class="fas fa-code"></i>
                    <span class="step-label">RTL Design</span>
                </div>
                <div class="step active">
                    <i class="fas fa-cogs"></i>
                    <span class="step-label">Synthesis</span>
                </div>
                <div class="step">
                    <i class="fas fa-microchip"></i>
                    <span class="step-label">Physical Design</span>
                </div>
                <div class="step">
                    <i class="fas fa-rocket"></i>
                    <span class="step-label">Tapeout Ready</span>
                </div>
            </div>
        </div>
        
        <div class="stats">
            <div class="stat-card">
                <div class="stat-number">3500+</div>
                <div class="stat-label">Participants</div>
            </div>
            <div class="stat-card">
                <div class="stat-number">12</div>
                <div class="stat-label">Weeks</div>
            </div>
            <div class="stat-card">
                <div class="stat-number">100%</div>
                <div class="stat-label">Open Source</div>
            </div>
        </div>
        
        <div class="program-info">
            <h2>Program Objectives & Scope</h2>
            <div class="info-grid">
                <div class="info-card">
                    <h3><i class="fas fa-graduation-cap"></i> Learning Path</h3>
                    <p>Complete SoC Design: RTL → Synthesis → Physical Design → Tapeout</p>
                </div>
                <div class="info-card">
                    <h3><i class="fas fa-tools"></i> Tools Focus</h3>
                    <p>Open-Source EDA Ecosystem (Yosys, OpenLane, Magic, etc.)</p>
                </div>
                <div class="info-card">
                    <h3><i class="fas fa-industry"></i> Industry Relevance</h3>
                    <p>Real-world semiconductor design methodologies</p>
                </div>
                <div class="info-card">
                    <h3><i class="fas fa-users"></i> Collaboration</h3>
                    <p>Part of India's largest RISC-V tapeout initiative</p>
                </div>
                <div class="info-card">
                    <h3><i class="fas fa-expand-arrows-alt"></i> Scale</h3>
                    <p>3500+ participants contributing to silicon advancement</p>
                </div>
                <div class="info-card">
                    <h3><i class="fas fa-globe-asia"></i> National Impact</h3>
                    <p>Advancing India's semiconductor ecosystem</p>
                </div>
            </div>
        </div>
        
        <div class="acknowledgment">
            <h2>Acknowledgment</h2>
            <div class="acknowledgment-content">
                <h3>Program Leadership & Support</h3>
                <p>I am thankful to <strong>Kunal Ghosh</strong> and Team <strong>VLSI System Design (VSD)</strong> for the opportunity to participate in the ongoing <strong>RISC-V SoC Tapeout Program</strong>.</p>
                
                <h3 style="margin-top: 1.5rem;">Weekly Progress Tracker</h3>
                <div class="tracker">
                    <div class="tracker-item">
                        <i class="fas fa-tasks"></i>
                        <div>Weekly Progress Tracker</div>
                    </div>
                    <div class="tracker-item completed">
                        <i class="fas fa-check-circle"></i>
                        <div>Week 0</div>
                    </div>
                    <div class="tracker-item completed">
                        <i class="fas fa-check-circle"></i>
                        <div>Tools Setup</div>
                    </div>
                    <div class="tracker-item">
                        <i class="fas fa-clock"></i>
                        <div>Week 1 - Coming Soon</div>
                    </div>
                    <div class="tracker-item">
                        <i class="fas fa-clock"></i>
                        <div>Week 2 - Upcoming</div>
                    </div>
                    <div class="tracker-item">
                        <i class="fas fa-road"></i>
                        <div>Journey Continues...</div>
                    </div>
                </div>
                
                <p>Stay tuned for upcoming weeks covering RTL design, synthesis, physical design, and final tapeout preparation!</p>
                
                <div class="program-links">
                    <a href="#" class="program-link">VSD</a>
                    <a href="#" class="program-link">Official Website</a>
                    <a href="#" class="program-link">RISC-V International</a>
                    <a href="#" class="program-link">EASIESS Platform</a>
                </div>
                
                <div class="participant">
                    <strong>Participant:</strong> Senthil_Kumar_Mahalingam
                </div>
            </div>
        </div>
        
        <footer>
            <p>"In this program, we learn to design a System-on-Chip (SoC) from basic RTL to GDSII using open-source tools. Part of India's largest collaborative RISC-V tapeout initiative, empowering 3500+ participants to build silicon and advance the nation's semiconductor ecosystem."</p>
            <p>© 2023 RISC-V SoC Tapeout Program | VSD</p>
        </footer>
    </div>

    <script>
        // Simple animation for progress bar
        document.addEventListener('DOMContentLoaded', function() {
            const progressBar = document.querySelector('.progress-bar');
            setTimeout(() => {
                progressBar.style.width = '75%';
            }, 500);
            
            // Animate stat numbers
            const statNumbers = document.querySelectorAll('.stat-number');
            statNumbers.forEach(stat => {
                const target = parseInt(stat.textContent);
                let current = 0;
                const duration = 2000;
                const steps = 50;
                const increment = target / steps;
                const stepTime = duration / steps;
                
                const timer = setInterval(() => {
                    current += increment;
                    if (current >= target) {
                        stat.textContent = target + (stat.textContent.includes('+') ? '+' : '');
                        clearInterval(timer);
                    } else {
                        stat.textContent = Math.round(current) + (stat.textContent.includes('+') ? '+' : '');
                    }
                }, stepTime);
            });
        });
    </script>
</body>
</html>
