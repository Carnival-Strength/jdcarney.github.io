<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Tempo Run Calculator</title>
<style>
    body {
        font-family: Arial, sans-serif;
        background-color: #000;
        color: #ffd700; /* Gold color */
    }
    .container {
        max-width: 400px;
        margin: 0 auto;
        padding: 20px;
        border: 1px solid #ffd700; /* Gold border */
        border-radius: 5px;
        background-color: #000;
    }
    .input-group {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        margin-bottom: 10px;
    }
    .input-group label {
        margin-bottom: 5px;
    }
    .input-group select {
        width: 100px;
    }
    input[type="number"] {
        width: 100%;
        padding: 10px;
        margin: 5px 0;
        box-sizing: border-box;
    }
    button {
        width: 100%;
        padding: 10px;
        margin: 10px 0;
        background-color: #ffd700; /* Gold background */
        color: #000; /* Black text */
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }
    button:hover {
        background-color: #ffcc00; /* Lighter gold on hover */
    }
    #result {
        font-weight: bold;
    }
</style>
</head>
<body>

<div class="container">
    <h2>Tempo Run Calculator</h2>
    <div class="input-group">
        <label for="distance">Distance:</label>
        <input type="number" id="distance" step="0.01">
    </div>
    <div class="input-group">
        <label for="unit">Unit:</label>
        <select id="unit">
            <option value="miles">Miles</option>
            <option value="kilometers">Kilometers</option>
        </select>
    </div>
    <label for="minutes">Time:</label>
    <input type="number" id="minutes" placeholder="Minutes">
    <input type="number" id="seconds" placeholder="Seconds">
    <button onclick="calculate()">Calculate</button>
    <div id="result"></div>
</div>

<script>
    function calculate() {
        var distance = parseFloat(document.getElementById('distance').value);
        var unit = document.getElementById('unit').value;
        var minutes = parseInt(document.getElementById('minutes').value);
        var seconds = parseInt(document.getElementById('seconds').value);

        if (unit === "miles") {
            // Convert miles to kilometers
            distance *= 1.60934;
        }

        var distanceMeters = distance * 1000; // Convert distance to meters
        var totalTime = (minutes * 60) + seconds;
        var maxAerobicSpeed = distanceMeters / totalTime;
        var tempoRunSpeed = maxAerobicSpeed * 1.3;
        var yardsIn15Seconds = Math.round(tempoRunSpeed * 15 * 1.09361); // Rounding to the nearest yard

        document.getElementById('result').innerText = "Distance for Tempo Run: " + yardsIn15Seconds + " yards";
    }
</script>

</body>
</html>
