<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weather Dashboard</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f4f4f9;
      margin: 0;
      padding: 20px;
    }
    h1 {
      text-align: center;
      margin-bottom: 20px;
    }
    .dashboard {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
      gap: 20px;
    }
    .card {
      background: #fff;
      border-radius: 10px;
      box-shadow: 0 4px 10px rgba(0,0,0,0.1);
      padding: 20px;
      text-align: center;
    }
    .temp {
      font-size: 2rem;
      color: #2196F3;
    }
    input {
      padding: 10px;
      border: 1px solid #ccc;
      border-radius: 5px;
      margin-right: 10px;
    }
    button {
      padding: 10px 15px;
      border: none;
      border-radius: 5px;
      background: #2196F3;
      color: white;
      cursor: pointer;
    }
    button:hover {
      background: #1976D2;
    }
    .search-bar {
      text-align: center;
      margin-bottom: 20px;
    }
  </style>
</head>
<body>
  <h1>Weather Dashboard</h1>
  <div class="search-bar">
    <input type="text" id="cityInput" placeholder="Enter city">
    <button onclick="addCity()">Add City</button>
  </div>
  <div class="dashboard" id="dashboard"></div>

  <script>
    const apiKey = "YOUR_API_KEY"; // Replace with your OpenWeatherMap API key
    const dashboard = document.getElementById("dashboard");

    async function fetchWeather(city) {
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`;
      try {
        const response = await fetch(url);
        const data = await response.json();
        if (data.cod === 200) {
          const card = document.createElement("div");
          card.className = "card";
          card.innerHTML = `
            <h3>${data.name}, ${data.sys.country}</h3>
            <p class="temp">${data.main.temp}°C</p>
            <p>${data.weather[0].description}</p>
            <p>Humidity: ${data.main.humidity}%</p>
            <p>Wind: ${data.wind.speed} m/s</p>
          `;
          dashboard.appendChild(card);
        } else {
          alert("City not found!");
        }
      } catch (error) {
        alert("Error fetching weather data");
      }
    }

    function addCity() {
      const city = document.getElementById("cityInput").value.trim();
      if (city) {
        fetchWeather(city);
        document.getElementById("cityInput").value = "";
      }
    }
  </script>
</body>
</html>
