<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome to my Github!</title>
    <style>
        body {
            background-color: #000000;
            color: #00FF00;
            font-family: "Courier New", Courier, monospace;
            text-align: center;
            padding: 20px;
        }
        h1 {
            font-size: 36px;
            text-shadow: 2px 2px #FF00FF;
        }
        .rainbow-text {
            background-image: linear-gradient(to left, violet, indigo, blue, green, yellow, orange, red);
            -webkit-background-clip: text;
            color: transparent;
            font-size: 24px;
            font-weight: bold;
        }
        .animation-container {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
            gap: 20px;
            margin-top: 20px;
        }
        .animation {
            background-color: #001100;
            border: 2px solid #00FF00;
            padding: 10px;
            width: 300px;
        }
        canvas {
            border: 2px solid #00FF00;
        }
    </style>
</head>
<body>
    <h1>Retro Math and Science Animations</h1>
    <p class="rainbow-text">Watch cool visualizations!</p>
    <div class="animation-container">
        <div class="animation">
            <h2>Bubble Sort</h2>
            <canvas id="bubbleSortCanvas" width="280" height="200"></canvas>
        </div>
        <div class="animation">
            <h2>Sine Wave</h2>
            <canvas id="sineWaveCanvas" width="280" height="200"></canvas>
        </div>
        <div class="animation">
            <h2>Solar System</h2>
            <canvas id="solarSystemCanvas" width="280" height="200"></canvas>
        </div>
    </div>

    <script>
        // Bubble Sort Animation
        const bubbleSortCanvas = document.getElementById('bubbleSortCanvas');
        const bsCtx = bubbleSortCanvas.getContext('2d');
        let bsArray = Array.from({length: 20}, () => Math.floor(Math.random() * 180) + 10);
        let bsIndex = 0;

        function bubbleSort() {
            if (bsIndex < bsArray.length - 1) {
                for (let j = 0; j < bsArray.length - bsIndex - 1; j++) {
                    if (bsArray[j] > bsArray[j + 1]) {
                        [bsArray[j], bsArray[j + 1]] = [bsArray[j + 1], bsArray[j]];
                    }
                }
                bsIndex++;
            } else {
                bsIndex = 0;
                bsArray = Array.from({length: 20}, () => Math.floor(Math.random() * 180) + 10);
            }
            drawBubbleSort();
        }

        function drawBubbleSort() {
            bsCtx.fillStyle = '#000000';
            bsCtx.fillRect(0, 0, bubbleSortCanvas.width, bubbleSortCanvas.height);
            bsArray.forEach((value, index) => {
                bsCtx.fillStyle = index === bsIndex ? '#FF00FF' : '#00FF00';
                bsCtx.fillRect(index * 14, bubbleSortCanvas.height - value, 12, value);
            });
        }

        // Sine Wave Animation
        const sineWaveCanvas = document.getElementById('sineWaveCanvas');
        const swCtx = sineWaveCanvas.getContext('2d');
        let time = 0;

        function drawSineWave() {
            swCtx.fillStyle = '#000000';
            swCtx.fillRect(0, 0, sineWaveCanvas.width, sineWaveCanvas.height);
            swCtx.beginPath();
            for (let x = 0; x < sineWaveCanvas.width; x++) {
                let y = Math.sin(x * 0.05 + time) * 50 + sineWaveCanvas.height / 2;
                swCtx.lineTo(x, y);
            }
            swCtx.strokeStyle = '#00FF00';
            swCtx.stroke();
            time += 0.1;
        }

        // Solar System Animation
        const solarSystemCanvas = document.getElementById('solarSystemCanvas');
        const ssCtx = solarSystemCanvas.getContext('2d');
        let planets = [
            {radius: 5, orbit: 40, angle: 0, speed: 0.02, color: '#FFA500'},
            {radius: 3, orbit: 65, angle: 0, speed: 0.01, color: '#00FFFF'},
            {radius: 4, orbit: 90, angle: 0, speed: 0.005, color: '#FF0000'}
        ];

        function drawSolarSystem() {
            ssCtx.fillStyle = '#000000';
            ssCtx.fillRect(0, 0, solarSystemCanvas.width, solarSystemCanvas.height);
            
            // Draw sun
            ssCtx.beginPath();
            ssCtx.arc(solarSystemCanvas.width / 2, solarSystemCanvas.height / 2, 15, 0, Math.PI * 2);
            ssCtx.fillStyle = '#FFFF00';
            ssCtx.fill();

            // Draw planets
            planets.forEach(planet => {
                planet.angle += planet.speed;
                let x = Math.cos(planet.angle) * planet.orbit + solarSystemCanvas.width / 2;
                let y = Math.sin(planet.angle) * planet.orbit + solarSystemCanvas.height / 2;
                
                ssCtx.beginPath();
                ssCtx.arc(x, y, planet.radius, 0, Math.PI * 2);
                ssCtx.fillStyle = planet.color;
                ssCtx.fill();

                // Draw orbit
                ssCtx.beginPath();
                ssCtx.arc(solarSystemCanvas.width / 2, solarSystemCanvas.height / 2, planet.orbit, 0, Math.PI * 2);
                ssCtx.strokeStyle = '#003300';
                ssCtx.stroke();
            });
        }

        // Animation loop
        function animate() {
            bubbleSort();
            drawSineWave();
            drawSolarSystem();
            requestAnimationFrame(animate);
        }

        animate();
    </script>
</body>
</html>
