<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Проект "КРУГ"</title>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
        
        body {
            font-family: 'Segoe UI', -apple-system, BlinkMacSystemFont, sans-serif;
            background: linear-gradient(135deg, #f5f7fa 0%, #e4edf5 100%);
            min-height: 100vh;
            color: #333;
            line-height: 1.6;
            overflow-x: hidden;
        }
        
        .container {
            max-width: 1200px;
            margin: 0 auto;
            padding: 40px 20px;
            text-align: center;
        }
        
        /* Главная страница */
        .main-screen {
            opacity: 1;
            transition: opacity 0.8s cubic-bezier(0.4, 0, 0.2, 1);
        }
        
        .main-screen.hidden {
            opacity: 0;
            pointer-events: none;
            transform: translateY(-20px);
        }
        
        .logo {
            font-size: 42px;
            font-weight: 300;
            letter-spacing: 8px;
            margin-bottom: 60px;
            color: #222;
            position: relative;
            display: inline-block;
        }
        
        .logo:after {
            content: '';
            position: absolute;
            bottom: -10px;
            left: 50%;
            transform: translateX(-50%);
            width: 60px;
            height: 2px;
            background: #222;
        }
        
        .intro-text {
            font-size: 24px;
            font-weight: 300;
            max-width: 800px;
            margin: 0 auto 80px;
            color: #444;
            text-align: center;
            line-height: 1.8;
            padding: 0 20px;
        }
        
        .highlight {
            font-weight: 500;
            color: #222;
            position: relative;
            display: inline-block;
        }
        
        .highlight:after {
            content: '';
            position: absolute;
            bottom: -2px;
            left: 0;
            width: 100%;
            height: 1px;
            background: #222;
            transform: scaleX(0);
            transition: transform 0.3s ease;
        }
        
        .highlight:hover:after {
            transform: scaleX(1);
        }
        
        .buttons-grid {
            display: flex;
            justify-content: center;
            gap: 30px;
            margin-top: 60px;
            flex-wrap: wrap;
        }
        
        .mode-btn {
            background: #111;
            color: white;
            border: none;
            padding: 25px 40px;
            font-size: 20px;
            font-weight: 400;
            letter-spacing: 1px;
            cursor: pointer;
            transition: all 0.4s cubic-bezier(0.4, 0, 0.2, 1);
            min-width: 220px;
            position: relative;
            overflow: hidden;
            border-radius: 2px;
        }
        
        .mode-btn:before {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            width: 0;
            height: 0;
            background: rgba(255, 255, 255, 0.1);
            border-radius: 50%;
            transform: translate(-50%, -50%);
            transition: width 0.6s, height 0.6s;
        }
        
        .mode-btn:hover:before {
            width: 300px;
            height: 300px;
        }
        
        .mode-btn:hover {
            transform: translateY(-5px);
            box-shadow: 0 15px 30px rgba(0, 0, 0, 0.15);
        }
        
        .mode-btn:active {
            transform: translateY(-2px);
        }
        
        /* Экран режимов */
        .mode-screen {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background: white;
            display: flex;
            justify-content: center;
            align-items: center;
            opacity: 0;
            pointer-events: none;
            transition: opacity 0.8s cubic-bezier(0.4, 0, 0.2, 1);
            z-index: 100;
        }
        
        .mode-screen.active {
            opacity: 1;
            pointer-events: all;
        }
        
        /* Точка */
        .pulsing-dot {
            width: 20px;
            height: 20px;
            background: #111;
            border-radius: 50%;
            animation: pulse 1s infinite;
            box-shadow: 0 0 0 0 rgba(17, 17, 17, 0.7);
        }
        
        @keyframes pulse {
            0% {
                transform: scale(0.95);
                box-shadow: 0 0 0 0 rgba(17, 17, 17, 0.7);
            }
            70% {
                transform: scale(1);
                box-shadow: 0 0 0 15px rgba(17, 17, 17, 0);
            }
            100% {
                transform: scale(0.95);
                box-shadow: 0 0 0 0 rgba(17, 17, 17, 0);
            }
        }
        
        /* Круг */
        .red-circle {
            width: 200px;
            height: 200px;
            background: #ff3b30;
            border-radius: 50%;
            position: relative;
            box-shadow: 0 10px 30px rgba(255, 59, 48, 0.3);
        }
        
        .red-circle:after {
            content: '';
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 180px;
            height: 180px;
            border-radius: 50%;
            background: #ff5e54;
            z-index: -1;
            animation: circleGlow 3s infinite alternate;
        }
        
        @keyframes circleGlow {
            0% { opacity: 0.5; transform: translate(-50%, -50%) scale(1); }
            100% { opacity: 0.8; transform: translate(-50%, -50%) scale(1.1); }
        }
        
        /* Кнопка возврата */
        .back-btn {
            position: fixed;
            top: 30px;
            left: 30px;
            background: rgba(0, 0, 0, 0.8);
            color: white;
            border: none;
            width: 50px;
            height: 50px;
            border-radius: 50%;
            cursor: pointer;
            display: flex;
            justify-content: center;
            align-items: center;
            z-index: 101;
            opacity: 0;
            transform: translateX(-20px);
            transition: all 0.5s cubic-bezier(0.4, 0, 0.2, 1);
        }
        
        .back-btn.visible {
            opacity: 1;
            transform: translateX(0);
        }
        
        .back-btn:hover {
            background: #000;
            transform: scale(1.1);
        }
        
        /* Футер */
        .footer {
            position: fixed;
            bottom: 30px;
            width: 100%;
            text-align: center;
            font-size: 14px;
            color: #777;
            z-index: 1;
        }
        
        /* Адаптивность */
        @media (max-width: 768px) {
            .container {
                padding: 30px 15px;
            }
            
            .logo {
                font-size: 32px;
                letter-spacing: 6px;
                margin-bottom: 40px;
            }
            
            .intro-text {
                font-size: 20px;
                margin-bottom: 50px;
            }
            
            .buttons-grid {
                flex-direction: column;
                align-items: center;
                gap: 20px;
                margin-top: 40px;
            }
            
            .mode-btn {
                width: 100%;
                max-width: 280px;
                padding: 20px;
            }
            
            .red-circle {
                width: 150px;
                height: 150px;
            }
            
            .red-circle:after {
                width: 130px;
                height: 130px;
            }
        }
        
        /* Анимация появления */
        @keyframes fadeInUp {
            from {
                opacity: 0;
                transform: translateY(30px);
            }
            to {
                opacity: 1;
                transform: translateY(0);
            }
        }
        
        .fade-in {
            animation: fadeInUp 0.8s ease forwards;
        }
        
        .delay-1 { animation-delay: 0.2s; opacity: 0; }
        .delay-2 { animation-delay: 0.4s; opacity: 0; }
        .delay-3 { animation-delay: 0.6s; opacity: 0; }
    </style>
</head>
<body>
    <!-- Кнопка возврата -->
    <button class="back-btn" id="backBtn">
        <i class="fas fa-arrow-left"></i>
    </button>
    
    <!-- Главный экран -->
    <div class="container">
        <div class="main-screen" id="mainScreen">
            <h1 class="logo fade-in">КРУГ</h1>
            
            <div class="intro-text fade-in delay-1">
                Привет, это проект <span class="highlight">"КРУГ"</span>. Помните видео Эштона Холла? Он говорит, что его распорядок дня помог ему добиться такого успеха. Мы же делаем ставку на технологию <span class="highlight">"отключения"</span>. Вам можно попробовать прямо сейчас. Это бесплатно!
            </div>
            
            <div class="buttons-grid">
                <button class="mode-btn fade-in delay-2" data-mode="white">
                    <i class="fas fa-square"></i> БЕЛЫЙ ЭКРАН
                </button>
                <button class="mode-btn fade-in delay-2" data-mode="dot">
                    <i class="fas fa-circle"></i> ТОЧКА
                </button>
                <button class="mode-btn fade-in delay-3" data-mode="circle">
                    <i class="fas fa-dot-circle"></i> КРУГ
                </button>
            </div>
        </div>
    </div>
    
    <!-- Экран режимов -->
    <div class="mode-screen" id="whiteScreen">
        <!-- Просто белый экран -->
    </div>
    
    <div class="mode-screen" id="dotScreen">
        <div class="pulsing-dot"></div>
    </div>
    
    <div class="mode-screen" id="circleScreen">
        <div class="red-circle"></div>
    </div>
    
    <!-- Футер -->
    <div class="footer fade-in delay-3">
        Проект "КРУГ" • Технология отключения • 2023
    </div>
    
    <script>
        // Элементы
        const mainScreen = document.getElementById('mainScreen');
        const backBtn = document.getElementById('backBtn');
        const modeButtons = document.querySelectorAll('.mode-btn');
        const modeScreens = {
            white: document.getElementById('whiteScreen'),
            dot: document.getElementById('dotScreen'),
            circle: document.getElementById('circleScreen')
        };
        
        // Текущий активный режим
        let currentMode = null;
        
        // Функция перехода в режим
        function enterMode(mode) {
            currentMode = mode;
            
            // Плавно скрываем главный экран
            mainScreen.classList.add('hidden');
            
            // Показываем кнопку возврата
            setTimeout(() => {
                backBtn.classList.add('visible');
            }, 300);
            
            // Показываем выбранный экран
            setTimeout(() => {
                // Скрываем все экраны
                Object.values(modeScreens).forEach(screen => {
                    screen.classList.remove('active');
                });
                
                // Показываем выбранный экран
                if (modeScreens[mode]) {
                    modeScreens[mode].classList.add('active');
                }
            }, 500);
        }
        
        // Функция возврата на главный экран
        function returnToMain() {
            // Скрываем кнопку возврата
            backBtn.classList.remove('visible');
            
            // Скрываем все экраны режимов
            Object.values(modeScreens).forEach(screen => {
                screen.classList.remove('active');
            });
            
            // Показываем главный экран
            setTimeout(() => {
                mainScreen.classList.remove('hidden');
            }, 300);
            
            currentMode = null;
        }
        
        // Обработчики событий для кнопок режимов
        modeButtons.forEach(button => {
            button.addEventListener('click', function() {
                const mode = this.getAttribute('data-mode');
                enterMode(mode);
            });
        });
        
        // Обработчик для кнопки возврата
        backBtn.addEventListener('click', returnToMain);
        
        // Закрытие по клавише Escape
        document.addEventListener('keydown', function(event) {
            if (event.key === 'Escape' && currentMode) {
                returnToMain();
            }
        });
        
        // Плавное появление элементов при загрузке
        window.addEventListener('load', function() {
            document.body.style.opacity = 0;
            document.body.style.transition = 'opacity 0.8s';
            
            setTimeout(() => {
                document.body.style.opacity = 1;
            }, 100);
        });
        
        // Дополнительный эффект при наведении на кнопки
        modeButtons.forEach(btn => {
            btn.addEventListener('mouseenter', function() {
                this.style.transform = 'translateY(-5px)';
            });
            
            btn.addEventListener('mouseleave', function() {
                this.style.transform = 'translateY(0)';
            });
        });
    </script>
</body>
</html>
