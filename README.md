# PRODIGY_WD_02
I have created a code for stopwatch application which implements start, stop, reset, lap functions - using html, css, javascript
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Stopwatch with Lap Times</title>
<link href="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
<style>
body {
    background-image: url(ss.jpg);
    background-repeat: no-repeat;
    background-size: cover;
    font-family: Arial, sans-serif;
    text-align: center;
    background-color: #f0f0f0;
    margin: 0;
    padding: 0;
}

.stopwatch {
    margin: 20px auto;
    padding: 20px;
    background-color: #fff;
    width: 100%;
    max-width: 400px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

.btn {
    margin: 5px;
    padding: 10px 20px;
    font-size: 16px;
    cursor: pointer;
    border: none;
    border-radius: 4px;
    transition: background-color 0.3s ease;
}

#startButton {
    background-color: #28a745;
    color: #fff;
}

#startButton:hover {
    background-color: #218838;
    color: #fff;
}

#lapButton {
    background-color: #007bff;
    color: #fff;
}

#lapButton:hover {
    background-color: #0056b3;
    color: #fff;
}

#stopButton {
    background-color: #dc3545;
    color: #fff;
}

#stopButton:hover {
    background-color: #c82333;
    color: #fff;
}

#resetButton {
    background-color: #ffc107;
    color: #fff;
}

#resetButton:hover {
    background-color: #e0a800;
    color: #fff;
}

.display {
    font-size: 48px;
    margin: 20px 0;
    color: #333;
}

.lap-times {
    list-style-type: none;
    padding: 0;
    margin: 0;
}

.lap-times li {
    margin-bottom: 5px;
    padding: 5px;
    background-color: #e787cf;
    color: black;
    border-radius: 4px;
}
</style>
</head>
<body>
    <h1 style="color: #fff;"><b><i>STOPWATCH</b></i></h1>
<div class="container">
    <div class="stopwatch">
        <div class="controls">
            <button id="startButton" class="btn" onclick="startStopwatch()">Start</button>
            <button id="lapButton" class="btn" onclick="recordLap()" disabled>Lap</button>
            <button id="stopButton" class="btn" onclick="stopStopwatch()" disabled>Stop</button>
            <button id="resetButton" class="btn" onclick="resetStopwatch()">Reset</button>
        </div>
        <div id="display" class="display">00:00:00</div>
        <ul id="lapTimes" class="lap-times"></ul>
    </div>
</div>

<script>
let stopwatchInterval;
let startTime;
let lapCounter = 1;

function startStopwatch() {
    startTime = Date.now() - (lapCounter > 1 ? lapTimes[lapCounter - 2].time : 0);
    stopwatchInterval = setInterval(updateDisplay, 10);
    document.getElementById('startButton').disabled = true;
    document.getElementById('lapButton').disabled = false;
    document.getElementById('stopButton').disabled = false;
}

function stopStopwatch() {
    clearInterval(stopwatchInterval);
    document.getElementById('startButton').disabled = false;
    document.getElementById('stopButton').disabled = true;
}

function resetStopwatch() {
    clearInterval(stopwatchInterval);
    document.getElementById('display').textContent = '00:00:00';
    document.getElementById('startButton').disabled = false;
    document.getElementById('lapButton').disabled = true;
    document.getElementById('stopButton').disabled = true;
    document.getElementById('lapTimes').innerHTML = '';
    lapCounter = 1;
}

function recordLap() {
    let currentTime = Date.now();
    let lapTime = currentTime - startTime;
    let formattedTime = formatTime(lapTime);
    let lapItem = document.createElement('li');
    lapItem.textContent = `Lap ${lapCounter}: ${formattedTime}`;
    document.getElementById('lapTimes').appendChild(lapItem);
    lapCounter++;
}

function updateDisplay() {
    let currentTime = Date.now();
    let elapsedTime = currentTime - startTime;
    let formattedTime = formatTime(elapsedTime);
    document.getElementById('display').textContent = formattedTime;
}

function formatTime(milliseconds) {
    let hours = Math.floor(milliseconds / 3600000);
    let minutes = Math.floor((milliseconds % 3600000) / 60000);
    let seconds = Math.floor((milliseconds % 60000) / 1000);
    let centiseconds = Math.floor((milliseconds % 1000) / 10);
    return `${pad(hours)}:${pad(minutes)}:${pad(seconds)}.${pad(centiseconds)}`;
}

function pad(number) {
    return (number < 10 ? '0' : '') + number;
}
</script>
<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.3/dist/umd/popper.min.js"></script>
<script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js"></script>
</body>
</html>

