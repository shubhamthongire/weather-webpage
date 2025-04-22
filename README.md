# weather-webpage
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Live Weather</title>
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;600&display=swap" rel="stylesheet">
  <style>
    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      padding: 0;
      font-family: 'Poppins', sans-serif;
      background: linear-gradient(135deg, #74ebd5, #9face6);
      display: flex;
      align-items: center;
      justify-content: center;
      height: 100vh;
      overflow: hidden;
    }

    .weather-container {
      background: rgba(255, 255, 255, 0.15);
      backdrop-filter: blur(20px);
      border-radius: 20px;
      padding: 30px;
      width: 90%;
      max-width: 400px;
      color: #fff;
      box-shadow: 0 8px 32px 0 rgba(0,0,0,0.2);
      text-align: center;
    }

    h1 {
      font-size: 2rem;
      margin-bottom: 20px;
    }

    input {
      padding: 10px 15px;
      border-radius: 10px;
      border: none;
      width: 80%;
      margin-bottom: 10px;
      font-size: 1rem;
    }

    button {
      background-color: #22eff333;
      color: white;
      border: none;
      padding: 10px 20px;
      margin-top: 10px;
      border-radius: 10px;
      cursor: pointer;
      font-weight: 600;
    }

    button:hover {
      background-color: #ffffff55;
    }

    .weather-result {
      margin-top: 20px;
    }

    .weather-icon {
      width: 100px;
      height: 100px;
      margin-bottom: 10px;
    }

    .fade-in {
      animation: fadeIn 0.5s ease-in-out forwards;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>
  <div class="weather-container">
    <h1>🌤 Weather Forecast</h1>
    <input type="text" id="cityInput" placeholder="Enter city..." />
    <button onclick="getWeather()">Check</button>
    <div class="weather-result" id="weather"></div>
  </div>

  <script>
    const apiKey = 'a936134f75ffca22acb9d530db5687ee'; // 

    async function getWeather() {
      const city = document.getElementById('cityInput').value;
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;

      try {
        const res = await fetch(url);
        if (!res.ok) throw new Error("City not found");
        const data = await res.json();

        const iconCode = data.weather[0].icon;
        const iconUrl = `https://openweathermap.org/img/wn/${iconCode}@4x.png`;

        document.getElementById('weather').innerHTML = `
          <div class="fade-in">
            <img src="${iconUrl}" class="weather-icon" alt="Weather icon">
            <h2>${data.name}</h2>
            <p><strong>${data.weather[0].main}</strong> - ${data.weather[0].description}</p>
            <p>🌡 Temp: ${data.main.temp}°C</p>
            <p>💧 Humidity: ${data.main.humidity}%</p>
            <p>🌬 Wind: ${data.wind.speed} m/s</p>
          </div>
        `;
      } catch (err) {
        document.getElementById('weather').innerHTML = `
          <p style="color: #ffcccc;">${err.message}</p>
        `;
      }
    }
  </script>
</body>
</html>
