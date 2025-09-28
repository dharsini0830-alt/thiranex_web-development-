# thiranex_web-development-
This project demonstrates how to:  Build a small real-world application with front-end web technologies  Use LocalStorage for client-side data persistence  Apply HTML for structure, CSS for styling, and JavaScript for interactivity  Organize a project with clean code and documentation
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weather App</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="app">
    <h1>🌦️ Weather App</h1>
    <div class="search-box">
      <input type="text" id="cityInput" placeholder="Enter city name">
      <button onclick="getWeather()">Search</button>
    </div>
    <div id="weatherResult" class="result-box"></div>
  </div>
  <script src="script.js"></script>
</body>
</html>
body {
  font-family: Arial, sans-serif;
  background: linear-gradient(to right, #74ebd5, #ACB6E5);
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

.app {
  background: #fff;
  padding: 30px;
  border-radius: 15px;
  text-align: center;
  width: 350px;
  box-shadow: 0 4px 10px rgba(0,0,0,0.2);
}

h1 {
  margin-bottom: 20px;
  color: #333;
}

.search-box {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.search-box input {
  flex: 1;
  padding: 10px;
  border-radius: 8px;
  border: 1px solid #ccc;
}

.search-box button {
  padding: 10px 15px;
  border: none;
  background: #4facfe;
  color: white;
  border-radius: 8px;
  cursor: pointer;
  font-weight: bold;
}

.search-box button:hover {
  background: #00f2fe;
}

.result-box {
  margin-top: 20px;
  padding: 15px;
  background: #f8f8f8;
  border-radius: 10px;
  color: #333;
  font-size: 16px;
}
const apiKey = "YOUR_API_KEY"; // 🔑 Replace with your OpenWeather API key

async function getWeather() {
  const city = document.getElementById("cityInput").value;
  const resultBox = document.getElementById("weatherResult");

  if (city === "") {
    resultBox.innerHTML = "⚠️ Please enter a city name.";
    return;
  }

  try {
    const response = await fetch(
      `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric`
    );

    if (!response.ok) {
      throw new Error("City not found");
    }

    const data = await response.json();

    resultBox.innerHTML = `
      <h2>${data.name}, ${data.sys.country}</h2>
      <p>🌡️ Temperature: ${data.main.temp} °C</p>
      <p>☁️ Weather: ${data.weather[0].description}</p>
      <p>💧 Humidity: ${data.main.humidity}%</p>
      <p>🌬️ Wind Speed: ${data.wind.speed} m/s</p>
    `;
  } catch (error) {
    resultBox.innerHTML = "❌ Error: " + error.message;
  }
}