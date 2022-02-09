# weather_app
 javascript Weather App
 
 <h3><i> you can <a href="https://admiralanne-js-weather.netlify.app/" target="_blank"> click me</a> To view the app. </a></i></h3>

<li>You can get your openweathermap API from [HERE](https://openweathermap.org/)</li><br>

We create a function called 'fetchWeather' _city_ as the parameter-- which fetches a URL --in this case, our weatherApiURL.
we get a JSON file with required weather information.
<li>q="+city" --so that we can fetch data of Any city we want!</li><br>

```js
apiKey: "YOUR API GOES HERE",
    fetchWeather: function (city) {
      fetch(
        "https://api.openweathermap.org/data/2.5/weather?q=" +
          city +
          "&units=metric&appid=" +
          this.apiKey
      )
        .then((response) => {
          if (!response.ok) {
            alert("No weather found.");
            throw new Error("No weather found.");
          }
          return response.json();
        })
        .then((data) => this.displayWeather(data));
    },
```

We create a function displayWeather --for the same purpose as named.
Paramater is-- "data" <br>
<li>GET as const--- name, describtion, icon,temp,humidity,speed etc~ as **variables**</li><br>
<li>documnet.QuerySelector-- to Display the information on the page-- replace necessary data in html. </li><br>


```js
displayWeather: function (data) {
      const { name } = data;
      const { icon, description } = data.weather[0]; //since we are dealing with an array--check JSON
      const { temp, humidity } = data.main;
      const { speed } = data.wind;
      document.querySelector(".city").innerText = "Weather in " + name;
      document.querySelector(".icon").src =
        "https://openweathermap.org/img/wn/" + icon + ".png";
      document.querySelector(".description").innerText = description;
      document.querySelector(".temp").innerText = temp + "°C";
      document.querySelector(".humidity").innerText =
        "Humidity: " + humidity + "%";
      document.querySelector(".wind").innerText =
        "Wind speed: " + speed + " km/h";
      document.querySelector(".weather").classList.remove("loading");
      document.body.style.backgroundImage =
        "url('https://source.unsplash.com/1600x900/?" + name + "')";
    },
```

<li>querySelector -- on search-bar. Get information inserted and pass it to the function~ what function? The fetchWeather function, you dumbass~ </li>

```js
search: function () {
      this.fetchWeather(document.querySelector(".search-bar").value);
    },
  };
  
  document.querySelector(".search button").addEventListener("click", function () {
    weather.search();
  });
  
  document
    .querySelector(".search-bar") //when you press enter, it searches the City
    .addEventListener("keyup", function (event) {
      if (event.key == "Enter") {
        weather.search();
      }
    });
```

<li>to display a city when you load the site-- just a minor detail</li><br>

```js
weather.fetchWeather("Dimapur");
```

