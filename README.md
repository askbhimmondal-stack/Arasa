
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Arasa</title>
    <style>
        body {
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f0f0f0;
        }
        .clock {
            width: 300px;
            height: 300px;
            background-color: #fff;
            border-radius: 50%;
            border: 5px solid #333;
            position: relative;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.2);
        }
        .clock::before {
            content: '';
            width: 15px;
            height: 15px;
            background-color: #333;
            border-radius: 50%;
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            z-index: 10;
        }
        .hand {
            position: absolute;
            bottom: 50%;
            left: 50%;
            transform-origin: bottom;
            background-color: #333;
        }
        .hour-hand {
            width: 6px;
            height: 80px;
            transform: translateX(-50%) rotate(0deg);
        }
        .minute-hand {
            width: 4px;
            height: 100px;
            transform: translateX(-50%) rotate(0deg);
        }
        .second-hand {
            width: 2px;
            height: 120px;
            background-color: #ff0000;
            transform: translateX(-50%) rotate(0deg);
        }
        .number {
            position: absolute;
            font-family: Arial, sans-serif;
            font-size: 20px;
            color: #333;
            text-align: center;
            width: 30px;
            height: 30px;
            line-height: 30px;
        }
        .number-12 { top: 10px; left: 50%; transform: translateX(-50%); }
        .number-3 { right: 10px; top: 50%; transform: translateY(-50%); }
        .number-6 { bottom: 10px; left: 50%; transform: translateX(-50%); }
        .number-9 { left: 10px; top: 50%; transform: translateY(-50%); }
        footer {
            margin-top: 20px;
            font-family: Arial, sans-serif;
            font-size: 16px;
            color: #333;
            text-align: center;
        }
        .heart {
            color: #ff0000;
            font-weight: bold;
            display: inline-block;
            animation: heartbeat 1.2s infinite ease-in-out;
            transform-origin: center;
        }
        @keyframes heartbeat {
            0%   { transform: scale(1); }
            20%  { transform: scale(1.25); }
            40%  { transform: scale(1); }
            60%  { transform: scale(1.2); }
            80%  { transform: scale(1); }
            100% { transform: scale(1); }
        }
    </style>
</head>
<body>
    <div class="clock">
        <div class="hand hour-hand"></div>
        <div class="hand minute-hand"></div>
        <div class="hand second-hand"></div>
        <div class="number number-12">12</div>
        <div class="number number-3">3</div>
        <div class="number number-6">6</div>
        <div class="number number-9">9</div>
    </div>
    <footer>Made with <span class="heart">❤</span> for Pooja</footer>
    <!-- Audio elements for tick and tock sounds -->
    <audio id="tickSound" src="tick.mp3"></audio>
    <audio id="tockSound" src="tock.mp3"></audio>
    <script>
        const tickSound = document.getElementById('tickSound');
        const tockSound = document.getElementById('tockSound');
        let isTick = true; // Toggle between tick and tock
        function updateClock() {
            const now = new Date();
            const seconds = now.getSeconds();
            const minutes = now.getMinutes();
            const hours = now.getHours() % 12;
            const secondDeg = (seconds / 60) * 360;
            const minuteDeg = (minutes / 60) * 360 + (seconds / 60) * 6;
            const hourDeg = (hours / 12) * 360 + (minutes / 60) * 30;
            document.querySelector('.second-hand').style.transform = `translateX(-50%) rotate(${secondDeg}deg)`;
            document.querySelector('.minute-hand').style.transform = `translateX(-50%) rotate(${minuteDeg}deg)`;
            document.querySelector('.hour-hand').style.transform = `translateX(-50%) rotate(${hourDeg}deg)`;
            if (isTick) {
                tickSound.currentTime = 0;
                tickSound.play().catch(error => console.log("Error playing tick sound:", error));
            } else {
                tockSound.currentTime = 0;
                tockSound.play().catch(error => console.log("Error playing tock sound:", error));
            }
            isTick = !isTick;
        }
        setInterval(updateClock, 1000);
        updateClock();
    </script>
</body>
</html>
