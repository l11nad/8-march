<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>С 8 Марта! 🌸</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: #f5e6e8;
            min-height: 100vh;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 20px;
            overflow: hidden;
        }

        /* Экран с конвертом */
        .envelope-screen {
            position: relative;
            width: 100%;
            max-width: 500px;
            height: 400px;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
        }

        .envelope-screen.hidden {
            display: none;
        }

        .hint {
            font-size: 1.2em;
            color: #c2185b;
            margin-bottom: 30px;
            text-align: center;
            animation: pulse 2s infinite;
        }

        @keyframes pulse {
            0%, 100% { opacity: 1; }
            50% { opacity: 0.5; }
        }

        .envelope-container {
            position: relative;
            width: 300px;
            height: 200px;
            cursor: pointer;
            transition: transform 0.3s ease;
        }

        .envelope-container:hover {
            transform: scale(1.05);
        }

        .envelope-back {
            position: absolute;
            width: 100%;
            height: 100%;
            background: #d32f2f;
            clip-path: polygon(0 0, 50% 60%, 100% 0, 100% 100%, 0 100%);
            z-index: 1;
        }

        .envelope-front {
            position: absolute;
            width: 100%;
            height: 100%;
            background: #e53935;
            clip-path: polygon(0 0, 50% 50%, 100% 0, 100% 100%, 0 100%);
            z-index: 3;
            transition: transform 0.6s ease;
            transform-origin: top center;
        }

        .envelope-front.open {
            transform: rotateX(-180deg);
        }

        .envelope-card {
            position: absolute;
            width: 90%;
            height: 85%;
            background: white;
            top: 10%;
            left: 5%;
            z-index: 2;
            border-radius: 5px;
            box-shadow: 0 2px 10px rgba(0,0,0,0.1);
            transition: transform 0.8s ease;
        }

        .envelope-card.pulled {
            transform: translateY(-120%);
        }

        .card-pattern {
            width: 100%;
            height: 100%;
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            grid-template-rows: repeat(3, 1fr);
            padding: 10px;
            gap: 5px;
        }

        .pattern-cell {
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2em;
        }

        .pattern-cell:nth-child(odd) {
            background: #e91e63;
            color: #fce4ec;
        }

        .pattern-cell:nth-child(even) {
            background: #fce4ec;
            color: #e91e63;
        }

        /* Экран с открыткой */
        .card-screen {
            display: none;
            animation: fadeIn 1s ease;
        }

        .card-screen.visible {
            display: block;
        }

        @keyframes fadeIn {
            from {
                opacity: 0;
                transform: scale(0.9);
            }
            to {
                opacity: 1;
                transform: scale(1);
            }
        }

        .container {
            background: white;
            border-radius: 20px;
            padding: 50px;
            max-width: 600px;
            width: 100%;
            box-shadow: 0 20px 60px rgba(0, 0, 0, 0.15);
            text-align: center;
            border: 8px solid #e91e63;
        }

        h1 {
            color: #c2185b;
            font-size: 2.5em;
            margin-bottom: 30px;
            font-weight: 700;
            letter-spacing: 1px;
        }

        .flower-pattern {
            width: 100%;
            height: 80px;
            display: flex;
            justify-content: center;
            align-items: center;
            gap: 15px;
            margin: 20px 0;
        }

        .flower {
            width: 50px;
            height: 50px;
            position: relative;
        }

        .flower::before {
            content: '✿';
            font-size: 50px;
            position: absolute;
            color: #e91e63;
        }

        .flower:nth-child(2n)::before {
            color: #fce4ec;
            text-shadow: 0 0 0 1px #e91e63;
        }

        .greeting {
            font-size: 1.2em;
            color: #333;
            line-height: 1.8;
            margin: 30px 0;
            min-height: 120px;
            display: flex;
            align-items: center;
            justify-content: center;
            padding: 20px;
        }

        button {
            background: #e91e63;
            color: white;
            border: none;
            padding: 15px 40px;
            font-size: 1.1em;
            border-radius: 50px;
            cursor: pointer;
            transition: all 0.3s ease;
            margin-top: 20px;
            font-weight: 600;
            box-shadow: 0 4px 15px rgba(233, 30, 99, 0.3);
        }

        button:hover {
            background: #c2185b;
            transform: translateY(-2px);
            box-shadow: 0 6px 20px rgba(233, 30, 99, 0.4);
        }

        button:active {
            transform: translateY(0);
        }

        .decorative-text {
            font-size: 0.9em;
            color: #c2185b;
            margin-top: 30px;
            font-style: italic;
        }

        @media (max-width: 600px) {
            .container {
                padding: 30px 20px;
            }
            
            h1 {
                font-size: 2em;
            }
            
            .greeting {
                font-size: 1.1em;
            }

            .envelope-container {
                width: 250px;
                height: 167px;
            }
        }

        @media (max-width: 400px) {
            .hint {
                font-size: 1em;
            }
        }
    </style>
</head>
<body>
    <!-- Экран 1: Конверт -->
    <div class="envelope-screen" id="envelopeScreen">
        <div class="hint">
            👆 Нажмите на конверт, чтобы открыть
        </div>
        <div class="envelope-container" id="envelope">
            <div class="envelope-back"></div>
            <div class="envelope-card" id="card">
                <div class="card-pattern">
                    <div class="pattern-cell">✿</div>
                    <div class="pattern-cell">✿</div>
                    <div class="pattern-cell">✿</div>
                    <div class="pattern-cell">✿</div>
                    <div class="pattern-cell">✿</div>
                    <div class="pattern-cell">✿</div>
                    <div class="pattern-cell">✿</div>
                    <div class="pattern-cell">✿</div>
                    <div class="pattern-cell">✿</div>
                </div>
            </div>
            <div class="envelope-front" id="envelopeFront"></div>
        </div>
    </div>

    <!-- Экран 2: Открытка -->
    <div class="card-screen" id="cardScreen">
        <div class="container">
            <h1>С 8 Марта!</h1>
            
            <div class="flower-pattern">
                <div class="flower"></div>
                <div class="flower"></div>
                <div class="flower"></div>
                <div class="flower"></div>
            </div>

            <div class="greeting" id="greeting">
                Желаем вам весеннего настроения, ярких улыбок и море цветов! Пусть каждый день радует новыми возможностями!
            </div>

            <button onclick="getRandomGreeting()">Ещё поздравление</button>

            <div class="decorative-text">
                [ наполняй энергией, мотивируй, заряжай эмоциями ]
            </div>
        </div>
    </div>

    <script>
        const greetings = [
            "Желаем вам весеннего настроения, ярких улыбок и море цветов! Пусть каждый день радует новыми возможностями!",
            
            "С праздником весны! Будьте счастливы, любимы и успешны во всех начинаниях!",
            
            "Пусть этот весенний день принесет море комплиментов, океан цветов и улыбок! С 8 Марта!",
            
            "Желаем вдохновения, радости и исполнения всех желаний! Вы делаете наш коллектив особенным!",
            
            "С праздником! Пусть жизнь будет яркой, как весенние цветы, и сладкой, как праздничный торт!",
            
            "Спасибо за то, что вы есть! Желаем здоровья, счастья и пусть все мечты сбываются!",
            
            "С Международным женским днем! Пусть каждый день будет наполнен теплом, уютом и любовью!",
            
            "Вы — наше вдохновение! Желаем успехов в работе и гармонии в личной жизни! С 8 Марта!",
            
            "Пусть весна принесет новые победы, яркие эмоции и незабываемые впечатления!",
            
            "С праздником, дорогие коллеги! Вы делаете мир краше просто своим присутствием!"
        ];

        let usedGreetings = [0]; // Первое поздравление уже показано
        let envelopeOpened = false;

        // Открытие конверта
        document.getElementById('envelope').addEventListener('click', function() {
            if (!envelopeOpened) {
                envelopeOpened = true;
                
                // Открываем клапан конверта
                document.getElementById('envelopeFront').classList.add('open');
                
                // Через 0.3с вытаскиваем открытку
                setTimeout(() => {
                    document.getElementById('card').classList.add('pulled');
                }, 300);
                
                // Через 1.5с показываем полную открытку
                setTimeout(() => {
                    document.getElementById('envelopeScreen').classList.add('hidden');
                    document.getElementById('cardScreen').classList.add('visible');
                }, 1500);
            }
        });

        // Получение случайного поздравления
        function getRandomGreeting() {
            if (usedGreetings.length === greetings.length) {
                usedGreetings = [];
            }

            let availableIndices = [];
            for (let i = 0; i < greetings.length; i++) {
                if (!usedGreetings.includes(i)) {
                    availableIndices.push(i);
                }
            }
            
            let randomIndex = availableIndices[Math.floor(Math.random() * availableIndices.length)];
            usedGreetings.push(randomIndex);

            const greetingElement = document.getElementById('greeting');
            greetingElement.style.opacity = '0';
            greetingElement.style.transform = 'scale(0.95)';
            
            setTimeout(() => {
                greetingElement.textContent = greetings[randomIndex];
                greetingElement.style.transition = 'all 0.5s ease';
                greetingElement.style.opacity = '1';
                greetingElement.style.transform = 'scale(1)';
            }, 300);
        }
    </script>
</body>
</html>
