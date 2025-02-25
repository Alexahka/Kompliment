<!DOCTYPE html>
<html lang="ru">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Приложение с сердечками и записной книжкой</title>
    <link href="https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&family=Pacifico&display=swap" rel="stylesheet">
    <style>
        body {
            margin: 0;
            padding: 0;
            overflow: hidden;
            background-color: #ffc0cb; /* Розовый фон */
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            position: relative;
            font-family: 'Montserrat', sans-serif; /* Основной шрифт */
        }

        .heart {
            position: absolute;
            color: red;
            font-size: 20px;
            animation: float 5s infinite ease-in-out;
        }

        @keyframes float {
            0% {
                transform: translateY(0) translateX(0) rotate(0deg);
            }
            50% {
                transform: translateY(-100px) translateX(100px) rotate(180deg);
            }
            100% {
                transform: translateY(0) translateX(0) rotate(360deg);
            }
        }

        .container {
            text-align: center;
            background-color: rgba(255, 255, 255, 0.9);
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
        }

        /* Стили для кнопки в форме сердца */
        .heart-button {
            background: none;
            border: none;
            cursor: pointer;
            width: 120px;
            height: 120px;
            padding: 0;
            margin: 10px;
            position: relative;
        }

        .heart-button svg {
            width: 100%;
            height: 100%;
            fill: #ff69b4; /* Розовый цвет сердца */
            transition: fill 0.3s ease;
        }

        .heart-button:hover svg {
            fill: #ff1493; /* Темно-розовый при наведении */
        }

        .heart-button text {
            font-size: 22px; /* Увеличенный размер шрифта */
            font-weight: bold;
            fill: white;
            text-anchor: middle;
            user-select: none;
            font-family: 'Pacifico', cursive; /* Красивый шрифт для текста на кнопке */
            text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.5);
            animation: pulse 1.5s infinite;
        }

        @keyframes pulse {
            0% {
                transform: scale(1);
            }
            50% {
                transform: scale(1.1);
            }
            100% {
                transform: scale(1);
            }
        }

        /* Стили для кнопки изменения фона */
        .change-background-button {
            position: absolute;
            bottom: 20px;
            right: 20px;
            width: 60px;
            height: 60px;
            border-radius: 50%;
            background-color: #ff69b4;
            border: none;
            color: white;
            font-size: 14px;
            cursor: pointer;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
            font-family: 'Montserrat', sans-serif;
        }

        .change-background-button:hover {
            background-color: #ff1493;
        }

        /* Стили для кнопок под сердцем */
        .bottom-buttons {
            display: flex;
            justify-content: center;
            gap: 20px;
            margin-top: 20px;
        }

        .square-button {
            width: 100px;
            height: 40px;
            border-radius: 5px;
            border: none;
            color: white;
            font-size: 14px;
            cursor: pointer;
            display: flex;
            align-items: center;
            justify-content: center;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.3);
            font-family: 'Montserrat', sans-serif;
        }

        .square-button.add-task {
            background-color: #4CAF50; /* Зеленый */
        }

        .square-button.add-task:hover {
            background-color: #45a049;
        }

        .round-button.thank-you {
            background-color: #ffcc00; /* Желтый */
            animation: glow 2s infinite;
        }

        .round-button.thank-you:hover {
            background-color: #e6b800;
        }

        @keyframes glow {
            0% {
                box-shadow: 0 0 10px #ffcc00;
            }
            50% {
                box-shadow: 0 0 20px #ffcc00;
            }
            100% {
                box-shadow: 0 0 10px #ffcc00;
            }
        }

        /* Стили для всплывающего окна с комплиментами */
        .popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
            text-align: center;
            width: 300px;
            height: 300px;
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="red" d="M462.3 62.6C407.5 15.9 326 24.3 275.7 76.2L256 96.5l-19.7-20.3C186.1 24.3 104.5 15.9 49.7 62.6c-62.8 53.6-66.1 149.8-9.9 207.9l193.5 199.8c12.5 12.9 32.8 12.9 45.3 0l193.5-199.8c56.3-58.1 53-154.3-9.8-207.9z"/></svg>');
            background-size: 100% 100%;
            background-repeat: no-repeat;
            color: white;
            font-size: 20px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            font-family: 'Pacifico', cursive; /* Красивый шрифт для текста */
        }

        .popup button {
            margin-top: 20px;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            background-color: #ff69b4;
            color: white;
            cursor: pointer;
            font-family: 'Montserrat', sans-serif;
        }

        .popup button:hover {
            background-color: #ff1493;
        }

        /* Стили для всплывающего окна с благодарностью */
        .thank-you-popup {
            display: none;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            background-color: white;
            padding: 20px;
            border-radius: 20px;
            box-shadow: 0 0 20px rgba(0, 0, 0, 0.5);
            text-align: center;
            width: 300px;
            height: 300px;
            background-image: url('data:image/svg+xml;utf8,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="red" d="M462.3 62.6C407.5 15.9 326 24.3 275.7 76.2L256 96.5l-19.7-20.3C186.1 24.3 104.5 15.9 49.7 62.6c-62.8 53.6-66.1 149.8-9.9 207.9l193.5 199.8c12.5 12.9 32.8 12.9 45.3 0l193.5-199.8c56.3-58.1 53-154.3-9.8-207.9z"/></svg>');
            background-size: 100% 100%;
            background-repeat: no-repeat;
            color: white;
            font-size: 20px;
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            font-family: 'Pacifico', cursive; /* Красивый шрифт для текста */
        }

        .thank-you-popup div {
            margin: 10px 0;
        }

        .thank-you-popup button {
            margin-top: 20px;
            padding: 10px 20px;
            border: none;
            border-radius: 5px;
            background-color: #ff69b4;
            color: white;
            cursor: pointer;
            font-family: 'Montserrat', sans-serif;
        }

        .thank-you-popup button:hover {
            background-color: #ff1493;
        }

        .input-field {
            width: 200px;
            height: 30px;
            padding: 5px;
            margin-top: 20px;
            border-radius: 5px;
            border: 1px solid #ccc;
            font-size: 16px;
            font-family: 'Montserrat', sans-serif;
        }

        /* Стили для бегущей строки */
        .marquee {
            width: 100%;
            overflow: hidden;
            white-space: nowrap;
            box-sizing: border-box;
            background-color: #ff69b4;
            color: white;
            font-size: 24px;
            padding: 10px 0;
            position: absolute;
            top: 0;
            left: 0;
            font-family: 'Pacifico', cursive; /* Красивый шрифт для бегущей строки */
        }

        .marquee span {
            display: inline-block;
            padding-left: 100%;
            animation: marquee 10s linear infinite;
        }

        @keyframes marquee {
            0% {
                transform: translateX(100%);
            }
            100% {
                transform: translateX(-100%);
            }
        }

        /* Стили для списка задач */
        .task-list {
            margin-top: 20px;
            text-align: left;
        }

        .task-item {
            display: flex;
            justify-content: space-between;
            align-items: center;
            padding: 10px;
            border-bottom: 1px solid #ccc;
            font-family: 'Montserrat', sans-serif;
        }

        .task-item.completed {
            text-decoration: line-through;
            opacity: 0.6;
        }

        .task-buttons {
            display: flex;
            gap: 10px;
        }

        .task-buttons button {
            padding: 5px 10px;
            border: none;
            border-radius: 5px;
            cursor: pointer;
            font-family: 'Montserrat', sans-serif;
        }

        .task-buttons button.complete {
            background-color: #4CAF50; /* Зеленый */
            color: white;
        }

        .task-buttons button.delete {
            background-color: #f44336; /* Красный */
            color: white;
        }
    </style>
</head>
<body>
    <!-- Бегущая строка -->
    <div class="marquee">
        <span>Я твой любимый помощник ❤️</span>
    </div>

    <div class="container">
        <!-- Кнопка в форме сердца с надписью -->
        <button class="heart-button" id="complimentButton">
            <svg viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg">
                <path d="M462.3 62.6C407.5 15.9 326 24.3 275.7 76.2L256 96.5l-19.7-20.3C186.1 24.3 104.5 15.9 49.7 62.6c-62.8 53.6-66.1 149.8-9.9 207.9l193.5 199.8c12.5 12.9 32.8 12.9 45.3 0l193.5-199.8c56.3-58.1 53-154.3-9.8-207.9z"/>
                <text x="50%" y="60%">Нажми меня</text>
            </svg>
        </button>

        <!-- Кнопки под сердцем -->
        <div class="bottom-buttons">
            <button class="square-button add-task" id="addTaskButton">Добавить</button>
            <button class="round-button thank-you" id="thankYouButton">☕</button>
        </div>

        <input type="text" class="input-field" id="taskInput" placeholder="Введите задачу">
        <div class="task-list" id="taskList"></div>
    </div>

    <!-- Кнопка изменения фона -->
    <button class="change-background-button" id="changeBackgroundButton">🎨</button>

    <!-- Всплывающее окно с комплиментами -->
    <div class="popup" id="complimentPopup">
        <div id="complimentText"></div>
        <button id="returnButton">Вернуться</button>
    </div>

    <!-- Всплывающее окно с благодарностью -->
    <div class="thank-you-popup" id="thankYouPopup">
        <div>Спасибо за поддержку! ❤️</div>
        <div>Ваша доброта делает мир лучше!</div>
        <div>Номер карты: 4323 3473 9932 3663</div>
        <button id="closeThankYouButton">Закрыть</button>
    </div>

    <script>
        // Массив с комплиментами
        const compliments = [
            "Ты выглядишь потрясающе!",
            "Ты светишься, как солнце!",
            "Ты умнее, чем ты думаешь!",
            "Ты делаешь мир лучше!",
            "Ты вдохновляешь окружающих!",
            "Ты уникален(а) и неповторим(а)!",
            "Ты — настоящая звезда!",
            "Ты заслуживаешь всего самого лучшего!",
        ];

        // Функция для показа случайного комплимента
        function showCompliment() {
            const complimentText = document.getElementById('complimentText');
            const randomCompliment = compliments[Math.floor(Math.random() * compliments.length)];
            complimentText.textContent = randomCompliment;
            document.getElementById('complimentPopup').style.display = 'flex';
        }

        // Функция для скрытия всплывающего окна
        function hideCompliment() {
            document.getElementById('complimentPopup').style.display = 'none';
        }

        // Функция для добавления задачи
        function addTask() {
            const taskInput = document.getElementById('taskInput');
            const taskText = taskInput.value.trim();

            if (taskText === "") {
                alert("Введите задачу!");
                return;
            }

            const taskList = document.getElementById('taskList');

            const taskItem = document.createElement('div');
            taskItem.classList.add('task-item');

            const taskTextElement = document.createElement('span');
            taskTextElement.textContent = taskText;

            const taskButtons = document.createElement('div');
            taskButtons.classList.add('task-buttons');

            const completeButton = document.createElement('button');
            completeButton.classList.add('complete');
            completeButton.textContent = "Завершено";
            completeButton.onclick = function () {
                taskItem.classList.toggle('completed');
            };

            const deleteButton = document.createElement('button');
            deleteButton.classList.add('delete');
            deleteButton.textContent = "Удалить";
            deleteButton.onclick = function () {
                taskList.removeChild(taskItem);
            };

            taskButtons.appendChild(completeButton);
            taskButtons.appendChild(deleteButton);

            taskItem.appendChild(taskTextElement);
            taskItem.appendChild(taskButtons);

            taskList.appendChild(taskItem);

            taskInput.value = ""; // Очищаем поле ввода
        }

        // Функция для изменения фона
        function changeBackground() {
            const colors = ["#ffc0cb", "#ffb6c1", "#ff69b4", "#ff1493", "#db7093"];
            const randomColor = colors[Math.floor(Math.random() * colors.length)];
            document.body.style.backgroundColor = randomColor;
        }

        // Функция для показа окна с благодарностью
        function showThankYouPopup() {
            document.getElementById('thankYouPopup').style.display = 'flex';
        }

        // Функция для скрытия окна с благодарностью
        function hideThankYouPopup() {
            document.getElementById('thankYouPopup').style.display = 'none';
        }

        // Назначение обработчиков событий
        document.getElementById('complimentButton').addEventListener('click', showCompliment);
        document.getElementById('returnButton').addEventListener('click', hideCompliment);
        document.getElementById('addTaskButton').addEventListener('click', addTask);
        document.getElementById('changeBackgroundButton').addEventListener('click', changeBackground);
        document.getElementById('thankYouButton').addEventListener('click', showThankYouPopup);
        document.getElementById('closeThankYouButton').addEventListener('click', hideThankYouPopup);

        // Создание летающих сердечек
        function createHeart() {
            const heart = document.createElement('div');
            heart.classList.add('heart');
            heart.innerHTML = '❤️';
            heart.style.left = Math.random() * window.innerWidth + 'px';
            heart.style.top = Math.random() * window.innerHeight + 'px';
            document.body.appendChild(heart);

            setTimeout(() => {
                heart.remove();
            }, 5000);
        }

        setInterval(createHeart, 500);
    </script>
</body>
</html>
