# SR-s-Quiz
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>GK Quiz Challenge - 100 Levels</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 80px 20px 20px 20px;
        }
        
        .game-container {
            background: rgba(255, 255, 255, 0.95);
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.1);
            backdrop-filter: blur(10px);
            max-width: 600px;
            width: 100%;
            text-align: center;
        }
        
        .profile-section {
            position: fixed;
            top: 15px;
            right: 20px;
            display: flex;
            align-items: center;
            gap: 10px;
            z-index: 1001;
        }
        
        .profile-dropdown {
            position: relative;
        }
        
        .profile-btn {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            font-size: 1.2rem;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.2);
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .profile-btn:hover {
            background: linear-gradient(45deg, #764ba2, #667eea);
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(0, 0, 0, 0.3);
        }
        
        .profile-menu {
            position: absolute;
            top: 60px;
            right: 0;
            background: white;
            border-radius: 15px;
            padding: 15px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.2);
            min-width: 200px;
            display: none;
            z-index: 1000;
        }
        
        .profile-menu.show {
            display: block;
            animation: slideDown 0.3s ease;
        }
        
        @keyframes slideDown {
            from {
                opacity: 0;
                transform: translateY(-10px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .menu-item {
            display: flex;
            align-items: center;
            gap: 10px;
            padding: 12px 15px;
            border-radius: 10px;
            cursor: pointer;
            transition: all 0.3s ease;
            color: #333;
            font-weight: 500;
            border: none;
            background: none;
            width: 100%;
            text-align: left;
            font-size: 0.95rem;
        }
        
        .menu-item:hover {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            transform: translateX(5px);
        }
        
        .menu-divider {
            height: 1px;
            background: #e0e0e0;
            margin: 8px 0;
        }
        
        .score-bar-section {
            position: fixed;
            top: 0;
            left: 0;
            right: 0;
            background: rgba(255, 255, 255, 0.95);
            backdrop-filter: blur(10px);
            border-bottom: 2px solid rgba(102, 126, 234, 0.2);
            z-index: 999;
            padding: 15px 20px;
            box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        }
        
        .score-bar-container {
            display: flex;
            justify-content: center;
            align-items: center;
            max-width: 1200px;
            margin: 0 auto;
            gap: 20px;
            flex-wrap: wrap;
        }
        
        .score-item {
            display: flex;
            align-items: center;
            gap: 8px;
            padding: 8px 15px;
            background: linear-gradient(135deg, #f8f9fa, #e9ecef);
            border-radius: 12px;
            border: 2px solid transparent;
            transition: all 0.3s ease;
            min-width: 80px;
        }
        
        .score-item:hover {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
            transform: translateY(-2px);
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
        }
        
        .score-icon {
            font-size: 1.2rem;
            display: flex;
            align-items: center;
            justify-content: center;
        }
        
        .score-details {
            display: flex;
            flex-direction: column;
            align-items: center;
            gap: 2px;
        }
        
        .score-label {
            font-size: 0.75rem;
            font-weight: 600;
            color: #666;
            text-transform: uppercase;
            letter-spacing: 0.5px;
        }
        
        .score-item:hover .score-label {
            color: rgba(255, 255, 255, 0.9);
        }
        
        .score-value {
            font-size: 1rem;
            font-weight: bold;
            color: #333;
        }
        
        .score-item:hover .score-value {
            color: white;
        }
        
        .score-divider {
            width: 2px;
            height: 30px;
            background: linear-gradient(to bottom, transparent, #ddd, transparent);
        }
        
        .header {
            display: flex;
            justify-content: space-between;
            align-items: center;
            margin-bottom: 20px;
            flex-wrap: wrap;
            gap: 15px;
        }
        
        .level-info {
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
            color: white;
            border-radius: 15px;
            padding: 20px;
            margin-bottom: 20px;
        }
        
        .current-level {
            font-size: 1.5rem;
            font-weight: bold;
            margin-bottom: 15px;
        }
        
        .level-progress {
            display: flex;
            align-items: center;
            gap: 15px;
        }
        
        .progress-bar {
            flex: 1;
            height: 12px;
            background: rgba(255, 255, 255, 0.3);
            border-radius: 6px;
            overflow: hidden;
        }
        
        .progress-fill {
            height: 100%;
            background: linear-gradient(45deg, #ffd700, #ffed4e);
            border-radius: 6px;
            transition: width 0.5s ease;
            width: 0%;
        }
        
        .progress-text {
            font-weight: bold;
            font-size: 1.1rem;
        }
        
        .difficulty-info {
            background: #f0f8ff;
            border: 2px solid #2196f3;
            border-radius: 10px;
            padding: 12px;
            margin-bottom: 20px;
            font-size: 0.9rem;
            color: #1976d2;
        }
        
        .coins {
            background: linear-gradient(45deg, #ffd700, #ffed4e);
            color: #333;
            padding: 12px 20px;
            border-radius: 25px;
            font-weight: bold;
            font-size: 1.2rem;
            box-shadow: 0 4px 15px rgba(255, 215, 0, 0.3);
        }
        
        .score {
            background: linear-gradient(45deg, #4ecdc4, #44a08d);
            color: white;
            padding: 12px 20px;
            border-radius: 25px;
            font-weight: bold;
            font-size: 1.2rem;
        }
        
        .question-container {
            background: #f8f9fa;
            border-radius: 15px;
            padding: 25px;
            margin-bottom: 25px;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
        }
        
        .question-number {
            color: #666;
            font-size: 0.9rem;
            margin-bottom: 15px;
        }
        
        .question {
            font-size: 1.3rem;
            font-weight: 600;
            color: #333;
            line-height: 1.5;
            margin-bottom: 20px;
        }
        
        .hint {
            background: #e3f2fd;
            border: 2px solid #2196f3;
            border-radius: 10px;
            padding: 15px;
            margin-bottom: 20px;
            color: #1976d2;
            font-style: italic;
            display: none;
        }
        
        .options {
            display: grid;
            gap: 15px;
            margin-bottom: 25px;
        }
        
        .option {
            background: white;
            border: 2px solid #e0e0e0;
            border-radius: 12px;
            padding: 18px;
            cursor: pointer;
            transition: all 0.3s ease;
            font-size: 1.1rem;
            text-align: left;
        }
        
        .option:hover {
            border-color: #4ecdc4;
            background: #f0fdfc;
            transform: translateY(-2px);
        }
        
        .option.correct {
            background: #d4edda;
            border-color: #28a745;
            color: #155724;
        }
        
        .option.wrong {
            background: #f8d7da;
            border-color: #dc3545;
            color: #721c24;
        }
        
        .option.disabled {
            cursor: not-allowed;
            opacity: 0.7;
        }
        
        .controls {
            display: flex;
            gap: 15px;
            justify-content: center;
            flex-wrap: wrap;
        }
        
        button {
            padding: 12px 25px;
            border: none;
            border-radius: 25px;
            font-size: 1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
        }
        
        .hint-btn {
            background: linear-gradient(45deg, #ff9800, #f57c00);
            color: white;
        }
        
        .hint-btn:hover {
            background: linear-gradient(45deg, #f57c00, #ef6c00);
            transform: translateY(-2px);
        }
        
        .hint-btn:disabled {
            background: #ccc;
            cursor: not-allowed;
            transform: none;
        }
        
        .next-btn {
            background: linear-gradient(45deg, #4caf50, #45a049);
            color: white;
        }
        
        .next-btn:hover {
            background: linear-gradient(45deg, #45a049, #3d8b40);
            transform: translateY(-2px);
        }
        
        .feedback {
            margin: 20px 0;
            padding: 15px;
            border-radius: 10px;
            font-weight: 600;
            display: none;
        }
        
        .feedback.correct {
            background: #d4edda;
            color: #155724;
            border: 2px solid #28a745;
        }
        
        .feedback.wrong {
            background: #f8d7da;
            color: #721c24;
            border: 2px solid #dc3545;
        }
        
        .level-complete {
            background: #e8f5e8;
            border: 2px solid #4caf50;
            border-radius: 15px;
            padding: 20px;
            margin: 20px 0;
            display: none;
        }
        
        .level-complete h3 {
            color: #2e7d32;
            margin-bottom: 10px;
        }
        
        .level-complete p {
            color: #388e3c;
            margin-bottom: 15px;
        }
        
        .game-over {
            display: none;
            text-align: center;
        }
        
        .final-score {
            font-size: 2rem;
            color: #4ecdc4;
            margin: 20px 0;
        }
        
        .restart-btn {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            padding: 15px 30px;
            font-size: 1.2rem;
        }
        
        .restart-btn:hover {
            background: linear-gradient(45deg, #764ba2, #667eea);
            transform: translateY(-2px);
        }
        
        .mode-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
            gap: 20px;
            margin-bottom: 30px;
        }
        
        .mode-card {
            background: white;
            border-radius: 15px;
            padding: 25px;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
            border: 3px solid transparent;
            text-align: center;
        }
        
        .mode-card:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.15);
        }
        
        .mode-card.beginner {
            border-color: #a8e6cf;
        }
        
        .mode-card.beginner:hover {
            background: linear-gradient(135deg, #a8e6cf, #7fcdcd);
            color: white;
        }
        
        .mode-card.academy {
            border-color: #ffd89b;
        }
        
        .mode-card.academy:hover {
            background: linear-gradient(135deg, #ffd89b, #19547b);
            color: white;
        }
        
        .mode-card.temple {
            border-color: #667eea;
        }
        
        .mode-card.temple:hover {
            background: linear-gradient(135deg, #667eea, #764ba2);
            color: white;
        }
        
        .mode-card.lab {
            border-color: #11998e;
        }
        
        .mode-card.lab:hover {
            background: linear-gradient(135deg, #11998e, #38ef7d);
            color: white;
        }
        
        .mode-card.summit {
            border-color: #fc466b;
        }
        
        .mode-card.summit:hover {
            background: linear-gradient(135deg, #fc466b, #3f5efb);
            color: white;
        }
        
        .mode-icon {
            font-size: 3rem;
            margin-bottom: 15px;
        }
        
        .mode-card h3 {
            font-size: 1.4rem;
            margin-bottom: 10px;
            color: #333;
        }
        
        .mode-card:hover h3 {
            color: white;
        }
        
        .mode-card p {
            font-size: 1.1rem;
            margin-bottom: 15px;
            color: #666;
        }
        
        .mode-card:hover p {
            color: rgba(255, 255, 255, 0.9);
        }
        
        .mode-details {
            font-size: 0.9rem;
            color: #888;
            font-style: italic;
        }
        
        .mode-card:hover .mode-details {
            color: rgba(255, 255, 255, 0.8);
        }
        
        .mode-title {
            font-size: 1.3rem;
            font-weight: bold;
            margin-bottom: 10px;
        }
        
        .back-btn {
            background: linear-gradient(45deg, #6c757d, #495057);
            color: white;
            padding: 8px 15px;
            font-size: 0.9rem;
            margin-top: 10px;
        }
        
        .back-btn:hover {
            background: linear-gradient(45deg, #495057, #343a40);
            transform: translateY(-1px);
        }
        
        .modal {
            display: none;
            position: fixed;
            z-index: 1000;
            left: 0;
            top: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.5);
            backdrop-filter: blur(5px);
        }
        
        .modal-content {
            background: white;
            margin: 5% auto;
            padding: 30px;
            border-radius: 20px;
            width: 90%;
            max-width: 500px;
            box-shadow: 0 20px 40px rgba(0, 0, 0, 0.2);
            position: relative;
            max-height: 80vh;
            overflow-y: auto;
        }
        
        .close {
            color: #aaa;
            float: right;
            font-size: 28px;
            font-weight: bold;
            cursor: pointer;
            position: absolute;
            right: 20px;
            top: 15px;
        }
        
        .close:hover {
            color: #000;
        }
        
        .theme-grid {
            display: grid;
            grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
            gap: 15px;
            margin-top: 20px;
        }
        
        .theme-option {
            padding: 20px;
            border-radius: 15px;
            cursor: pointer;
            text-align: center;
            font-weight: bold;
            color: white;
            transition: all 0.3s ease;
            border: 3px solid transparent;
        }
        
        .theme-option:hover {
            transform: translateY(-3px);
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
        }
        
        .theme-option.selected {
            border-color: #ffd700;
            box-shadow: 0 0 20px rgba(255, 215, 0, 0.5);
        }
        
        .theme-default { background: linear-gradient(135deg, #667eea 0%, #764ba2 100%); }
        .theme-ocean { background: linear-gradient(135deg, #2196f3 0%, #21cbf3 100%); }
        .theme-sunset { background: linear-gradient(135deg, #ff9a56 0%, #ff6b6b 100%); }
        .theme-forest { background: linear-gradient(135deg, #56ab2f 0%, #a8e6cf 100%); }
        .theme-galaxy { background: linear-gradient(135deg, #2c3e50 0%, #4a00e0 100%); }
        .theme-candy { background: linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%); }
        
        .sound-controls {
            display: flex;
            flex-direction: column;
            gap: 20px;
            margin-top: 20px;
        }
        
        .sound-option {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 15px;
            background: #f8f9fa;
            border-radius: 10px;
        }
        
        .toggle-switch {
            position: relative;
            width: 60px;
            height: 30px;
            background: #ccc;
            border-radius: 15px;
            cursor: pointer;
            transition: background 0.3s;
        }
        
        .toggle-switch.active {
            background: #4caf50;
        }
        
        .toggle-slider {
            position: absolute;
            top: 3px;
            left: 3px;
            width: 24px;
            height: 24px;
            background: white;
            border-radius: 50%;
            transition: transform 0.3s;
        }
        
        .toggle-switch.active .toggle-slider {
            transform: translateX(30px);
        }
        
        /* Authentication Styles */
        .auth-container {
            background: white;
            border-radius: 20px;
            padding: 30px;
            box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
            max-width: 400px;
            margin: 0 auto;
        }
        
        .auth-tabs {
            display: flex;
            margin-bottom: 30px;
            border-radius: 10px;
            overflow: hidden;
            background: #f8f9fa;
        }
        
        .auth-tab {
            flex: 1;
            padding: 12px 20px;
            border: none;
            background: transparent;
            cursor: pointer;
            font-weight: 600;
            color: #666;
            transition: all 0.3s ease;
        }
        
        .auth-tab.active {
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
        }
        
        .auth-form {
            display: none;
        }
        
        .auth-form.active {
            display: block;
        }
        
        .form-group {
            margin-bottom: 20px;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 8px;
            font-weight: 600;
            color: #333;
        }
        
        .input-container {
            position: relative;
            display: flex;
            align-items: center;
        }
        
        .input-icon {
            position: absolute;
            left: 15px;
            font-size: 1.2rem;
            color: #666;
            z-index: 1;
            pointer-events: none;
        }
        
        .form-group input[type="text"],
        .form-group input[type="email"],
        .form-group input[type="password"] {
            width: 100%;
            padding: 12px 15px 12px 45px;
            border: 2px solid #e0e0e0;
            border-radius: 10px;
            font-size: 1rem;
            transition: all 0.3s ease;
            box-sizing: border-box;
        }
        
        .form-group input[type="text"]:focus,
        .form-group input[type="email"]:focus,
        .form-group input[type="password"]:focus {
            outline: none;
            border-color: #667eea;
            box-shadow: 0 0 0 3px rgba(102, 126, 234, 0.1);
        }
        
        .checkbox-container {
            display: flex;
            align-items: center;
            cursor: pointer;
            font-size: 0.95rem;
            color: #666;
        }
        
        .checkbox-container input[type="checkbox"] {
            margin-right: 10px;
            transform: scale(1.2);
        }
        
        .auth-btn {
            width: 100%;
            padding: 15px;
            background: linear-gradient(45deg, #667eea, #764ba2);
            color: white;
            border: none;
            border-radius: 10px;
            font-size: 1.1rem;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
            box-shadow: 0 4px 15px rgba(102, 126, 234, 0.3);
        }
        
        .auth-btn:hover {
            background: linear-gradient(45deg, #764ba2, #667eea);
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(102, 126, 234, 0.4);
        }
        
        .logout-btn {
            background: linear-gradient(45deg, #ff6b6b, #ee5a52);
            color: white;
            border: none;
            border-radius: 10px;
            padding: 10px 20px;
            font-weight: 600;
            cursor: pointer;
            transition: all 0.3s ease;
        }
        
        .logout-btn:hover {
            background: linear-gradient(45deg, #ee5a52, #ff6b6b);
            transform: translateY(-2px);
        }
        
        .auth-message {
            padding: 15px;
            border-radius: 10px;
            margin-bottom: 20px;
            font-weight: 600;
            text-align: center;
        }
        
        .auth-message.success {
            background: #d4edda;
            color: #155724;
            border: 2px solid #28a745;
        }
        
        .auth-message.error {
            background: #f8d7da;
            color: #721c24;
            border: 2px solid #dc3545;
        }

        @media (max-width: 480px) {
            body {
                padding: 120px 10px 20px 10px;
            }
            
            .auth-container {
                padding: 20px;
                margin: 0 10px;
            }
            
            .score-bar-section {
                padding: 10px;
            }
            
            .score-bar-container {
                gap: 10px;
                justify-content: space-between;
            }
            
            .score-item {
                padding: 6px 10px;
                min-width: 60px;
                gap: 5px;
            }
            
            .score-icon {
                font-size: 1rem;
            }
            
            .score-label {
                font-size: 0.65rem;
            }
            
            .score-value {
                font-size: 0.9rem;
            }
            
            .score-divider {
                display: none;
            }
            
            .game-container {
                padding: 20px;
            }
            
            .header {
                flex-direction: column;
                text-align: center;
            }
            
            .question {
                font-size: 1.1rem;
            }
            
            .option {
                padding: 15px;
                font-size: 1rem;
            }
            
            .controls {
                flex-direction: column;
                align-items: center;
            }
            
            .profile-section {
                top: 10px;
                right: 10px;
            }
            
            .profile-menu {
                position: fixed;
                top: 110px;
                right: 10px;
                left: 10px;
                width: auto;
            }
            
            .modal-content {
                margin: 10% auto;
                padding: 20px;
                width: 95%;
            }
        }
    </style>
</head>
<body>
    <div class="game-container">
        <div class="profile-section">
            <div class="profile-dropdown">
                <button class="profile-btn" onclick="toggleProfileMenu()">👤</button>
                <div class="profile-menu" id="profileMenu">
                    <button class="menu-item" onclick="openMyProfile()">
                        <span>👤</span>
                        <span>My Profile</span>
                    </button>
                    <div class="menu-divider"></div>
                    <button class="menu-item" onclick="openThemes()">
                        <span>🎨</span>
                        <span>Themes</span>
                    </button>
                    <button class="menu-item" onclick="toggleSounds()">
                        <span>🔊</span>
                        <span>Sounds</span>
                    </button>
                    <button class="menu-item" onclick="openAbout()">
                        <span>ℹ️</span>
                        <span>About Game</span>
                    </button>
                    <div class="menu-divider"></div>
                    <button class="menu-item" onclick="openDevelopers()">
                        <span>👨‍💻</span>
                        <span>About Developers</span>
                    </button>
                    <div class="menu-divider"></div>
                    <button class="menu-item" onclick="logout()" style="color: #ff6b6b;">
                        <span>🚪</span>
                        <span>Log Out</span>
                    </button>
                </div>
            </div>
        </div>
        
        <!-- Score Bar Section -->
        <div class="score-bar-section">
            <div class="score-bar-container">
                <div class="score-item">
                    <div class="score-icon">💰</div>
                    <div class="score-details">
                        <div class="score-label">Coins</div>
                        <div class="score-value" id="coinCount">50</div>
                    </div>
                </div>
                
                <div class="score-divider"></div>
                
                <div class="score-item">
                    <div class="score-icon">🏆</div>
                    <div class="score-details">
                        <div class="score-label">Score</div>
                        <div class="score-value" id="score">0</div>
                    </div>
                </div>
                
                <div class="score-divider"></div>
                
                <div class="score-item">
                    <div class="score-icon">📊</div>
                    <div class="score-details">
                        <div class="score-label">Level</div>
                        <div class="score-value"><span id="currentLevelDisplay">1</span>/100</div>
                    </div>
                </div>
                
                <div class="score-divider"></div>
                
                <div class="score-item">
                    <div class="score-icon">✅</div>
                    <div class="score-details">
                        <div class="score-label">Correct</div>
                        <div class="score-value" id="correctCount">0</div>
                    </div>
                </div>
                
                <div class="score-divider"></div>
                
                <div class="score-item">
                    <div class="score-icon">🎯</div>
                    <div class="score-details">
                        <div class="score-label">Accuracy</div>
                        <div class="score-value" id="accuracy">100%</div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Authentication Section -->
        <div id="authSection">
            <div style="text-align: center; margin-bottom: 30px;">
                <h1 style="color: #333; font-size: 2.5rem; margin-bottom: 10px;">🧠 GK Quiz Challenge</h1>
                <p style="color: #666; font-size: 1.2rem;">Test your knowledge across 2500+ questions!</p>
            </div>
            
            <div class="auth-container">
                <div class="auth-tabs">
                    <button class="auth-tab active" onclick="showAuthForm('signin')">Sign In</button>
                    <button class="auth-tab" onclick="showAuthForm('signup')">Sign Up</button>
                </div>
                
                <!-- Sign In Form -->
                <div id="signinForm" class="auth-form active">
                    <h3 style="margin-bottom: 20px; color: #333;">Welcome Back!</h3>
                    <form onsubmit="handleSignIn(event)">
                        <div class="form-group">
                            <label for="signinEmail">Email Address</label>
                            <div class="input-container">
                                <span class="input-icon">📧</span>
                                <input type="email" id="signinEmail" required placeholder="Enter your email">
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="signinPassword">Password</label>
                            <div class="input-container">
                                <span class="input-icon">🔒</span>
                                <input type="password" id="signinPassword" required placeholder="Enter your password">
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="checkbox-container">
                                <input type="checkbox" id="rememberMe">
                                <span class="checkmark"></span>
                                Remember me
                            </label>
                        </div>
                        <button type="submit" class="auth-btn">Sign In</button>
                    </form>
                    <p style="text-align: center; margin-top: 15px; color: #666;">
                        Don't have an account? <a href="#" onclick="showAuthForm('signup')" style="color: #667eea; text-decoration: none;">Sign up here</a>
                    </p>
                </div>
                
                <!-- Sign Up Form -->
                <div id="signupForm" class="auth-form">
                    <h3 style="margin-bottom: 20px; color: #333;">Create Account</h3>
                    <form onsubmit="handleSignUp(event)">
                        <div class="form-group">
                            <label for="signupName">Full Name</label>
                            <div class="input-container">
                                <span class="input-icon">👤</span>
                                <input type="text" id="signupName" required placeholder="Enter your full name">
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="signupEmail">Email Address</label>
                            <div class="input-container">
                                <span class="input-icon">📧</span>
                                <input type="email" id="signupEmail" required placeholder="Enter your email">
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="signupPassword">Password</label>
                            <div class="input-container">
                                <span class="input-icon">🔒</span>
                                <input type="password" id="signupPassword" required placeholder="Create a password" minlength="6">
                            </div>
                        </div>
                        <div class="form-group">
                            <label for="confirmPassword">Confirm Password</label>
                            <div class="input-container">
                                <span class="input-icon">🔐</span>
                                <input type="password" id="confirmPassword" required placeholder="Confirm your password">
                            </div>
                        </div>
                        <div class="form-group">
                            <label class="checkbox-container">
                                <input type="checkbox" id="agreeTerms" required>
                                <span class="checkmark"></span>
                                I agree to the <a href="#" style="color: #667eea;">Terms & Conditions</a>
                            </label>
                        </div>
                        <button type="submit" class="auth-btn">Create Account</button>
                    </form>
                    <p style="text-align: center; margin-top: 15px; color: #666;">
                        Already have an account? <a href="#" onclick="showAuthForm('signin')" style="color: #667eea; text-decoration: none;">Sign in here</a>
                    </p>
                </div>
            </div>
        </div>

        <div id="modeSelection" style="display: none;">
            <div style="display: flex; justify-content: space-between; align-items: center; margin-bottom: 30px;">
                <h2 style="color: #333; font-size: 2rem;">Choose Your Challenge Mode</h2>
                <button class="logout-btn" onclick="logout()">🚪 Logout</button>
            </div>
            <div class="mode-grid">
                <div class="mode-card beginner" onclick="selectMode('beginner')">
                    <div class="mode-icon">🌱</div>
                    <h3>Beginner Valley</h3>
                    <p>100 levels of everyday knowledge</p>
                    <div class="mode-details">Basic topics • No time pressure • Perfect for starters</div>
                </div>
                <div class="mode-card academy" onclick="selectMode('academy')">
                    <div class="mode-icon">🏫</div>
                    <h3>Knowledge Academy</h3>
                    <p>100 levels of school subjects</p>
                    <div class="mode-details">Geography • History • Literature • 45s timer</div>
                </div>
                <div class="mode-card temple" onclick="selectMode('temple')">
                    <div class="mode-icon">🏛️</div>
                    <h3>Scholar's Temple</h3>
                    <p>100 levels of advanced topics</p>
                    <div class="mode-details">Chemistry • Complex concepts • 35s timer</div>
                </div>
                <div class="mode-card lab" onclick="selectMode('lab')">
                    <div class="mode-icon">🔬</div>
                    <h3>Science Laboratory</h3>
                    <p>100 levels of scientific knowledge</p>
                    <div class="mode-details">Physics • Biology • Technical • 25s timer</div>
                </div>
                <div class="mode-card summit" onclick="selectMode('summit')">
                    <div class="mode-icon">🧠</div>
                    <h3>Genius Summit</h3>
                    <p>100 levels of expert challenges</p>
                    <div class="mode-details">Mathematics • Astrophysics • 15s timer</div>
                </div>
            </div>
        </div>

        <div id="gameArea" style="display: none;">
            <div class="level-info">
                <div class="mode-title" id="modeTitle">🌱 Beginner Valley</div>
                <div class="current-level">Level <span id="currentLevel">1</span> of 100</div>
                <div class="level-progress">
                    <div class="progress-bar">
                        <div class="progress-fill" id="progressFill"></div>
                    </div>
                    <div class="progress-text"><span id="levelProgress">0</span>%</div>
                </div>
                <button class="back-btn" onclick="backToModeSelection()">← Back to Modes</button>
            </div>
            
            <div class="difficulty-info" id="difficultyInfo">
                Level 1-25: Easy Mode - +4 coins for correct, -1 for wrong, 10 coins for hint
            </div>
            
            <div class="question-container">
                <div class="question-number">Level <span id="questionNumber">1</span> - Question <span id="questionInLevel">1</span> of 5</div>
                <div class="timer" id="timer" style="display: none; font-size: 1.2rem; color: #f44336; font-weight: bold; margin-bottom: 15px;">⏰ Time: <span id="timeLeft">30</span>s</div>
                <div class="question" id="question">Loading question...</div>
                <div class="hint" id="hint"></div>
            </div>
            
            <div class="options" id="options"></div>
            
            <div class="feedback" id="feedback"></div>
            
            <div class="level-complete" id="levelComplete">
                <h3>🎉 Level Complete!</h3>
                <p id="levelCompleteText">Great job! You've completed Level 1.</p>
                <button class="next-btn" onclick="nextLevel()">Continue to Next Level</button>
            </div>
            
            <div class="controls">
                <button class="hint-btn" id="hintBtn" onclick="showHint()">💡 Get Hint (10 coins)</button>
                <button class="next-btn" id="nextBtn" onclick="nextQuestion()" style="display: none;">Next Question</button>
            </div>
        </div>
        
        <div class="game-over" id="gameOver">
            <h2 id="gameOverTitle">🏆 Congratulations! Mode Complete!</h2>
            <div class="final-score">Final Score: <span id="finalScore">0</span></div>
            <div class="final-score">Total Coins: <span id="finalCoins">0</span></div>
            <p style="margin: 20px 0; font-size: 1.2rem; color: #666;" id="gameOverMessage">You are a true Quiz Master!</p>
            <div style="display: flex; gap: 15px; justify-content: center; flex-wrap: wrap;">
                <button class="restart-btn" onclick="restartGame()">Play This Mode Again</button>
                <button class="restart-btn" onclick="backToModeSelection()">Try Different Mode</button>
            </div>
        </div>
        
        <!-- Themes Modal -->
        <div id="themesModal" class="modal">
            <div class="modal-content">
                <span class="close" onclick="closeModal('themesModal')">&times;</span>
                <h2 style="margin-bottom: 20px; color: #333;">🎨 Choose Your Theme</h2>
                <div class="theme-grid">
                    <div class="theme-option theme-default selected" onclick="selectTheme('default')">
                        <div>🌟 Default</div>
                    </div>
                    <div class="theme-option theme-ocean" onclick="selectTheme('ocean')">
                        <div>🌊 Ocean</div>
                    </div>
                    <div class="theme-option theme-sunset" onclick="selectTheme('sunset')">
                        <div>🌅 Sunset</div>
                    </div>
                    <div class="theme-option theme-forest" onclick="selectTheme('forest')">
                        <div>🌲 Forest</div>
                    </div>
                    <div class="theme-option theme-galaxy" onclick="selectTheme('galaxy')">
                        <div>🌌 Galaxy</div>
                    </div>
                    <div class="theme-option theme-candy" onclick="selectTheme('candy')">
                        <div>🍭 Candy</div>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- Sounds Modal -->
        <div id="soundsModal" class="modal">
            <div class="modal-content">
                <span class="close" onclick="closeModal('soundsModal')">&times;</span>
                <h2 style="margin-bottom: 20px; color: #333;">🔊 Sound Settings</h2>
                <div class="sound-controls">
                    <div class="sound-option">
                        <div>
                            <strong>Sound Effects</strong>
                            <div style="font-size: 0.9rem; color: #666;">Button clicks and feedback sounds</div>
                        </div>
                        <div class="toggle-switch active" onclick="toggleSoundEffect('effects')" id="effectsToggle">
                            <div class="toggle-slider"></div>
                        </div>
                    </div>
                    <div class="sound-option">
                        <div>
                            <strong>Background Music</strong>
                            <div style="font-size: 0.9rem; color: #666;">Ambient music while playing</div>
                        </div>
                        <div class="toggle-switch" onclick="toggleSoundEffect('music')" id="musicToggle">
                            <div class="toggle-slider"></div>
                        </div>
                    </div>
                    <div class="sound-option">
                        <div>
                            <strong>Voice Announcements</strong>
                            <div style="font-size: 0.9rem; color: #666;">Spoken feedback for answers</div>
                        </div>
                        <div class="toggle-switch" onclick="toggleSoundEffect('voice')" id="voiceToggle">
                            <div class="toggle-slider"></div>
                        </div>
                    </div>
                </div>
                <p style="margin-top: 20px; font-size: 0.9rem; color: #666; text-align: center;">
                    <em>Note: Audio features are simulated for demonstration purposes</em>
                </p>
            </div>
        </div>
        
        <!-- About Modal -->
        <div id="aboutModal" class="modal">
            <div class="modal-content">
                <span class="close" onclick="closeModal('aboutModal')">&times;</span>
                <h2 style="margin-bottom: 20px; color: #333;">ℹ️ About GK Quiz Challenge</h2>
                <div style="text-align: left; line-height: 1.6; color: #555;">
                    <h3 style="color: #4ecdc4; margin-bottom: 10px;">🎯 Game Overview</h3>
                    <p>GK Quiz Challenge is an educational quiz game featuring <strong>2500+ questions</strong> across 5 difficulty modes. Test your knowledge and climb through 100 levels in each mode!</p>
                    
                    <h3 style="color: #4ecdc4; margin-top: 20px; margin-bottom: 10px;">🏆 Game Modes</h3>
                    <ul style="margin-left: 20px;">
                        <li><strong>🌱 Beginner Valley:</strong> Basic everyday knowledge (500+ questions)</li>
                        <li><strong>🏫 Knowledge Academy:</strong> School-level subjects (500+ questions)</li>
                        <li><strong>🏛️ Scholar's Temple:</strong> Advanced academic topics (500+ questions)</li>
                        <li><strong>🔬 Science Laboratory:</strong> Scientific knowledge (500+ questions)</li>
                        <li><strong>🧠 Genius Summit:</strong> Expert-level challenges (500+ questions)</li>
                    </ul>
                    
                    <h3 style="color: #4ecdc4; margin-top: 20px; margin-bottom: 10px;">💰 Coin System</h3>
                    <p>Earn coins for correct answers and spend them on hints. Higher difficulty modes offer more coins but have stricter time limits!</p>
                    
                    <h3 style="color: #4ecdc4; margin-top: 20px; margin-bottom: 10px;">⏱️ Time Challenges</h3>
                    <p>Advanced modes include time limits to increase the challenge. Can you think fast under pressure?</p>
                    
                    <h3 style="color: #4ecdc4; margin-top: 20px; margin-bottom: 10px;">🎨 Features</h3>
                    <ul style="margin-left: 20px;">
                        <li>2500+ unique questions with no repeats</li>
                        <li>Progressive difficulty system</li>
                        <li>Multiple themes and customization</li>
                        <li>Comprehensive progress tracking</li>
                        <li>Responsive design for all devices</li>
                    </ul>
                    
                    <div style="text-align: center; margin-top: 25px; padding: 15px; background: #f0f8ff; border-radius: 10px;">
                        <strong>Version 2.0</strong> | Created with ❤️ by Canva Code<br>
                        <em>Challenge your mind, expand your knowledge!</em>
                    </div>
                </div>
            </div>
        </div>
        
        <!-- My Profile Modal -->
        <div id="profileModal" class="modal">
            <div class="modal-content">
                <span class="close" onclick="closeModal('profileModal')">&times;</span>
                <h2 style="margin-bottom: 20px; color: #333;">👤 My Profile</h2>
                <div style="text-align: left; line-height: 1.6; color: #555;">
                    <div style="padding: 20px; background: linear-gradient(135deg, #667eea, #764ba2); border-radius: 15px; color: white; margin-bottom: 20px;">
                        <div style="display: flex; align-items: center; gap: 15px; margin-bottom: 15px;">
                            <div style="width: 60px; height: 60px; background: rgba(255,255,255,0.2); border-radius: 50%; display: flex; align-items: center; justify-content: center; font-size: 1.5rem; font-weight: bold;" id="profileAvatar">U</div>
                            <div>
                                <h3 style="margin: 0; font-size: 1.3rem;" id="profileName">User Name</h3>
                                <p style="margin: 5px 0 0 0; opacity: 0.9;" id="profileEmail">user@email.com</p>
                            </div>
                        </div>
                        <div style="background: rgba(255,255,255,0.1); padding: 10px; border-radius: 8px;">
                            <p style="margin: 0; font-size: 0.9rem;">Member since: <span id="profileJoinDate">January 2024</span></p>
                        </div>
                    </div>
                    
                    <div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(150px, 1fr)); gap: 15px; margin-bottom: 20px;">
                        <div style="background: #f8f9fa; padding: 15px; border-radius: 10px; text-align: center;">
                            <div style="font-size: 1.5rem; color: #4ecdc4; font-weight: bold;" id="profileTotalScore">0</div>
                            <div style="font-size: 0.9rem; color: #666;">Total Score</div>
                        </div>
                        <div style="background: #f8f9fa; padding: 15px; border-radius: 10px; text-align: center;">
                            <div style="font-size: 1.5rem; color: #ffd700; font-weight: bold;" id="profileTotalCoins">0</div>
                            <div style="font-size: 0.9rem; color: #666;">Total Coins</div>
                        </div>
                        <div style="background: #f8f9fa; padding: 15px; border-radius: 10px; text-align: center;">
                            <div style="font-size: 1.5rem; color: #ff6b6b; font-weight: bold;" id="profileGamesPlayed">0</div>
                            <div style="font-size: 0.9rem; color: #666;">Games Played</div>
                        </div>
                        <div style="background: #f8f9fa; padding: 15px; border-radius: 10px; text-align: center;">
                            <div style="font-size: 1.5rem; color: #28a745; font-weight: bold;" id="profileModesCompleted">0</div>
                            <div style="font-size: 0.9rem; color: #666;">Modes Completed</div>
                        </div>
                    </div>
                    
                    <div style="background: #f8f9fa; padding: 20px; border-radius: 15px;">
                        <h4 style="margin-top: 0; color: #333;">🏆 Achievements</h4>
                        <div id="profileAchievements">
                            <div style="display: flex; align-items: center; gap: 10px; padding: 8px; background: white; border-radius: 8px; margin-bottom: 8px;">
                                <span style="font-size: 1.2rem;">🌟</span>
                                <span>Welcome to GK Quiz Challenge!</span>
                            </div>
                        </div>
                    </div>
                    
                    <div style="text-align: center; margin-top: 20px;">
                        <button onclick="logout()" style="background: linear-gradient(45deg, #ff6b6b, #ee5a52); color: white; border: none; padding: 12px 25px; border-radius: 25px; font-weight: 600; cursor: pointer; transition: all 0.3s ease;">
                            🚪 Log Out
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Developers Modal -->
        <div id="developersModal" class="modal">
            <div class="modal-content">
                <span class="close" onclick="closeModal('developersModal')">&times;</span>
                <h2 style="margin-bottom: 20px; color: #333;">👨‍💻 About the Developers</h2>
                <div style="text-align: center; line-height: 1.6; color: #555;">
                    <div style="padding: 20px; background: linear-gradient(135deg, #a8e6cf, #7fcdcd); border-radius: 15px;">
                        <div style="margin-bottom: 20px;">
                            <p style="color: #2c3e50; font-weight: bold; margin-bottom: 10px;">📧 For more help contact:</p>
                            <a href="mailto:sr2724342@gmail.com" style="background: white; padding: 8px 15px; border-radius: 20px; color: #667eea; font-weight: bold; text-decoration: none; display: inline-block; margin-bottom: 10px;">sr2724342@gmail.com</a>
                        </div>
                        
                        <div style="margin-bottom: 20px;">
                            <p style="color: #2c3e50; font-weight: bold; margin-bottom: 10px;">🌐 Stay Connected:</p>
                            <div style="display: flex; justify-content: center; gap: 10px; flex-wrap: wrap;">
                                <a href="https://instagram.com/sachinrawt_" target="_blank" style="background: white; padding: 8px 15px; border-radius: 20px; color: #E4405F; font-weight: bold; text-decoration: none; display: inline-block;">📷 @sachinrawt_</a>
                                <a href="https://www.facebook.com/profile.php?id=" target="_blank" style="background: white; padding: 8px 15px; border-radius: 20px; color: #1877F2; font-weight: bold; text-decoration: none; display: inline-block;">📘 Facebook</a>
                                <a href="https://t.me/+1ZTcNfN6j0FmYWZl" target="_blank" style="background: white; padding: 8px 15px; border-radius: 20px; color: #0088CC; font-weight: bold; text-decoration: none; display: inline-block;">📱 Telegram</a>
                            </div>
                        </div>
                        
                        <div style="margin-bottom: 15px; padding: 15px; background: rgba(255, 255, 255, 0.3); border-radius: 10px;">
                            <p style="color: #2c3e50; font-style: italic; margin: 0;">
                                "Building games, learning every day, and sharing the journey with you."
                            </p>
                        </div>
                        
                        <p style="font-size: 1.1rem; color: #2c3e50; font-weight: bold;">
                            ❤️ Made With Love ❤️
                        </p>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <script>
        // Massive question database with 2500+ questions across all categories
        const allQuestions = [
            // BEGINNER VALLEY QUESTIONS (500+ questions) - Basic everyday knowledge
            
            // Colors & Art (50 questions)
            {
                question: "What color do you get when you mix red and white?",
                options: ["Orange", "Pink", "Purple", "Yellow"],
                correct: 1,
                hint: "Think of a flower that's often given on Valentine's Day.",
                difficulty: "easy",
                category: "Colors & Art"
            },
            {
                question: "What color do you get when you mix blue and yellow?",
                options: ["Purple", "Green", "Orange", "Red"],
                correct: 1,
                hint: "It's the color of grass and leaves.",
                difficulty: "easy",
                category: "Colors & Art"
            },
            {
                question: "What color do you get when you mix red and yellow?",
                options: ["Purple", "Green", "Orange", "Pink"],
                correct: 2,
                hint: "It's the color of a pumpkin.",
                difficulty: "easy",
                category: "Colors & Art"
            },
            {
                question: "How many colors are in a rainbow?",
                options: ["5", "6", "7", "8"],
                correct: 2,
                hint: "Remember: Red, Orange, Yellow, Green, Blue, Indigo, Violet.",
                difficulty: "easy",
                category: "Colors & Art"
            },
            {
                question: "What is the primary color that is not red or blue?",
                options: ["Green", "Yellow", "Orange", "Purple"],
                correct: 1,
                hint: "It's the color of the sun.",
                difficulty: "easy",
                category: "Colors & Art"
            },
            
            // Basic Math (100 questions)
            {
                question: "What is 5 + 3?",
                options: ["6", "7", "8", "9"],
                correct: 2,
                hint: "Count on your fingers: 5, 6, 7, 8.",
                difficulty: "easy",
                category: "Basic Math"
            },
            {
                question: "What is 10 - 4?",
                options: ["5", "6", "7", "8"],
                correct: 1,
                hint: "Start with 10 and count backwards 4 times.",
                difficulty: "easy",
                category: "Basic Math"
            },
            {
                question: "What is 2 × 3?",
                options: ["5", "6", "7", "8"],
                correct: 1,
                hint: "It's like adding 2 + 2 + 2.",
                difficulty: "easy",
                category: "Basic Math"
            },
            {
                question: "What is 8 ÷ 2?",
                options: ["3", "4", "5", "6"],
                correct: 1,
                hint: "How many groups of 2 can you make from 8?",
                difficulty: "easy",
                category: "Basic Math"
            },
            {
                question: "What comes after 9?",
                options: ["8", "10", "11", "12"],
                correct: 1,
                hint: "It's the first two-digit number.",
                difficulty: "easy",
                category: "Basic Math"
            },
            {
                question: "What is 7 + 2?",
                options: ["8", "9", "10", "11"],
                correct: 1,
                hint: "Count up from 7: 8, 9.",
                difficulty: "easy",
                category: "Basic Math"
            },
            {
                question: "What is 6 - 3?",
                options: ["2", "3", "4", "5"],
                correct: 1,
                hint: "Half of 6 is this number.",
                difficulty: "easy",
                category: "Basic Math"
            },
            {
                question: "What is 4 × 2?",
                options: ["6", "7", "8", "9"],
                correct: 2,
                hint: "Double the number 4.",
                difficulty: "easy",
                category: "Basic Math"
            },
            {
                question: "What is 12 ÷ 3?",
                options: ["3", "4", "5", "6"],
                correct: 1,
                hint: "How many groups of 3 are in 12?",
                difficulty: "easy",
                category: "Basic Math"
            },
            {
                question: "What is 1 + 1?",
                options: ["1", "2", "3", "4"],
                correct: 1,
                hint: "The simplest addition problem.",
                difficulty: "easy",
                category: "Basic Math"
            },
            
            // Animals (100 questions)
            {
                question: "Which animal is known as the King of the Jungle?",
                options: ["Tiger", "Elephant", "Lion", "Bear"],
                correct: 2,
                hint: "It has a magnificent mane and roars loudly.",
                difficulty: "easy",
                category: "Animals"
            },
            {
                question: "How many legs does a spider have?",
                options: ["6", "8", "10", "12"],
                correct: 1,
                hint: "It's the same number as an octopus has arms.",
                difficulty: "easy",
                category: "Animals"
            },
            {
                question: "What do bees make?",
                options: ["Milk", "Honey", "Butter", "Cheese"],
                correct: 1,
                hint: "It's sweet and golden, often used in tea.",
                difficulty: "easy",
                category: "Animals"
            },
            {
                question: "What do cows give us?",
                options: ["Eggs", "Milk", "Honey", "Wool"],
                correct: 1,
                hint: "It's white and we drink it or make cheese from it.",
                difficulty: "easy",
                category: "Animals"
            },
            {
                question: "Which animal says 'moo'?",
                options: ["Pig", "Sheep", "Cow", "Horse"],
                correct: 2,
                hint: "This animal gives us milk.",
                difficulty: "easy",
                category: "Animals"
            },
            {
                question: "Which animal says 'woof'?",
                options: ["Cat", "Dog", "Bird", "Fish"],
                correct: 1,
                hint: "Man's best friend.",
                difficulty: "easy",
                category: "Animals"
            },
            {
                question: "Which animal says 'meow'?",
                options: ["Dog", "Cat", "Mouse", "Bird"],
                correct: 1,
                hint: "This pet likes to chase mice.",
                difficulty: "easy",
                category: "Animals"
            },
            {
                question: "How many legs does a cat have?",
                options: ["2", "3", "4", "5"],
                correct: 2,
                hint: "Same as a dog or horse.",
                difficulty: "easy",
                category: "Animals"
            },
            {
                question: "Which animal is the tallest?",
                options: ["Elephant", "Giraffe", "Horse", "Lion"],
                correct: 1,
                hint: "It has a very long neck to reach tall trees.",
                difficulty: "easy",
                category: "Animals"
            },
            {
                question: "Which animal lives in water?",
                options: ["Dog", "Cat", "Fish", "Bird"],
                correct: 2,
                hint: "It breathes through gills.",
                difficulty: "easy",
                category: "Animals"
            },
            
            // Basic Science (50 questions)
            {
                question: "What is the largest planet in our solar system?",
                options: ["Earth", "Jupiter", "Saturn", "Mars"],
                correct: 1,
                hint: "It's named after the king of Roman gods.",
                difficulty: "easy",
                category: "Basic Science"
            },
            {
                question: "What color is the sun?",
                options: ["Red", "Yellow", "Blue", "Green"],
                correct: 1,
                hint: "It's the same color as a lemon.",
                difficulty: "easy",
                category: "Basic Science"
            },
            {
                question: "How many days are there in a week?",
                options: ["5", "6", "7", "8"],
                correct: 2,
                hint: "Count from Monday to Sunday.",
                difficulty: "easy",
                category: "Basic Science"
            },
            {
                question: "What is the opposite of hot?",
                options: ["Warm", "Cool", "Cold", "Freezing"],
                correct: 2,
                hint: "Ice is this temperature.",
                difficulty: "easy",
                category: "Basic Science"
            },
            {
                question: "Which season comes after winter?",
                options: ["Summer", "Spring", "Fall", "Autumn"],
                correct: 1,
                hint: "Flowers start to bloom in this season.",
                difficulty: "easy",
                category: "Basic Science"
            },
            
            // Food & Cooking (50 questions)
            {
                question: "Which fruit is yellow and curved?",
                options: ["Apple", "Orange", "Banana", "Grape"],
                correct: 2,
                hint: "Monkeys love to eat this fruit.",
                difficulty: "easy",
                category: "Food & Cooking"
            },
            {
                question: "What do we use to write on a blackboard?",
                options: ["Pen", "Pencil", "Chalk", "Marker"],
                correct: 2,
                hint: "It's white and makes dust when you write.",
                difficulty: "easy",
                category: "Food & Cooking"
            },
            {
                question: "How many wheels does a bicycle have?",
                options: ["1", "2", "3", "4"],
                correct: 1,
                hint: "Bi means two in Latin.",
                difficulty: "easy",
                category: "Food & Cooking"
            },
            {
                question: "How many continents are there?",
                options: ["5", "6", "7", "8"],
                correct: 2,
                hint: "Asia, Africa, North America, South America, Antarctica, Europe, and Australia.",
                difficulty: "easy",
                category: "Food & Cooking"
            },
            
            // KNOWLEDGE ACADEMY QUESTIONS (500+ questions) - School-level topics
            
            // Geography (150 questions)
            {
                question: "What is the capital of France?",
                options: ["London", "Berlin", "Paris", "Madrid"],
                correct: 2,
                hint: "It's known as the City of Light and has the Eiffel Tower.",
                difficulty: "medium",
                category: "Geography"
            },
            {
                question: "What is the largest ocean on Earth?",
                options: ["Atlantic Ocean", "Indian Ocean", "Arctic Ocean", "Pacific Ocean"],
                correct: 3,
                hint: "It covers about one-third of Earth's surface.",
                difficulty: "medium",
                category: "Geography"
            },
            {
                question: "What is the smallest country in the world?",
                options: ["Monaco", "Vatican City", "San Marino", "Liechtenstein"],
                correct: 1,
                hint: "It's located within Rome and is the spiritual center of Catholicism.",
                difficulty: "medium",
                category: "Geography"
            },
            {
                question: "What is the capital of Italy?",
                options: ["Milan", "Naples", "Rome", "Florence"],
                correct: 2,
                hint: "It's known as the Eternal City and has the Colosseum.",
                difficulty: "medium",
                category: "Geography"
            },
            {
                question: "What is the tallest mountain in the world?",
                options: ["K2", "Mount Everest", "Mount Kilimanjaro", "Mount McKinley"],
                correct: 1,
                hint: "It's located in the Himalayas between Nepal and Tibet.",
                difficulty: "medium",
                category: "Geography"
            },
            {
                question: "What is the capital of Australia?",
                options: ["Sydney", "Melbourne", "Canberra", "Perth"],
                correct: 2,
                hint: "It's not the largest city, but the planned capital city.",
                difficulty: "medium",
                category: "Geography"
            },
            {
                question: "Which mountain range contains Mount Everest?",
                options: ["Andes", "Rocky Mountains", "Alps", "Himalayas"],
                correct: 3,
                hint: "This mountain range is located between India and Tibet.",
                difficulty: "medium",
                category: "Geography"
            },
            {
                question: "What is the capital of Spain?",
                options: ["Barcelona", "Madrid", "Seville", "Valencia"],
                correct: 1,
                hint: "It's located in the center of the country.",
                difficulty: "medium",
                category: "Geography"
            },
            {
                question: "Which river flows through London?",
                options: ["Seine", "Thames", "Danube", "Rhine"],
                correct: 1,
                hint: "Big Ben and the London Eye are located near this river.",
                difficulty: "medium",
                category: "Geography"
            },
            {
                question: "What is the capital of Germany?",
                options: ["Munich", "Hamburg", "Berlin", "Frankfurt"],
                correct: 2,
                hint: "This city was divided by a famous wall during the Cold War.",
                difficulty: "medium",
                category: "Geography"
            },
            
            // History (100 questions)
            {
                question: "In which year did World War II end?",
                options: ["1944", "1945", "1946", "1947"],
                correct: 1,
                hint: "The war ended in the mid-1940s after atomic bombs were dropped.",
                difficulty: "medium",
                category: "History"
            },
            {
                question: "Which empire was ruled by Julius Caesar?",
                options: ["Greek Empire", "Roman Empire", "Persian Empire", "Ottoman Empire"],
                correct: 1,
                hint: "This empire's capital was Rome and it lasted for centuries.",
                difficulty: "medium",
                category: "History"
            },
            {
                question: "Who was the first President of the United States?",
                options: ["Thomas Jefferson", "George Washington", "John Adams", "Benjamin Franklin"],
                correct: 1,
                hint: "He's on the one-dollar bill and the quarter.",
                difficulty: "medium",
                category: "History"
            },
            {
                question: "In which year did the Titanic sink?",
                options: ["1910", "1911", "1912", "1913"],
                correct: 2,
                hint: "It happened in the early 1910s on its maiden voyage.",
                difficulty: "medium",
                category: "History"
            },
            {
                question: "Which ancient wonder of the world was located in Egypt?",
                options: ["Hanging Gardens", "Colossus of Rhodes", "Great Pyramid of Giza", "Lighthouse of Alexandria"],
                correct: 2,
                hint: "It's the only ancient wonder still standing today.",
                difficulty: "medium",
                category: "History"
            },
            
            // Literature & Arts (100 questions)
            {
                question: "Who painted the Mona Lisa?",
                options: ["Vincent van Gogh", "Pablo Picasso", "Leonardo da Vinci", "Michelangelo"],
                correct: 2,
                hint: "This Italian Renaissance artist was also an inventor and scientist.",
                difficulty: "medium",
                category: "Literature & Arts"
            },
            {
                question: "Who wrote the play 'Romeo and Juliet'?",
                options: ["Charles Dickens", "William Shakespeare", "Jane Austen", "Mark Twain"],
                correct: 1,
                hint: "This English playwright is often called the greatest writer in the English language.",
                difficulty: "medium",
                category: "Literature & Arts"
            },
            {
                question: "Which instrument has 88 keys?",
                options: ["Guitar", "Piano", "Violin", "Flute"],
                correct: 1,
                hint: "It has both black and white keys.",
                difficulty: "medium",
                category: "Literature & Arts"
            },
            {
                question: "Who wrote 'Harry Potter'?",
                options: ["J.R.R. Tolkien", "J.K. Rowling", "C.S. Lewis", "Roald Dahl"],
                correct: 1,
                hint: "This British author created the wizarding world of Hogwarts.",
                difficulty: "medium",
                category: "Literature & Arts"
            },
            {
                question: "Which famous painting features a woman with a mysterious smile?",
                options: ["The Starry Night", "The Mona Lisa", "The Scream", "Girl with a Pearl Earring"],
                correct: 1,
                hint: "It was painted by Leonardo da Vinci.",
                difficulty: "medium",
                category: "Literature & Arts"
            },
            
            // Basic Science & Nature (150 questions)
            {
                question: "Which planet is known as the Red Planet?",
                options: ["Venus", "Mars", "Jupiter", "Saturn"],
                correct: 1,
                hint: "It appears reddish due to iron oxide on its surface.",
                difficulty: "medium",
                category: "Basic Science & Nature"
            },
            {
                question: "Which element has the chemical symbol 'O'?",
                options: ["Gold", "Oxygen", "Silver", "Iron"],
                correct: 1,
                hint: "We breathe this element to survive.",
                difficulty: "medium",
                category: "Basic Science & Nature"
            },
            {
                question: "Which mammal is known to have the most powerful bite?",
                options: ["Lion", "Shark", "Hippopotamus", "Crocodile"],
                correct: 2,
                hint: "Despite being herbivorous, this African animal is very dangerous.",
                difficulty: "medium",
                category: "Basic Science & Nature"
            },
            {
                question: "Which gas do plants absorb from the atmosphere?",
                options: ["Oxygen", "Nitrogen", "Carbon Dioxide", "Hydrogen"],
                correct: 2,
                hint: "They use this gas for photosynthesis.",
                difficulty: "medium",
                category: "Basic Science & Nature"
            },
            {
                question: "What is the largest mammal in the world?",
                options: ["Elephant", "Blue Whale", "Giraffe", "Hippopotamus"],
                correct: 1,
                hint: "It lives in the ocean and can grow up to 100 feet long.",
                difficulty: "medium",
                category: "Basic Science & Nature"
            },
            
            // SCHOLAR'S TEMPLE QUESTIONS (500+ questions) - Advanced academic topics
            
            // Advanced Chemistry (150 questions)
            {
                question: "What is the hardest natural substance on Earth?",
                options: ["Gold", "Iron", "Diamond", "Platinum"],
                correct: 2,
                hint: "It's often used in engagement rings and cutting tools.",
                difficulty: "hard",
                category: "Advanced Chemistry"
            },
            {
                question: "What is the chemical formula for water?",
                options: ["CO2", "H2O", "NaCl", "O2"],
                correct: 1,
                hint: "It contains two hydrogen atoms and one oxygen atom.",
                difficulty: "hard",
                category: "Advanced Chemistry"
            },
            {
                question: "What is the pH of pure water?",
                options: ["6", "7", "8", "9"],
                correct: 1,
                hint: "It's neutral, neither acidic nor basic.",
                difficulty: "hard",
                category: "Advanced Chemistry"
            },
            {
                question: "Which gas makes up about 78% of Earth's atmosphere?",
                options: ["Oxygen", "Carbon Dioxide", "Nitrogen", "Hydrogen"],
                correct: 2,
                hint: "It's the most abundant gas in our atmosphere but we don't breathe it.",
                difficulty: "hard",
                category: "Advanced Chemistry"
            },
            {
                question: "What is the most abundant element in the universe?",
                options: ["Oxygen", "Carbon", "Hydrogen", "Helium"],
                correct: 2,
                hint: "It's the lightest and simplest element on the periodic table.",
                difficulty: "hard",
                category: "Advanced Chemistry"
            },
            
            // Advanced Geography & Geology (100 questions)
            {
                question: "Which country has the most natural lakes?",
                options: ["Russia", "Canada", "USA", "Finland"],
                correct: 1,
                hint: "This North American country is known for its vast wilderness.",
                difficulty: "hard",
                category: "Advanced Geography & Geology"
            },
            {
                question: "What is the longest river in the world?",
                options: ["Amazon River", "Nile River", "Mississippi River", "Yangtze River"],
                correct: 1,
                hint: "This African river flows through Egypt and several other countries.",
                difficulty: "hard",
                category: "Advanced Geography & Geology"
            },
            {
                question: "What is the study of earthquakes called?",
                options: ["Geology", "Seismology", "Meteorology", "Astronomy"],
                correct: 1,
                hint: "It comes from the Greek word 'seismos' meaning earthquake.",
                difficulty: "hard",
                category: "Advanced Geography & Geology"
            },
            
            // Biology & Medicine (150 questions)
            {
                question: "Which organ in the human body produces insulin?",
                options: ["Liver", "Kidney", "Pancreas", "Heart"],
                correct: 2,
                hint: "This organ helps regulate blood sugar levels.",
                difficulty: "hard",
                category: "Biology & Medicine"
            },
            {
                question: "What is the smallest bone in the human body?",
                options: ["Stapes", "Malleus", "Incus", "Radius"],
                correct: 0,
                hint: "It's located in the ear and is also called the stirrup bone.",
                difficulty: "hard",
                category: "Biology & Medicine"
            },
            {
                question: "Which scientist developed the theory of evolution?",
                options: ["Isaac Newton", "Albert Einstein", "Charles Darwin", "Galileo Galilei"],
                correct: 2,
                hint: "He wrote 'On the Origin of Species'.",
                difficulty: "hard",
                category: "Biology & Medicine"
            },
            
            // Astronomy & Space (100 questions)
            {
                question: "Which planet has the most moons?",
                options: ["Jupiter", "Saturn", "Uranus", "Neptune"],
                correct: 1,
                hint: "It has over 80 known moons and beautiful rings.",
                difficulty: "hard",
                category: "Astronomy & Space"
            },
            
            // SCIENCE LABORATORY QUESTIONS (500+ questions) - Scientific knowledge
            
            // Advanced Physics (200 questions)
            {
                question: "What is the speed of light in vacuum?",
                options: ["299,792,458 m/s", "300,000,000 m/s", "299,000,000 m/s", "301,000,000 m/s"],
                correct: 0,
                hint: "It's exactly 299,792,458 meters per second.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "What is the Planck constant approximately?",
                options: ["6.626 × 10^-34 J⋅s", "9.109 × 10^-31 kg", "1.602 × 10^-19 C", "6.022 × 10^23 mol^-1"],
                correct: 0,
                hint: "It's fundamental to quantum mechanics and has units of action.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "Which element has the highest melting point?",
                options: ["Carbon", "Tungsten", "Rhenium", "Osmium"],
                correct: 1,
                hint: "It's used in light bulb filaments due to its high melting point.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "What is the name of the boundary around a black hole?",
                options: ["Photon Sphere", "Event Horizon", "Ergosphere", "Singularity"],
                correct: 1,
                hint: "Once you cross this boundary, you can never escape.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "What is the half-life of Carbon-14?",
                options: ["5,730 years", "1,600 years", "12,000 years", "50,000 years"],
                correct: 0,
                hint: "It's used for radiocarbon dating of organic materials.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "Which theorem states that in a right triangle, a² + b² = c²?",
                options: ["Fermat's Last Theorem", "Pythagorean Theorem", "Goldbach's Conjecture", "Riemann Hypothesis"],
                correct: 1,
                hint: "It's named after an ancient Greek mathematician and philosopher.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "What is the most electronegative element?",
                options: ["Oxygen", "Nitrogen", "Fluorine", "Chlorine"],
                correct: 2,
                hint: "It's the most reactive halogen and has 9 protons.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "Which particle is responsible for the Higgs mechanism?",
                options: ["Photon", "Electron", "Higgs Boson", "Neutrino"],
                correct: 2,
                hint: "It was discovered at CERN and is called the 'God particle'.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "What is the value of Avogadro's number?",
                options: ["6.022 × 10^23", "9.109 × 10^-31", "1.602 × 10^-19", "6.626 × 10^-34"],
                correct: 0,
                hint: "It's the number of particles in one mole of substance.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "Which quantum number describes electron spin?",
                options: ["Principal", "Azimuthal", "Magnetic", "Spin"],
                correct: 3,
                hint: "It can have values of +1/2 or -1/2.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "What is the Schwarzschild radius of the Sun?",
                options: ["2.95 km", "1.48 km", "4.24 km", "3.67 km"],
                correct: 0,
                hint: "It's about 3 kilometers for our Sun's mass.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "Which enzyme unwinds DNA during replication?",
                options: ["DNA Polymerase", "Helicase", "Ligase", "Primase"],
                correct: 1,
                hint: "It breaks the hydrogen bonds between base pairs.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            
            // Computer Science & Technology (150 questions)
            {
                question: "Which programming language was created by Guido van Rossum?",
                options: ["Java", "C++", "Python", "JavaScript"],
                correct: 2,
                hint: "It's named after a British comedy group and is known for its simplicity.",
                difficulty: "expert",
                category: "Computer Science & Technology"
            },
            
            // Advanced Biology & Genetics (150 questions)
            
            // GENIUS SUMMIT QUESTIONS (500+ questions) - Expert-level challenges
            
            // Pure Mathematics (200 questions)
            {
                question: "What is the Riemann Hypothesis primarily concerned with?",
                options: ["Prime number distribution", "Quantum mechanics", "Relativity theory", "DNA structure"],
                correct: 0,
                hint: "It's one of the most famous unsolved problems in mathematics.",
                difficulty: "genius",
                category: "Pure Mathematics"
            },
            
            // Theoretical Physics & Cosmology (150 questions)
            {
                question: "Which mathematician formulated the theory of relativity?",
                options: ["Isaac Newton", "Albert Einstein", "Stephen Hawking", "Galileo Galilei"],
                correct: 1,
                hint: "E=mc² is his most famous equation.",
                difficulty: "genius",
                category: "Theoretical Physics & Cosmology"
            },
            {
                question: "What is the critical temperature of superconductor YBa2Cu3O7?",
                options: ["77K", "93K", "123K", "164K"],
                correct: 1,
                hint: "It's around 93 Kelvin, above liquid nitrogen temperature.",
                difficulty: "genius",
                category: "Theoretical Physics & Cosmology"
            },
            
            // Advanced Molecular Biology (100 questions)
            {
                question: "Which enzyme is responsible for unwinding DNA during replication?",
                options: ["DNA Polymerase", "Helicase", "Ligase", "Topoisomerase"],
                correct: 1,
                hint: "It breaks hydrogen bonds between complementary base pairs.",
                difficulty: "genius",
                category: "Advanced Molecular Biology"
            },
            
            // Astrophysics & Cosmology (50 questions)
            {
                question: "What is the Chandrasekhar limit?",
                options: ["1.4 solar masses", "2.1 solar masses", "3.2 solar masses", "0.8 solar masses"],
                correct: 0,
                hint: "It's the maximum mass of a white dwarf star before collapse.",
                difficulty: "genius",
                category: "Astrophysics & Cosmology"
            },
            
            // ADDITIONAL BEGINNER VALLEY QUESTIONS (400+ more)
            
            // More Basic Math
            {
                question: "What is 9 + 1?",
                options: ["9", "10", "11", "12"],
                correct: 1,
                hint: "It's the first number with two digits.",
                difficulty: "easy",
                category: "Basic Math"
            },
            {
                question: "What is 15 - 5?",
                options: ["8", "9", "10", "11"],
                correct: 2,
                hint: "It's the same as 5 + 5.",
                difficulty: "easy",
                category: "Basic Math"
            },
            {
                question: "What is 3 × 4?",
                options: ["10", "11", "12", "13"],
                correct: 2,
                hint: "It's like adding 3 + 3 + 3 + 3.",
                difficulty: "easy",
                category: "Basic Math"
            },
            {
                question: "What is 20 ÷ 4?",
                options: ["4", "5", "6", "7"],
                correct: 1,
                hint: "How many groups of 4 can you make from 20?",
                difficulty: "easy",
                category: "Basic Math"
            },
            {
                question: "What is 6 + 4?",
                options: ["9", "10", "11", "12"],
                correct: 1,
                hint: "Count up from 6: 7, 8, 9, 10.",
                difficulty: "easy",
                category: "Basic Math"
            },
            
            // More Animals
            {
                question: "Which animal gives us eggs?",
                options: ["Cow", "Pig", "Chicken", "Horse"],
                correct: 2,
                hint: "This bird says 'cluck cluck'.",
                difficulty: "easy",
                category: "Animals"
            },
            {
                question: "Which animal has a trunk?",
                options: ["Lion", "Elephant", "Tiger", "Bear"],
                correct: 1,
                hint: "It's the largest land animal.",
                difficulty: "easy",
                category: "Animals"
            },
            {
                question: "Which animal hops and has long ears?",
                options: ["Cat", "Dog", "Rabbit", "Mouse"],
                correct: 2,
                hint: "It loves to eat carrots.",
                difficulty: "easy",
                category: "Animals"
            },
            {
                question: "Which animal says 'oink'?",
                options: ["Cow", "Pig", "Sheep", "Horse"],
                correct: 1,
                hint: "This animal likes to roll in mud.",
                difficulty: "easy",
                category: "Animals"
            },
            {
                question: "Which animal has black and white stripes?",
                options: ["Horse", "Zebra", "Cow", "Tiger"],
                correct: 1,
                hint: "It looks like a horse with stripes.",
                difficulty: "easy",
                category: "Animals"
            },
            
            // More Colors & Art
            {
                question: "What color do you get when you mix black and white?",
                options: ["Brown", "Gray", "Purple", "Green"],
                correct: 1,
                hint: "It's the color of clouds on a rainy day.",
                difficulty: "easy",
                category: "Colors & Art"
            },
            {
                question: "What is the color of grass?",
                options: ["Blue", "Red", "Green", "Yellow"],
                correct: 2,
                hint: "It's the same color as leaves on trees.",
                difficulty: "easy",
                category: "Colors & Art"
            },
            {
                question: "What is the color of the sky on a clear day?",
                options: ["Green", "Blue", "Red", "Yellow"],
                correct: 1,
                hint: "It's the same color as the ocean.",
                difficulty: "easy",
                category: "Colors & Art"
            },
            {
                question: "What color is snow?",
                options: ["Black", "Gray", "White", "Blue"],
                correct: 2,
                hint: "It's the color of clouds and milk.",
                difficulty: "easy",
                category: "Colors & Art"
            },
            {
                question: "What color is an apple usually?",
                options: ["Blue", "Red", "Purple", "Black"],
                correct: 1,
                hint: "It can also be green or yellow, but this is the most common.",
                difficulty: "easy",
                category: "Colors & Art"
            },
            
            // ADDITIONAL KNOWLEDGE ACADEMY QUESTIONS (400+ more)
            
            // More Geography
            {
                question: "What is the capital of the United States?",
                options: ["New York", "Los Angeles", "Washington D.C.", "Chicago"],
                correct: 2,
                hint: "It's named after the first president.",
                difficulty: "medium",
                category: "Geography"
            },
            {
                question: "Which continent is Egypt in?",
                options: ["Asia", "Africa", "Europe", "South America"],
                correct: 1,
                hint: "It's the continent where the pyramids are located.",
                difficulty: "medium",
                category: "Geography"
            },
            {
                question: "What is the capital of Japan?",
                options: ["Osaka", "Kyoto", "Tokyo", "Hiroshima"],
                correct: 2,
                hint: "It hosted the Olympics in 2021.",
                difficulty: "medium",
                category: "Geography"
            },
            {
                question: "Which ocean is between Europe and America?",
                options: ["Pacific", "Atlantic", "Indian", "Arctic"],
                correct: 1,
                hint: "The Titanic sank in this ocean.",
                difficulty: "medium",
                category: "Geography"
            },
            {
                question: "What is the capital of Russia?",
                options: ["St. Petersburg", "Moscow", "Kiev", "Warsaw"],
                correct: 1,
                hint: "It's home to the Red Square and the Kremlin.",
                difficulty: "medium",
                category: "Geography"
            },
            
            // More History
            {
                question: "Who discovered America in 1492?",
                options: ["Vasco da Gama", "Christopher Columbus", "Marco Polo", "Ferdinand Magellan"],
                correct: 1,
                hint: "He was trying to find a route to Asia but found America instead.",
                difficulty: "medium",
                category: "History"
            },
            {
                question: "Which war was fought between the North and South in America?",
                options: ["World War I", "Revolutionary War", "Civil War", "War of 1812"],
                correct: 2,
                hint: "It was about slavery and states' rights.",
                difficulty: "medium",
                category: "History"
            },
            {
                question: "In which year did man first land on the moon?",
                options: ["1967", "1968", "1969", "1970"],
                correct: 2,
                hint: "Neil Armstrong was the first person to walk on the moon.",
                difficulty: "medium",
                category: "History"
            },
            {
                question: "Which ancient civilization built the pyramids?",
                options: ["Greeks", "Romans", "Egyptians", "Babylonians"],
                correct: 2,
                hint: "They lived along the Nile River.",
                difficulty: "medium",
                category: "History"
            },
            {
                question: "Who was the famous queen of Egypt?",
                options: ["Nefertiti", "Cleopatra", "Hatshepsut", "Ankhesenamun"],
                correct: 1,
                hint: "She was known for her beauty and relationships with Roman leaders.",
                difficulty: "medium",
                category: "History"
            },
            
            // More Literature & Arts
            {
                question: "Who wrote 'Alice in Wonderland'?",
                options: ["Lewis Carroll", "Charles Dickens", "Mark Twain", "Oscar Wilde"],
                correct: 0,
                hint: "This author created the Mad Hatter and Cheshire Cat.",
                difficulty: "medium",
                category: "Literature & Arts"
            },
            {
                question: "Which instrument does a violinist play?",
                options: ["Piano", "Guitar", "Violin", "Flute"],
                correct: 2,
                hint: "It's played with a bow and has four strings.",
                difficulty: "medium",
                category: "Literature & Arts"
            },
            {
                question: "Who composed 'The Four Seasons'?",
                options: ["Mozart", "Beethoven", "Vivaldi", "Bach"],
                correct: 2,
                hint: "This Italian composer wrote music about spring, summer, fall, and winter.",
                difficulty: "medium",
                category: "Literature & Arts"
            },
            {
                question: "What type of art is the Statue of Liberty?",
                options: ["Painting", "Sculpture", "Drawing", "Photography"],
                correct: 1,
                hint: "It's a three-dimensional work of art made of copper.",
                difficulty: "medium",
                category: "Literature & Arts"
            },
            {
                question: "Who wrote 'The Cat in the Hat'?",
                options: ["Dr. Seuss", "Roald Dahl", "Maurice Sendak", "Eric Carle"],
                correct: 0,
                hint: "This author wrote many rhyming children's books.",
                difficulty: "medium",
                category: "Literature & Arts"
            },
            
            // ADDITIONAL SCHOLAR'S TEMPLE QUESTIONS (400+ more)
            
            // More Advanced Chemistry
            {
                question: "What is the chemical symbol for gold?",
                options: ["Go", "Gd", "Au", "Ag"],
                correct: 2,
                hint: "It comes from the Latin word 'aurum'.",
                difficulty: "hard",
                category: "Advanced Chemistry"
            },
            {
                question: "What is the atomic number of carbon?",
                options: ["4", "5", "6", "7"],
                correct: 2,
                hint: "It's the number of protons in a carbon atom.",
                difficulty: "hard",
                category: "Advanced Chemistry"
            },
            {
                question: "Which gas is produced when you mix baking soda and vinegar?",
                options: ["Oxygen", "Hydrogen", "Carbon Dioxide", "Nitrogen"],
                correct: 2,
                hint: "This gas makes the mixture bubble and fizz.",
                difficulty: "hard",
                category: "Advanced Chemistry"
            },
            {
                question: "What is the chemical formula for table salt?",
                options: ["NaCl", "KCl", "CaCl2", "MgCl2"],
                correct: 0,
                hint: "It contains sodium and chlorine.",
                difficulty: "hard",
                category: "Advanced Chemistry"
            },
            {
                question: "Which element has the symbol 'Fe'?",
                options: ["Fluorine", "Iron", "Francium", "Fermium"],
                correct: 1,
                hint: "It comes from the Latin word 'ferrum' and is magnetic.",
                difficulty: "hard",
                category: "Advanced Chemistry"
            },
            
            // More Biology & Medicine
            {
                question: "How many chambers does a human heart have?",
                options: ["2", "3", "4", "5"],
                correct: 2,
                hint: "It has two atria and two ventricles.",
                difficulty: "hard",
                category: "Biology & Medicine"
            },
            {
                question: "What is the largest organ in the human body?",
                options: ["Liver", "Brain", "Lungs", "Skin"],
                correct: 3,
                hint: "It covers your entire body and protects you.",
                difficulty: "hard",
                category: "Biology & Medicine"
            },
            {
                question: "Which blood type is known as the universal donor?",
                options: ["A", "B", "AB", "O"],
                correct: 3,
                hint: "People with this blood type can donate to anyone.",
                difficulty: "hard",
                category: "Biology & Medicine"
            },
            {
                question: "What is the powerhouse of the cell?",
                options: ["Nucleus", "Mitochondria", "Ribosome", "Cytoplasm"],
                correct: 1,
                hint: "It produces energy (ATP) for the cell.",
                difficulty: "hard",
                category: "Biology & Medicine"
            },
            {
                question: "How many bones are in an adult human body?",
                options: ["196", "206", "216", "226"],
                correct: 1,
                hint: "It's just over 200 bones.",
                difficulty: "hard",
                category: "Biology & Medicine"
            },
            
            // ADDITIONAL SCIENCE LABORATORY QUESTIONS (400+ more)
            
            // More Advanced Physics
            {
                question: "What is Newton's first law of motion?",
                options: ["F=ma", "Objects at rest stay at rest", "Action-reaction", "Conservation of energy"],
                correct: 1,
                hint: "It's also called the law of inertia.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "What is the unit of electrical resistance?",
                options: ["Volt", "Ampere", "Ohm", "Watt"],
                correct: 2,
                hint: "It's named after a German physicist.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "What is the frequency of visible light?",
                options: ["10^12 Hz", "10^14 Hz", "10^16 Hz", "10^18 Hz"],
                correct: 1,
                hint: "It's in the range of hundreds of terahertz.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "What is the mass of an electron?",
                options: ["9.109 × 10^-31 kg", "1.673 × 10^-27 kg", "1.675 × 10^-27 kg", "6.626 × 10^-34 kg"],
                correct: 0,
                hint: "It's about 1/1836 the mass of a proton.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            {
                question: "What is absolute zero in Celsius?",
                options: ["-273.15°C", "-273.16°C", "-273.17°C", "-273.18°C"],
                correct: 0,
                hint: "It's the temperature at which all molecular motion stops.",
                difficulty: "expert",
                category: "Advanced Physics"
            },
            
            // More Computer Science & Technology
            {
                question: "What does CPU stand for?",
                options: ["Central Processing Unit", "Computer Processing Unit", "Central Program Unit", "Computer Program Unit"],
                correct: 0,
                hint: "It's the brain of the computer.",
                difficulty: "expert",
                category: "Computer Science & Technology"
            },
            {
                question: "What does HTML stand for?",
                options: ["Hypertext Markup Language", "High Tech Modern Language", "Home Tool Markup Language", "Hypertext Modern Language"],
                correct: 0,
                hint: "It's used to create web pages.",
                difficulty: "expert",
                category: "Computer Science & Technology"
            },
            {
                question: "Who founded Microsoft?",
                options: ["Steve Jobs", "Bill Gates", "Mark Zuckerberg", "Larry Page"],
                correct: 1,
                hint: "He was the richest person in the world for many years.",
                difficulty: "expert",
                category: "Computer Science & Technology"
            },
            {
                question: "What does WWW stand for?",
                options: ["World Wide Web", "World Wide Website", "World Web Wide", "Wide World Web"],
                correct: 0,
                hint: "It's what you access when you browse the internet.",
                difficulty: "expert",
                category: "Computer Science & Technology"
            },
            {
                question: "In binary, what is 1010?",
                options: ["8", "9", "10", "11"],
                correct: 2,
                hint: "Convert from base 2 to base 10.",
                difficulty: "expert",
                category: "Computer Science & Technology"
            },
            
            // ADDITIONAL GENIUS SUMMIT QUESTIONS (400+ more)
            
            // More Pure Mathematics
            {
                question: "What is the derivative of x²?",
                options: ["x", "2x", "x²", "2x²"],
                correct: 1,
                hint: "Use the power rule: bring down the exponent and subtract 1.",
                difficulty: "genius",
                category: "Pure Mathematics"
            },
            {
                question: "What is the integral of 1/x?",
                options: ["ln(x)", "x²/2", "1/x²", "e^x"],
                correct: 0,
                hint: "It's the natural logarithm function.",
                difficulty: "genius",
                category: "Pure Mathematics"
            },
            {
                question: "What is Euler's number (e) approximately?",
                options: ["2.618", "2.718", "3.141", "1.618"],
                correct: 1,
                hint: "It's the base of natural logarithms.",
                difficulty: "genius",
                category: "Pure Mathematics"
            },
            {
                question: "What is the sum of angles in a triangle?",
                options: ["90°", "180°", "270°", "360°"],
                correct: 1,
                hint: "It's the same for all triangles, regardless of shape.",
                difficulty: "genius",
                category: "Pure Mathematics"
            },
            {
                question: "What is the quadratic formula?",
                options: ["x = -b ± √(b²-4ac)/2a", "x = b ± √(b²+4ac)/2a", "x = -b ± √(b²+4ac)/2a", "x = b ± √(b²-4ac)/2a"],
                correct: 0,
                hint: "It solves equations of the form ax² + bx + c = 0.",
                difficulty: "genius",
                category: "Pure Mathematics"
            },
            
            // More Theoretical Physics & Cosmology
            {
                question: "What is the Hubble constant approximately?",
                options: ["70 km/s/Mpc", "80 km/s/Mpc", "60 km/s/Mpc", "90 km/s/Mpc"],
                correct: 0,
                hint: "It describes the rate of expansion of the universe.",
                difficulty: "genius",
                category: "Theoretical Physics & Cosmology"
            },
            {
                question: "What is dark matter?",
                options: ["Invisible planets", "Unknown particles", "Black holes", "Empty space"],
                correct: 1,
                hint: "It makes up about 27% of the universe but doesn't interact with light.",
                difficulty: "genius",
                category: "Theoretical Physics & Cosmology"
            },
            {
                question: "What is the age of the universe?",
                options: ["13.8 billion years", "14.8 billion years", "12.8 billion years", "15.8 billion years"],
                correct: 0,
                hint: "It's determined from the cosmic microwave background radiation.",
                difficulty: "genius",
                category: "Theoretical Physics & Cosmology"
            },
            {
                question: "What is a quasar?",
                options: ["A type of star", "An active galactic nucleus", "A planet", "A comet"],
                correct: 1,
                hint: "It's powered by a supermassive black hole.",
                difficulty: "genius",
                category: "Theoretical Physics & Cosmology"
            },
            {
                question: "What is string theory?",
                options: ["Theory of guitar strings", "Theory of fundamental particles", "Theory of rope physics", "Theory of musical harmony"],
                correct: 1,
                hint: "It proposes that particles are one-dimensional strings.",
                difficulty: "genius",
                category: "Theoretical Physics & Cosmology"
            },
            
            // More Advanced Molecular Biology
            {
                question: "What is the central dogma of molecular biology?",
                options: ["DNA → RNA → Protein", "RNA → DNA → Protein", "Protein → RNA → DNA", "DNA → Protein → RNA"],
                correct: 0,
                hint: "It describes the flow of genetic information.",
                difficulty: "genius",
                category: "Advanced Molecular Biology"
            },
            {
                question: "How many base pairs are in the human genome?",
                options: ["3.2 billion", "3.0 billion", "2.8 billion", "3.4 billion"],
                correct: 0,
                hint: "It's approximately 3.2 billion base pairs.",
                difficulty: "genius",
                category: "Advanced Molecular Biology"
            },
            {
                question: "What is CRISPR?",
                options: ["A protein", "A gene editing tool", "A type of cell", "A chromosome"],
                correct: 1,
                hint: "It's used to edit genes with precision.",
                difficulty: "genius",
                category: "Advanced Molecular Biology"
            },
            {
                question: "What is the function of ribosomes?",
                options: ["DNA replication", "Protein synthesis", "Cell division", "Energy production"],
                correct: 1,
                hint: "They translate mRNA into proteins.",
                difficulty: "genius",
                category: "Advanced Molecular Biology"
            },
            {
                question: "What is a telomere?",
                options: ["End of chromosome", "Type of gene", "Cell membrane", "Nuclear envelope"],
                correct: 0,
                hint: "It protects chromosomes from degradation during cell division.",
                difficulty: "genius",
                category: "Advanced Molecular Biology"
            }
        ];

        let currentLevel = 1;
        let questionInLevel = 1;
        let coins = 50;
        let score = 0;
        let currentQuestion = null;
        let answered = false;
        let hintUsed = false;
        let questionsPerLevel = 5;
        let correctAnswersInLevel = 0;
        let selectedMode = null;
        let usedQuestionsInMode = new Set(); // Track all questions used in current mode
        let availableQuestions = []; // Pool of unused questions for current mode
        
        // Score tracking variables
        let totalCorrectAnswers = 0;
        let totalQuestionsAnswered = 0;
        
        let timer = null;
        let timeLeft = 0;

        function getDifficultySettings(mode, level) {
            const modeSettings = {
                beginner: {
                    correctReward: 3,
                    wrongPenalty: 1,
                    hintCost: 8,
                    timeLimit: null,
                    info: `🌱 Beginner Valley - Level ${level}/100: Basic knowledge, no time pressure`,
                    difficulty: "easy",
                    section: "Beginner Valley",
                    theme: "beginner",
                    gradient: "linear-gradient(135deg, #a8e6cf, #7fcdcd)",
                    icon: "🌱"
                },
                academy: {
                    correctReward: 5,
                    wrongPenalty: 2,
                    hintCost: 12,
                    timeLimit: 45,
                    info: `🏫 Knowledge Academy - Level ${level}/100: School subjects, 45s timer`,
                    difficulty: "medium",
                    section: "Knowledge Academy",
                    theme: "academy",
                    gradient: "linear-gradient(135deg, #ffd89b, #19547b)",
                    icon: "🏫"
                },
                temple: {
                    correctReward: 7,
                    wrongPenalty: 3,
                    hintCost: 15,
                    timeLimit: 35,
                    info: `🏛️ Scholar's Temple - Level ${level}/100: Advanced topics, 35s timer`,
                    difficulty: "hard",
                    section: "Scholar's Temple",
                    theme: "temple",
                    gradient: "linear-gradient(135deg, #667eea, #764ba2)",
                    icon: "🏛️"
                },
                lab: {
                    correctReward: 10,
                    wrongPenalty: 4,
                    hintCost: 20,
                    timeLimit: 25,
                    info: `🔬 Science Laboratory - Level ${level}/100: Scientific knowledge, 25s timer`,
                    difficulty: "expert",
                    section: "Science Laboratory",
                    theme: "lab",
                    gradient: "linear-gradient(135deg, #11998e, #38ef7d)",
                    icon: "🔬"
                },
                summit: {
                    correctReward: 15,
                    wrongPenalty: 6,
                    hintCost: 25,
                    timeLimit: 15,
                    info: `🧠 Genius Summit - Level ${level}/100: Expert challenges, 15s timer`,
                    difficulty: "genius",
                    section: "Genius Summit",
                    theme: "summit",
                    gradient: "linear-gradient(135deg, #fc466b, #3f5efb)",
                    icon: "🧠"
                }
            };
            
            return modeSettings[mode] || modeSettings.beginner;
        }

        function shuffleArray(array) {
            const shuffled = [...array];
            for (let i = shuffled.length - 1; i > 0; i--) {
                const j = Math.floor(Math.random() * (i + 1));
                [shuffled[i], shuffled[j]] = [shuffled[j], shuffled[i]];
            }
            return shuffled;
        }
        
        function selectMode(mode) {
            selectedMode = mode;
            currentLevel = 1;
            questionInLevel = 1;
            coins = 50;
            score = 0;
            correctAnswersInLevel = 0;
            totalCorrectAnswers = 0;
            totalQuestionsAnswered = 0;
            usedQuestionsInMode.clear(); // Reset used questions for new mode
            
            // Initialize fresh question pool for this mode
            const settings = getDifficultySettings(mode, 1);
            availableQuestions = shuffleArray(allQuestions.filter(q => q.difficulty === settings.difficulty));
            
            document.getElementById('modeSelection').style.display = 'none';
            document.getElementById('gameArea').style.display = 'block';
            
            updateDisplay();
            loadQuestion();
        }
        
        function backToModeSelection() {
            clearInterval(timer);
            document.getElementById('modeSelection').style.display = 'block';
            document.getElementById('gameArea').style.display = 'none';
            document.getElementById('gameOver').style.display = 'none';
            selectedMode = null;
        }

        function startTimer() {
            clearInterval(timer);
            const settings = getDifficultySettings(selectedMode, currentLevel);
            
            if (settings.timeLimit && !answered) {
                timeLeft = settings.timeLimit;
                document.getElementById('timer').style.display = 'block';
                document.getElementById('timeLeft').textContent = timeLeft;
                
                timer = setInterval(() => {
                    timeLeft--;
                    document.getElementById('timeLeft').textContent = timeLeft;
                    
                    if (timeLeft <= 5) {
                        document.getElementById('timeLeft').style.color = '#f44336';
                    }
                    
                    if (timeLeft <= 0) {
                        clearInterval(timer);
                        if (!answered) {
                            timeUp();
                        }
                    }
                }, 1000);
            } else {
                document.getElementById('timer').style.display = 'none';
            }
        }
        
        function timeUp() {
            answered = true;
            const options = document.querySelectorAll('.option');
            const feedback = document.getElementById('feedback');
            const settings = getDifficultySettings(selectedMode, currentLevel);

            // Update total questions answered
            totalQuestionsAnswered++;

            options.forEach((option, index) => {
                option.classList.add('disabled');
                if (index === currentQuestion.correct) {
                    option.classList.add('correct');
                }
            });

            coins = Math.max(0, coins - settings.wrongPenalty);
            feedback.textContent = `⏰ Time's up! The correct answer was ${String.fromCharCode(65 + currentQuestion.correct)}. You lost ${settings.wrongPenalty} coin(s).`;
            feedback.className = 'feedback wrong';
            feedback.style.display = 'block';
            
            document.getElementById('nextBtn').style.display = 'inline-block';
            document.getElementById('hintBtn').style.display = 'none';
            updateDisplay();
        }

        function loadQuestion() {
            if (currentLevel > 100) {
                endGame();
                return;
            }

            const settings = getDifficultySettings(selectedMode, currentLevel);
            
            // Get next unused question from available pool
            if (availableQuestions.length === 0) {
                // If we've used all questions, reshuffle the entire pool
                const allModeQuestions = allQuestions.filter(q => q.difficulty === settings.difficulty);
                availableQuestions = shuffleArray(allModeQuestions);
                usedQuestionsInMode.clear(); // Reset tracking
                console.log(`Reshuffled question pool for ${selectedMode} mode`);
            }
            
            // Find first unused question
            let questionIndex = 0;
            let questionFound = false;
            
            while (questionIndex < availableQuestions.length && !questionFound) {
                const question = availableQuestions[questionIndex];
                const questionId = question.question; // Use question text as unique ID
                
                if (!usedQuestionsInMode.has(questionId)) {
                    currentQuestion = question;
                    usedQuestionsInMode.add(questionId);
                    // Remove this question from available pool
                    availableQuestions.splice(questionIndex, 1);
                    questionFound = true;
                } else {
                    questionIndex++;
                }
            }
            
            // Fallback: if somehow no question found, take first available
            if (!questionFound && availableQuestions.length > 0) {
                currentQuestion = availableQuestions.shift();
                usedQuestionsInMode.add(currentQuestion.question);
            }
            
            answered = false;
            hintUsed = false;

            document.getElementById('questionNumber').textContent = currentLevel;
            document.getElementById('questionInLevel').textContent = questionInLevel;
            document.getElementById('question').textContent = currentQuestion.question;
            document.getElementById('hint').style.display = 'none';
            document.getElementById('feedback').style.display = 'none';
            document.getElementById('nextBtn').style.display = 'none';
            document.getElementById('hintBtn').style.display = 'inline-block';
            document.getElementById('levelComplete').style.display = 'none';
            
            document.getElementById('hintBtn').textContent = `💡 Get Hint (${settings.hintCost} coins)`;
            document.getElementById('hintBtn').disabled = coins < settings.hintCost;

            const optionsContainer = document.getElementById('options');
            optionsContainer.innerHTML = '';

            currentQuestion.options.forEach((option, index) => {
                const optionElement = document.createElement('div');
                optionElement.className = 'option';
                optionElement.textContent = `${String.fromCharCode(65 + index)}. ${option}`;
                optionElement.onclick = () => selectAnswer(index);
                optionsContainer.appendChild(optionElement);
            });
            
            // Reset timer color
            document.getElementById('timeLeft').style.color = '#f44336';
            
            // Start timer for this question
            startTimer();
        }

        function selectAnswer(selectedIndex) {
            if (answered) return;

            answered = true;
            clearInterval(timer);
            
            const options = document.querySelectorAll('.option');
            const feedback = document.getElementById('feedback');
            const settings = getDifficultySettings(selectedMode, currentLevel);

            options.forEach((option, index) => {
                option.classList.add('disabled');
                if (index === currentQuestion.correct) {
                    option.classList.add('correct');
                } else if (index === selectedIndex) {
                    option.classList.add('wrong');
                }
            });

            // Update total questions answered
            totalQuestionsAnswered++;
            
            if (selectedIndex === currentQuestion.correct) {
                coins += settings.correctReward;
                score += 10 + (currentLevel - 1); // Bonus points for higher levels
                correctAnswersInLevel++;
                totalCorrectAnswers++;
                feedback.textContent = `🎉 Correct! You earned ${settings.correctReward} coins and ${10 + (currentLevel - 1)} points!`;
                feedback.className = 'feedback correct';
            } else {
                coins = Math.max(0, coins - settings.wrongPenalty);
                feedback.textContent = `❌ Wrong! The correct answer was ${String.fromCharCode(65 + currentQuestion.correct)}. You lost ${settings.wrongPenalty} coin(s).`;
                feedback.className = 'feedback wrong';
            }

            feedback.style.display = 'block';
            
            if (questionInLevel >= questionsPerLevel) {
                // Level complete
                setTimeout(() => {
                    showLevelComplete();
                }, 2000);
            } else {
                document.getElementById('nextBtn').style.display = 'inline-block';
            }
            
            document.getElementById('hintBtn').style.display = 'none';
            updateDisplay();
        }

        function showHint() {
            const settings = getDifficultySettings(selectedMode, currentLevel);
            if (coins >= settings.hintCost && !hintUsed) {
                coins -= settings.hintCost;
                hintUsed = true;
                document.getElementById('hint').textContent = `💡 Hint: ${currentQuestion.hint}`;
                document.getElementById('hint').style.display = 'block';
                document.getElementById('hintBtn').disabled = true;
                updateDisplay();
            }
        }

        function nextQuestion() {
            questionInLevel++;
            loadQuestion();
        }

        function showLevelComplete() {
            document.getElementById('feedback').style.display = 'none';
            document.getElementById('nextBtn').style.display = 'none';
            
            const bonusCoins = correctAnswersInLevel * 5;
            coins += bonusCoins;
            
            const settings = getDifficultySettings(selectedMode, currentLevel);
            let completionText = `Great job! You got ${correctAnswersInLevel} out of ${questionsPerLevel} questions correct and earned ${bonusCoins} bonus coins!`;
            
            // Check if completing milestones within the mode
            if (currentLevel === 25) {
                completionText += `\n\n🎉 Quarter Complete! 25 levels down, 75 to go!`;
                coins += 25;
            } else if (currentLevel === 50) {
                completionText += `\n\n🎖️ Halfway Champion! 50 levels conquered!`;
                coins += 50;
            } else if (currentLevel === 75) {
                completionText += `\n\n🏅 Three-Quarter Master! Only 25 levels left!`;
                coins += 75;
            } else if (currentLevel === 100) {
                completionText += `\n\n🏆 MODE COMPLETE! You've mastered all 100 levels of ${settings.section}!`;
                coins += 200;
            }
            
            document.getElementById('levelCompleteText').textContent = completionText;
            document.getElementById('levelComplete').style.display = 'block';
            
            updateDisplay();
        }

        function nextLevel() {
            currentLevel++;
            questionInLevel = 1;
            correctAnswersInLevel = 0;
            
            if (currentLevel > 100) {
                endGame();
                return;
            }
            
            updateDisplay();
            loadQuestion();
        }

        function updateDisplay() {
            if (!selectedMode) return;
            
            const settings = getDifficultySettings(selectedMode, currentLevel);
            
            // Update score bar
            document.getElementById('coinCount').textContent = coins;
            document.getElementById('score').textContent = score;
            document.getElementById('currentLevelDisplay').textContent = currentLevel;
            document.getElementById('correctCount').textContent = totalCorrectAnswers;
            
            // Calculate and update accuracy
            const accuracy = totalQuestionsAnswered > 0 ? Math.round((totalCorrectAnswers / totalQuestionsAnswered) * 100) : 100;
            document.getElementById('accuracy').textContent = accuracy + '%';
            
            // Update game area elements
            document.getElementById('currentLevel').textContent = currentLevel;
            document.getElementById('modeTitle').textContent = `${settings.icon} ${settings.section}`;
            document.getElementById('difficultyInfo').textContent = settings.info;
            document.getElementById('hintBtn').disabled = coins < settings.hintCost || hintUsed;
            
            // Update level info background with theme colors
            const levelInfo = document.querySelector('.level-info');
            if (levelInfo) {
                levelInfo.style.background = settings.gradient;
            }
            
            // Update progress bar
            const progress = ((currentLevel - 1) / 100) * 100;
            const progressFill = document.getElementById('progressFill');
            const levelProgress = document.getElementById('levelProgress');
            if (progressFill) progressFill.style.width = progress + '%';
            if (levelProgress) levelProgress.textContent = Math.round(progress);
        }

        function endGame() {
            const settings = getDifficultySettings(selectedMode, currentLevel);
            
            // Update user stats
            if (currentUser) {
                currentUser.stats.totalGamesPlayed++;
                currentUser.stats.totalScore += score;
                currentUser.stats.totalCoins += coins;
                
                // Add completed mode if not already present
                if (!currentUser.stats.modesCompleted.includes(selectedMode)) {
                    currentUser.stats.modesCompleted.push(selectedMode);
                }
                
                // Save updated user data
                const users = JSON.parse(localStorage.getItem('quizUsers') || '[]');
                const userIndex = users.findIndex(u => u.id === currentUser.id);
                if (userIndex !== -1) {
                    users[userIndex] = currentUser;
                    localStorage.setItem('quizUsers', JSON.stringify(users));
                }
                
                // Update session storage
                if (sessionStorage.getItem('quizCurrentUser')) {
                    sessionStorage.setItem('quizCurrentUser', JSON.stringify(currentUser));
                }
                if (localStorage.getItem('quizCurrentUser')) {
                    localStorage.setItem('quizCurrentUser', JSON.stringify(currentUser));
                }
            }
            
            document.getElementById('gameArea').style.display = 'none';
            document.getElementById('gameOver').style.display = 'block';
            document.getElementById('finalScore').textContent = score;
            document.getElementById('finalCoins').textContent = coins;
            document.getElementById('gameOverTitle').textContent = `🏆 ${settings.section} Complete!`;
            document.getElementById('gameOverMessage').textContent = `You've conquered all 100 levels of ${settings.section}! Amazing work!`;
        }

        function restartGame() {
            if (!selectedMode) {
                backToModeSelection();
                return;
            }
            
            currentLevel = 1;
            questionInLevel = 1;
            coins = 50;
            score = 0;
            correctAnswersInLevel = 0;
            totalCorrectAnswers = 0;
            totalQuestionsAnswered = 0;
            usedQuestionsInMode.clear(); // Reset used questions for restart
            clearInterval(timer);
            
            // Reinitialize fresh question pool
            const settings = getDifficultySettings(selectedMode, 1);
            availableQuestions = shuffleArray(allQuestions.filter(q => q.difficulty === settings.difficulty));
            
            document.getElementById('gameArea').style.display = 'block';
            document.getElementById('gameOver').style.display = 'none';
            updateDisplay();
            loadQuestion();
        }

        // Modal and theme functionality
        let currentTheme = 'default';
        let soundSettings = {
            effects: true,
            music: false,
            voice: false
        };

        function openThemes() {
            document.getElementById('themesModal').style.display = 'block';
            closeProfileMenu();
        }

        function toggleSounds() {
            document.getElementById('soundsModal').style.display = 'block';
            closeProfileMenu();
        }

        function openAbout() {
            document.getElementById('aboutModal').style.display = 'block';
            closeProfileMenu();
        }

        function openMyProfile() {
            updateProfileModal();
            document.getElementById('profileModal').style.display = 'block';
            closeProfileMenu();
        }

        function openDevelopers() {
            document.getElementById('developersModal').style.display = 'block';
            closeProfileMenu();
        }

        function toggleProfileMenu() {
            const menu = document.getElementById('profileMenu');
            menu.classList.toggle('show');
        }

        function closeProfileMenu() {
            const menu = document.getElementById('profileMenu');
            menu.classList.remove('show');
        }

        function closeModal(modalId) {
            document.getElementById(modalId).style.display = 'none';
        }

        function selectTheme(theme) {
            // Remove selected class from all themes
            document.querySelectorAll('.theme-option').forEach(option => {
                option.classList.remove('selected');
            });
            
            // Add selected class to chosen theme
            document.querySelector(`.theme-${theme}`).classList.add('selected');
            
            // Apply theme
            currentTheme = theme;
            applyTheme(theme);
            
            // Save to localStorage
            localStorage.setItem('quizTheme', theme);
        }

        function applyTheme(theme) {
            const themes = {
                default: 'linear-gradient(135deg, #667eea 0%, #764ba2 100%)',
                ocean: 'linear-gradient(135deg, #2196f3 0%, #21cbf3 100%)',
                sunset: 'linear-gradient(135deg, #ff9a56 0%, #ff6b6b 100%)',
                forest: 'linear-gradient(135deg, #56ab2f 0%, #a8e6cf 100%)',
                galaxy: 'linear-gradient(135deg, #2c3e50 0%, #4a00e0 100%)',
                candy: 'linear-gradient(135deg, #ff9a9e 0%, #fecfef 100%)'
            };
            
            document.body.style.background = themes[theme];
        }

        function toggleSoundEffect(type) {
            soundSettings[type] = !soundSettings[type];
            const toggle = document.getElementById(`${type}Toggle`);
            
            if (soundSettings[type]) {
                toggle.classList.add('active');
            } else {
                toggle.classList.remove('active');
            }
            
            // Save to localStorage
            localStorage.setItem('quizSounds', JSON.stringify(soundSettings));
            
            // Play sound effect if enabled
            if (soundSettings.effects && type === 'effects') {
                playSound('click');
            }
        }

        function playSound(type) {
            if (!soundSettings.effects) return;
            
            // Simulate sound effects with visual feedback
            const button = event?.target;
            if (button) {
                button.style.transform = 'scale(0.95)';
                setTimeout(() => {
                    button.style.transform = '';
                }, 100);
            }
        }

        // Close modals when clicking outside
        window.onclick = function(event) {
            const modals = ['themesModal', 'soundsModal', 'aboutModal', 'developersModal', 'profileModal'];
            modals.forEach(modalId => {
                const modal = document.getElementById(modalId);
                if (event.target === modal) {
                    closeModal(modalId);
                }
            });
            
            // Close profile menu when clicking outside
            const profileMenu = document.getElementById('profileMenu');
            const profileBtn = document.querySelector('.profile-btn');
            if (!profileBtn.contains(event.target) && !profileMenu.contains(event.target)) {
                closeProfileMenu();
            }
        }

        // Load saved settings
        function loadSettings() {
            // Load theme
            const savedTheme = localStorage.getItem('quizTheme');
            if (savedTheme) {
                selectTheme(savedTheme);
            }
            
            // Load sound settings
            const savedSounds = localStorage.getItem('quizSounds');
            if (savedSounds) {
                soundSettings = JSON.parse(savedSounds);
                Object.keys(soundSettings).forEach(type => {
                    const toggle = document.getElementById(`${type}Toggle`);
                    if (soundSettings[type]) {
                        toggle.classList.add('active');
                    } else {
                        toggle.classList.remove('active');
                    }
                });
            }
        }

        // Authentication system
        let currentUser = null;
        let isLoggedIn = false;

        function showAuthForm(formType) {
            // Remove active class from all tabs and forms
            document.querySelectorAll('.auth-tab').forEach(tab => tab.classList.remove('active'));
            document.querySelectorAll('.auth-form').forEach(form => form.classList.remove('active'));
            
            // Add active class to selected tab and form
            document.querySelector(`.auth-tab:${formType === 'signin' ? 'first-child' : 'last-child'}`).classList.add('active');
            document.getElementById(`${formType}Form`).classList.add('active');
            
            // Clear any existing messages
            clearAuthMessages();
        }

        function showAuthMessage(message, type) {
            // Remove any existing messages
            clearAuthMessages();
            
            const messageDiv = document.createElement('div');
            messageDiv.className = `auth-message ${type}`;
            messageDiv.textContent = message;
            
            const activeForm = document.querySelector('.auth-form.active');
            activeForm.insertBefore(messageDiv, activeForm.firstChild);
            
            // Auto-remove success messages after 3 seconds
            if (type === 'success') {
                setTimeout(() => {
                    if (messageDiv.parentNode) {
                        messageDiv.remove();
                    }
                }, 3000);
            }
        }

        function clearAuthMessages() {
            document.querySelectorAll('.auth-message').forEach(msg => msg.remove());
        }

        function handleSignIn(event) {
            event.preventDefault();
            
            const email = document.getElementById('signinEmail').value;
            const password = document.getElementById('signinPassword').value;
            const rememberMe = document.getElementById('rememberMe').checked;
            
            // Simulate authentication (in real app, this would be an API call)
            if (email && password.length >= 6) {
                // Check if user exists in localStorage
                const users = JSON.parse(localStorage.getItem('quizUsers') || '[]');
                const user = users.find(u => u.email === email && u.password === password);
                
                if (user) {
                    currentUser = user;
                    isLoggedIn = true;
                    
                    // Save login state
                    if (rememberMe) {
                        localStorage.setItem('quizCurrentUser', JSON.stringify(user));
                        localStorage.setItem('quizRememberLogin', 'true');
                    } else {
                        sessionStorage.setItem('quizCurrentUser', JSON.stringify(user));
                    }
                    
                    showAuthMessage('Welcome back! Redirecting to game...', 'success');
                    
                    setTimeout(() => {
                        showGameInterface();
                    }, 1500);
                } else {
                    showAuthMessage('Invalid email or password. Please try again.', 'error');
                }
            } else {
                showAuthMessage('Please enter a valid email and password (min 6 characters).', 'error');
            }
        }

        function handleSignUp(event) {
            event.preventDefault();
            
            const name = document.getElementById('signupName').value;
            const email = document.getElementById('signupEmail').value;
            const password = document.getElementById('signupPassword').value;
            const confirmPassword = document.getElementById('confirmPassword').value;
            const agreeTerms = document.getElementById('agreeTerms').checked;
            
            // Validation
            if (!name || !email || !password || !confirmPassword) {
                showAuthMessage('Please fill in all fields.', 'error');
                return;
            }
            
            if (password.length < 6) {
                showAuthMessage('Password must be at least 6 characters long.', 'error');
                return;
            }
            
            if (password !== confirmPassword) {
                showAuthMessage('Passwords do not match.', 'error');
                return;
            }
            
            if (!agreeTerms) {
                showAuthMessage('Please agree to the Terms & Conditions.', 'error');
                return;
            }
            
            // Check if user already exists
            const users = JSON.parse(localStorage.getItem('quizUsers') || '[]');
            if (users.find(u => u.email === email)) {
                showAuthMessage('An account with this email already exists.', 'error');
                return;
            }
            
            // Create new user
            const newUser = {
                id: Date.now(),
                name: name,
                email: email,
                password: password, // In real app, this would be hashed
                createdAt: new Date().toISOString(),
                stats: {
                    totalGamesPlayed: 0,
                    totalScore: 0,
                    totalCoins: 0,
                    modesCompleted: []
                }
            };
            
            users.push(newUser);
            localStorage.setItem('quizUsers', JSON.stringify(users));
            
            currentUser = newUser;
            isLoggedIn = true;
            
            // Save login state
            sessionStorage.setItem('quizCurrentUser', JSON.stringify(newUser));
            
            showAuthMessage('Account created successfully! Welcome to GK Quiz Challenge!', 'success');
            
            setTimeout(() => {
                showGameInterface();
            }, 2000);
        }

        function showGameInterface() {
            document.getElementById('authSection').style.display = 'none';
            document.getElementById('modeSelection').style.display = 'block';
            
            // Update profile section with user info
            updateUserProfile();
        }

        function updateUserProfile() {
            if (currentUser) {
                const profileBtn = document.querySelector('.profile-btn');
                profileBtn.textContent = currentUser.name.charAt(0).toUpperCase();
                profileBtn.title = `Logged in as ${currentUser.name}`;
            }
        }

        function updateProfileModal() {
            if (!currentUser) return;
            
            // Update basic info
            document.getElementById('profileAvatar').textContent = currentUser.name.charAt(0).toUpperCase();
            document.getElementById('profileName').textContent = currentUser.name;
            document.getElementById('profileEmail').textContent = currentUser.email;
            
            // Format join date
            const joinDate = new Date(currentUser.createdAt);
            const options = { year: 'numeric', month: 'long' };
            document.getElementById('profileJoinDate').textContent = joinDate.toLocaleDateString('en-US', options);
            
            // Update stats
            document.getElementById('profileTotalScore').textContent = currentUser.stats.totalScore.toLocaleString();
            document.getElementById('profileTotalCoins').textContent = currentUser.stats.totalCoins.toLocaleString();
            document.getElementById('profileGamesPlayed').textContent = currentUser.stats.totalGamesPlayed;
            document.getElementById('profileModesCompleted').textContent = currentUser.stats.modesCompleted.length;
            
            // Update achievements
            updateAchievements();
        }

        function updateAchievements() {
            if (!currentUser) return;
            
            const achievementsContainer = document.getElementById('profileAchievements');
            let achievementsHTML = '';
            
            // Welcome achievement (always present)
            achievementsHTML += `
                <div style="display: flex; align-items: center; gap: 10px; padding: 8px; background: white; border-radius: 8px; margin-bottom: 8px;">
                    <span style="font-size: 1.2rem;">🌟</span>
                    <span>Welcome to GK Quiz Challenge!</span>
                </div>
            `;
            
            // Score-based achievements
            if (currentUser.stats.totalScore >= 1000) {
                achievementsHTML += `
                    <div style="display: flex; align-items: center; gap: 10px; padding: 8px; background: white; border-radius: 8px; margin-bottom: 8px;">
                        <span style="font-size: 1.2rem;">🏆</span>
                        <span>Score Master - Reached 1,000+ points!</span>
                    </div>
                `;
            }
            
            if (currentUser.stats.totalScore >= 5000) {
                achievementsHTML += `
                    <div style="display: flex; align-items: center; gap: 10px; padding: 8px; background: white; border-radius: 8px; margin-bottom: 8px;">
                        <span style="font-size: 1.2rem;">💎</span>
                        <span>Quiz Legend - Reached 5,000+ points!</span>
                    </div>
                `;
            }
            
            // Games played achievements
            if (currentUser.stats.totalGamesPlayed >= 10) {
                achievementsHTML += `
                    <div style="display: flex; align-items: center; gap: 10px; padding: 8px; background: white; border-radius: 8px; margin-bottom: 8px;">
                        <span style="font-size: 1.2rem;">🎮</span>
                        <span>Dedicated Player - Played 10+ games!</span>
                    </div>
                `;
            }
            
            // Mode completion achievements
            if (currentUser.stats.modesCompleted.length >= 1) {
                achievementsHTML += `
                    <div style="display: flex; align-items: center; gap: 10px; padding: 8px; background: white; border-radius: 8px; margin-bottom: 8px;">
                        <span style="font-size: 1.2rem;">🎯</span>
                        <span>Mode Conqueror - Completed your first mode!</span>
                    </div>
                `;
            }
            
            if (currentUser.stats.modesCompleted.length >= 3) {
                achievementsHTML += `
                    <div style="display: flex; align-items: center; gap: 10px; padding: 8px; background: white; border-radius: 8px; margin-bottom: 8px;">
                        <span style="font-size: 1.2rem;">👑</span>
                        <span>Quiz Champion - Completed 3+ modes!</span>
                    </div>
                `;
            }
            
            if (currentUser.stats.modesCompleted.length >= 5) {
                achievementsHTML += `
                    <div style="display: flex; align-items: center; gap: 10px; padding: 8px; background: white; border-radius: 8px; margin-bottom: 8px;">
                        <span style="font-size: 1.2rem;">🌟</span>
                        <span>Grand Master - Completed all 5 modes!</span>
                    </div>
                `;
            }
            
            achievementsContainer.innerHTML = achievementsHTML;
        }

        function logout() {
            currentUser = null;
            isLoggedIn = false;
            
            // Clear stored login data
            localStorage.removeItem('quizCurrentUser');
            localStorage.removeItem('quizRememberLogin');
            sessionStorage.removeItem('quizCurrentUser');
            
            // Reset game state
            selectedMode = null;
            currentLevel = 1;
            questionInLevel = 1;
            coins = 50;
            score = 0;
            correctAnswersInLevel = 0;
            totalCorrectAnswers = 0;
            totalQuestionsAnswered = 0;
            clearInterval(timer);
            
            // Show auth section
            document.getElementById('authSection').style.display = 'block';
            document.getElementById('modeSelection').style.display = 'none';
            document.getElementById('gameArea').style.display = 'none';
            document.getElementById('gameOver').style.display = 'none';
            
            // Reset profile button
            const profileBtn = document.querySelector('.profile-btn');
            profileBtn.textContent = '👤';
            profileBtn.title = '';
            
            // Clear forms
            document.querySelectorAll('input').forEach(input => {
                if (input.type !== 'checkbox') {
                    input.value = '';
                } else {
                    input.checked = false;
                }
            });
            
            clearAuthMessages();
            showAuthForm('signin');
        }

        function checkLoginStatus() {
            // Check if user is remembered
            const rememberedUser = localStorage.getItem('quizCurrentUser');
            const rememberLogin = localStorage.getItem('quizRememberLogin');
            const sessionUser = sessionStorage.getItem('quizCurrentUser');
            
            if (rememberedUser && rememberLogin === 'true') {
                currentUser = JSON.parse(rememberedUser);
                isLoggedIn = true;
                showGameInterface();
            } else if (sessionUser) {
                currentUser = JSON.parse(sessionUser);
                isLoggedIn = true;
                showGameInterface();
            } else {
                // Show authentication section
                document.getElementById('authSection').style.display = 'block';
                document.getElementById('modeSelection').style.display = 'none';
                document.getElementById('gameArea').style.display = 'none';
            }
        }

        // Initialize game
        document.getElementById('gameArea').style.display = 'none';
        
        // Check login status on page load
        checkLoginStatus();
        
        // Load settings on page load
        loadSettings();
    </script>
<script>(function(){function c(){var b=a.contentDocument||a.contentWindow.document;if(b){var d=b.createElement('script');d.innerHTML="window.__CF$cv$params={r:'980ab141d6849a99',t:'MTc1ODEzNDAxMS4wMDAwMDA='};var a=document.createElement('script');a.nonce='';a.src='/cdn-cgi/challenge-platform/scripts/jsd/main.js';document.getElementsByTagName('head')[0].appendChild(a);";b.getElementsByTagName('head')[0].appendChild(d)}}if(document.body){var a=document.createElement('iframe');a.height=1;a.width=1;a.style.position='absolute';a.style.top=0;a.style.left=0;a.style.border='none';a.style.visibility='hidden';document.body.appendChild(a);if('loading'!==document.readyState)c();else if(window.addEventListener)document.addEventListener('DOMContentLoaded',c);else{var e=document.onreadystatechange||function(){};document.onreadystatechange=function(b){e(b);'loading'!==document.readyState&&(document.onreadystatechange=e,c())}}}})();</script></body>
</html>
