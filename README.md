// This is html file
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>weather </title>
    <link rel="stylesheet" href="index.css">
</head>

<body>
    <div class="card">
        <div class="search">
            <input type="text" placeholder="enter city name" class="input-box">

            <button class="fa-solid fa-magnifying-glass"></button>
        </div>
        <div class="error">
            <p>City Not Fond</p>
        </div>
        <div class="weather" >
            <img src="images/clear.png" alt="weather image" class="weather-icon">
            <h1 class="temp">22°c</h1>
            <h2 class="city">prayagraj</h2>
            <div class="details">
                <div class="col">
                    <img src="images/humidity.png">
                    <div>
                        <p class="humidity">50%</p>
                        <p>humidity</p>
                    </div>
                </div>
                <div class="col">
                    <img src="images/wind.png">
                    <div>
                        <p class="wind">22Km/h</p>
                        <p>Wind speed</p>
                    </div>
                </div>
            </div>
        </div>
    </div>



    <script src="https://kit.fontawesome.com/1e9ced58e2.js" crossorigin="anonymous"></script>
    <script src="index.js"></script>
</body>

</html>

//Tthis is css file

* {
    margin: 0px;
    padding: 0px;
    box-sizing: border-box;
    font-family: 'Poppins', sans-serif;
}

body {
    background-color: #222;
}

.card {
    width: 90%;
    max-width: 470px;
    background: linear-gradient(130deg, #00feba, #5b548a);
    color: #fff;
    margin: 50px auto 0;
    padding: 40px 35px;
    border-radius: 20px;
    text-align: center;

}

.search {
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.search input {
    background: #ebfffc;
    color: #555;
    flex: 1;
    padding: 10px 25px;
    height: 60px;
    border-radius: 30px;
    margin-right: 15px;
    font-size: 18px;
}

.search button {
    background: #ebfffc;
    border-radius: 50%;
    cursor: pointer;
    width: 50px;
    height: 50px;
}

.weather-icon {
    width: 170px;
    margin-top: 20px;
}

.weather h1 {
    font-size: 80px;
    font-weight: 500px;
}

.weather h2 {
    font-size: 45px;
    font-weight: 400px;
    margin-top: -10px;
}

.details {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0px 20px;
    margin-top: 50px;
}

.col {
    display: flex;
    align-items: center;
    text-align: left;
}

.col img {
    width: 40px;
    margin-right: 10px;
}

.humidity,
.wind {
    font-size: 28px;
    margin-top: -6px;
}
.weather{
    display: none;
}
.error{
    font-size: 25px;
    margin-left: 10px;
    margin-top: 10px;
    display: none;
}

//This is javascript file

const api = "a02a531ea1ebc96d408237bf994232a9";
const url = "https://api.openweathermap.org/data/2.5/weather?units=metric&q=";

const searchbox = document.querySelector(".search input");
const searchbtn = document.querySelector(".search button");
const weathericon = document.querySelector(".weather-icon");


async function cheackweather(city) {
    const response = await fetch(url + city + `&appid=${api}`);
    
    var data = await response.json();
    if (response.status == 404) {
        document.querySelector(".error").style.display = "block";
        document.querySelector(".weather").style.display = "none";
    }
    else {
        console.log(data);
        document.querySelector(".city").innerHTML = data.name;
        document.querySelector(".temp").innerHTML = Math.floor(data.main.temp) + "°c";
        document.querySelector(".humidity").innerHTML = data.main.humidity + "%";
        document.querySelector(".wind").innerHTML = data.wind.speed + " Km/h";
        if (data.weather[0].main == "Clouds") {
            weathericon.src = "images/clouds.png";
        }
        else if (data.weather[0].main == "Clear") {
            weathericon.src = "images/clear.png";
        }
        else if (data.weather[0].main == "Drizzle") {
            weathericon.src = "images/drizzle.png";
        }
        else if (data.weather[0].main == "Mist") {
            weathericon.src = "images/mist.png";
        }
        else if (data.weather[0].main == "Snow") {
            weathericon.src = "images/snow.png";
        }
        else if (data.weather[0].main == "Rain") {
            weathericon.src = "images/rain.png";
        }
        document.querySelector(".weather").style.display = "block";
        document.querySelector(".error").style.display = "none";
    }
}

searchbtn.addEventListener("click", () => {

    cheackweather(searchbox.value);
});
