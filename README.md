<!DOCTYPE html>
<html>
<head>
    <title>3D Classroom Roll Call</title>
    <style>
        body {
            margin: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            background: #f0f5ff;
            min-height: 100vh;
            font-family: Arial, sans-serif;
        }

        .class-buttons {
            margin: 30px 0;
            display: flex;
            gap: 20px;
        }

        .class-btn {
            padding: 15px 30px;
            border: none;
            border-radius: 10px;
            background: linear-gradient(145deg, #4CAF50, #45a049);
            color: white;
            font-size: 18px;
            cursor: pointer;
            transform-style: preserve-3d;
            transition: all 0.3s;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
        }

        .class-btn.active {
            background: linear-gradient(145deg, #FF9800, #fb8c00);
            transform: translateY(-3px);
        }

        .name-display {
            width: 300px;
            height: 150px;
            background: white;
            margin: 50px 0;
            display: flex;
            justify-content: center;
            align-items: center;
            font-size: 32px;
            font-weight: bold;
            border-radius: 20px;
            box-shadow: 0 10px 20px rgba(0,0,0,0.2);
            transform-style: preserve-3d;
            perspective: 1000px;
        }

        .name-text {
            transition: all 0.3s;
            transform-origin: center;
        }

        .controls {
            display: flex;
            gap: 30px;
        }

        .control-btn {
            padding: 20px 40px;
            border: none;
            border-radius: 15px;
            font-size: 20px;
            cursor: pointer;
            transition: all 0.3s;
            box-shadow: 0 5px 15px rgba(0,0,0,0.2);
            color: white;
        }

        #startBtn {
            background: linear-gradient(145deg, #2196F3, #1976D2);
        }

        #stopBtn {
            background: linear-gradient(145deg, #f44336, #d32f2f);
        }

        .jump {
            animation: jump 0.5s ease;
        }

        @keyframes jump {
            0%, 100% { transform: translateY(0); }
            50% { transform: translateY(-20px); }
        }
    </style>
</head>
<body>
    <div class="class-buttons">
        <button class="class-btn" onclick="selectClass(210241)">210241</button>
        <button class="class-btn" onclick="selectClass(210242)">210242</button>
        <button class="class-btn" onclick="selectClass(210243)">210243</button>
        <button class="class-btn" onclick="selectClass(210244)">210244</button>
    </div>

    <div class="name-display">
        <div class="name-text" id="name">Ready</div>
    </div>

    <div class="controls">
        <button class="control-btn" id="startBtn" onclick="startRoll()">Start</button>
        <button class="control-btn" id="stopBtn" onclick="stopRoll()">Stop</button>
    </div>

    <script>
        const students = {
            210241: ['    ', '    ', '  ͢  ', '    Ԫ', ' Ž   ', '   ', '     ', '     ', '      ', ' ߿ ɽ'],
            210242: ['    ', '    ', '  ͢  ', '    Ԫ', ' Ž   ', '   ', '     ', '     ', '      ', ' ߿ ɽ'],
            210243: ['    ', '    ', '  ͢  ', '    Ԫ', ' Ž   ', '   ', '     ', '     ', '      ', ' ߿ ɽ'],
            210244: ['    ', '    ', '  ͢  ', '    Ԫ', ' Ž   ', '   ', '     ', '     ', '      ', ' ߿ ɽ']
        };

        let currentClass = 210241;
        let isRolling = false;
        let intervalId = null;
        const nameElement = document.getElementById('name');

        function selectClass(className) {
            currentClass = className;
            document.querySelectorAll('.class-btn').forEach(btn => {
                btn.classList.toggle('active', btn.textContent == className);
            });
        }

        function startRoll() {
            if (!isRolling) {
                isRolling = true;
                intervalId = setInterval(() => {
                    const randomIndex = Math.floor(Math.random() * students[currentClass].length);
                    nameElement.textContent = students[currentClass][randomIndex];
                    nameElement.classList.add('jump');
                    setTimeout(() => nameElement.classList.remove('jump'), 500);
                }, 100);
            }
        }

        function stopRoll() {
            if (isRolling) {
                clearInterval(intervalId);
                isRolling = false;
                nameElement.classList.add('jump');
                setTimeout(() => nameElement.classList.remove('jump'), 500);
            }
        }

        //   ʼ  Ĭ ϰ༶
        selectClass(210241);
    </script>
</body>
</html>
