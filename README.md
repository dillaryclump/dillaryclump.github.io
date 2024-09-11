<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Retro GitHub Profile with Snake Game</title>
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
        .blink {
            animation: blinker 1s linear infinite;
        }
        @keyframes blinker {
            50% { opacity: 0; }
        }
        .marquee {
            width: 100%;
            overflow: hidden;
            background: #0000FF;
            color: #FFFF00;
        }
        .marquee span {
            display: inline-block;
            width: max-content;
            padding-left: 100%;
            animation: marquee 15s linear infinite;
        }
        @keyframes marquee {
            0%   { transform: translate(0, 0); }
            100% { transform: translate(-100%, 0); }
        }
        #gameCanvas {
            border: 2px solid #00FF00;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <h1>Welcome to My GitHub Profile!</h1>
    <p class="rainbow-text">Coding like it's 1999!</p>
    <p class="blink">Check out my repositories below</p>
    <div class="marquee">
        <span>Thanks for visiting my profile! Star my repos if you like them!</span>
    </div>
    <p>
        <img src="/api/placeholder/88/31" alt="Under Construction">
    </p>
    <h2>Play Snake Game!</h2>
    <canvas id="gameCanvas" width="300" height="300"></canvas>
    <p>Use arrow keys to control the snake. Eat the food to grow!</p>

    <script>
        const canvas = document.getElementById('gameCanvas');
        const ctx = canvas.getContext('2d');
        
        const scale = 10;
        const rows = canvas.height / scale;
        const columns = canvas.width / scale;
        
        let snake;
        
        (function setup() {
            snake = new Snake();
            fruit = new Fruit();
            fruit.pickLocation();
            
            window.setInterval(() => {
                ctx.clearRect(0, 0, canvas.width, canvas.height);
                fruit.draw();
                snake.update();
                snake.draw();
                
                if (snake.eat(fruit)) {
                    fruit.pickLocation();
                }
                
                snake.checkCollision();
            }, 250);
        }());
        
        window.addEventListener('keydown', ((evt) => {
            const direction = evt.key.replace('Arrow', '');
            snake.changeDirection(direction);
        }));
        
        function Snake() {
            this.x = 0;
            this.y = 0;
            this.xSpeed = scale * 1;
            this.ySpeed = 0;
            this.total = 0;
            this.tail = [];
            
            this.draw = function() {
                ctx.fillStyle = "#FFFFFF";
                for (let i=0; i<this.tail.length; i++) {
                    ctx.fillRect(this.tail[i].x, this.tail[i].y, scale, scale);
                }
                
                ctx.fillRect(this.x, this.y, scale, scale);
            }
            
            this.update = function() {
                for (let i=0; i<this.tail.length - 1; i++) {
                    this.tail[i] = this.tail[i+1];
                }
                
                this.tail[this.total - 1] = { x: this.x, y: this.y };
                
                this.x += this.xSpeed;
                this.y += this.ySpeed;
                
                if (this.x > canvas.width) {
                    this.x = 0;
                }
                if (this.y > canvas.height) {
                    this.y = 0;
                }
                if (this.x < 0) {
                    this.x = canvas.width;
                }
                if (this.y < 0) {
                    this.y = canvas.height;
                }
            }
            
            this.changeDirection = function(direction) {
                switch(direction) {
                    case 'Up':
                        this.xSpeed = 0;
                        this.ySpeed = -scale * 1;
                        break;
                    case 'Down':
                        this.xSpeed = 0;
                        this.ySpeed = scale * 1;
                        break;
                    case 'Left':
                        this.xSpeed = -scale * 1;
                        this.ySpeed = 0;
                        break;
                    case 'Right':
                        this.xSpeed = scale * 1;
                        this.ySpeed = 0;
                        break;
                }
            }
            
            this.eat = function(fruit) {
                if (this.x === fruit.x && this.y === fruit.y) {
                    this.total++;
                    return true;
                }
                return false;
            }
            
            this.checkCollision = function() {
                for (let i=0; i<this.tail.length; i++) {
                    if (this.x === this.tail[i].x && this.y === this.tail[i].y) {
                        this.total = 0;
                        this.tail = [];
                    }
                }
            }
        }
        
        function Fruit() {
            this.x;
            this.y;
            
            this.pickLocation = function() {
                this.x = (Math.floor(Math.random() * columns - 1) + 1) * scale;
                this.y = (Math.floor(Math.random() * rows - 1) + 1) * scale;
            }
            
            this.draw = function() {
                ctx.fillStyle = "#FF0000";
                ctx.fillRect(this.x, this.y, scale, scale)
            }
        }
    </script>
</body>
</html>
