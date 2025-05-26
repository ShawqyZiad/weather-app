# <h1 align="center">Weather App</h1>

<br>

Building a Weather app with JavaScript is an excellent project for beginners. It helps to understand the core basics of the DOM and teaches how to use fetch API, to call and get data from a third-party service.<br>

This is a simple javascript project made with the help of HTML, CSS, and OpenWeather API. We used weather API to fetch data and display it according to the city entered in the search bar.



# Demo of App

![Screenshot (20)](https://user-images.githubusercontent.com/90332218/194750372-b524eec3-5ef9-4f0c-b82b-770ec8850fc1.png)


1. Overview
HTML: Structure of the app (input box, button, display area).

CSS: Styling the app.

JavaScript: Fetching weather data and updating the UI dynamically.

2. Step-by-step Explanation
Step 1: Get an API key
Register at OpenWeatherMap.

Get a free API key to use in your app.

Step 2: HTML Structure
html

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>Weather App</title>
  <link rel="stylesheet" href="styles.css" />
</head>
<body>
  <div class="weather-app">
    <h1>Weather App</h1>
    <input type="text" id="cityInput" placeholder="Enter city name" />
    <button id="getWeatherBtn">Get Weather</button>

    <div id="weatherResult" class="weather-result">
      <!-- Weather data will appear here -->
    </div>
  </div>

  <script src="script.js"></script>
</body>
</html>
Input box for city name.

Button to trigger weather fetch.

Container to show weather results.

Step 3: CSS Styling (styles.css)
css

body {
  font-family: Arial, sans-serif;
  background: linear-gradient(to right, #74ebd5, #ACB6E5);
  color: #333;
  text-align: center;
  padding: 30px;
}

.weather-app {
  background: white;
  padding: 20px;
  border-radius: 10px;
  max-width: 400px;
  margin: auto;
  box-shadow: 0 0 10px rgba(0,0,0,0.1);
}

input {
  padding: 10px;
  font-size: 1rem;
  width: 70%;
  border: 1px solid #ccc;
  border-radius: 5px;
}

button {
  padding: 10px 15px;
  font-size: 1rem;
  margin-left: 10px;
  border: none;
  border-radius: 5px;
  background-color: #3498db;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: #2980b9;
}

.weather-result {
  margin-top: 20px;
  font-size: 1.2rem;
}
Step 4: JavaScript Logic (script.js)
js

const apiKey = 'YOUR_API_KEY_HERE'; // Replace with your OpenWeatherMap API key

document.getElementById('getWeatherBtn').addEventListener('click', () => {
  const city = document.getElementById('cityInput').value.trim();
  if (city === '') {
    alert('Please enter a city name');
    return;
  }
  getWeather(city);
});

function getWeather(city) {
  const weatherResult = document.getElementById('weatherResult');
  weatherResult.innerHTML = 'Loading...';

  fetch(`https://api.openweathermap.org/data/2.5/weather?q=${encodeURIComponent(city)}&appid=${apiKey}&units=metric`)
    .then(response => {
      if (!response.ok) {
        throw new Error('City not found');
      }
      return response.json();
    })
    .then(data => {
      const { name, main, weather } = data;
      weatherResult.innerHTML = `
        <h2>${name}</h2>
        <p>Temperature: ${main.temp} °C</p>
        <p>Condition: ${weather[0].description}</p>
      `;
    })
    .catch(error => {
      weatherResult.innerHTML = `<p style="color: red;">${error.message}</p>`;
    });
}
How it works:
User types a city name and clicks Get Weather.

JavaScript fetches weather data from OpenWeatherMap using the city name.

Displays temperature and weather description.

Handles errors (like invalid city name).
