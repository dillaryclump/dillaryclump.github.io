<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>My Retro GitHub Profile</title>
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
</body>
</html>
