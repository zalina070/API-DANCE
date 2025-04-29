<!DOCTYPE html>
<html lang="ru">

<head>
    <meta charset="UTF-8" />
    <title>Поиск Танцевальных Картинок</title>
    <link rel="stylesheet" href="api.css">
</head>

<body>
    <h1>Dance picture</h1>

    <input type="text" id="customDance" placeholder="Введите стиль танца" />

    <br />

    <select id="danceSelect">
    <option value="">-- Выберите стиль из списка --</option>
    <option value="Ballet">Балет</option>
    <option value="Hip hop dance">Хип-хоп</option>
    <option value="Breakdance">Брейк-данс</option>
    <option value="Salsa dance">Сальса</option>
    <option value="Contemporary dance">Контемп</option>
    <option value="Tango">Танго</option>
    <option value="Waltz">Вальс</option>
    <option value="Flamenco">Фламенко</option>
  </select>

    <br />

    <button onclick="searchImages()">Найти</button>
    <button onclick="randomDance()">Рандом</button>

    <div id="images"></div>
    <script src="api.js"></script>
</body>

</html>
body {
    text-align: center;
    padding: 30px;
    font-family: 'Arial', sans-serif;
    background: linear-gradient(135deg, #FDC830 0%, #F37335 100%);
}

h1 {
    font-size: 36px;
    margin-bottom: 20px;
}

input,
select,
button {
    padding: 10px;
    font-size: 18px;
    margin: 10px;
    border-radius: 8px;
    border: 2px solid #555;
}

button {
    background-color: #ff7e5f;
    color: white;
    border: none;
    cursor: pointer;
}

button:hover {
    background-color: #feb47b;
}

#images {
    margin-top: 30px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 20px;
}

img {
    width: 350px;
    height: 350px;
    object-fit: cover;
    border-radius: 15px;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
    transition: transform 0.3s;
}

img:hover {
    transform: scale(1.05);
}

// Функция для поиска изображений по танцевальному стилю
async function searchImages(randomOne = false) {
    const select = document.getElementById("danceSelect");
    const input = document.getElementById("customDance");

    let query = input.value || select.value;

    if (!query) {
        alert("Please enter or select a dance style!");
        return;
    }

    const apiKey = "F_vHuLfFcEBDIbzCeh06HkfAC4EWaEcSQsUinVzU-E8";
    const count = randomOne ? 1 : 9;
    const url = `https://api.unsplash.com/search/photos?query=${encodeURIComponent(query)}&client_id=${apiKey}&per_page=${count}`;

    try {
        // Запрос к API Unsplash для поиска изображений
        const response = await fetch(url);
        const data = await response.json();

        const imagesDiv = document.getElementById("images");
        imagesDiv.innerHTML = ""; // Очищаем контейнер для новых изображений
        if (data.results.length === 0) {
            imagesDiv.innerHTML = "<p>No images found 😢</p>"; // Если картинок не найдено
            return;
        }

        // Создаём элементы <img> для каждой найденной картинки
        data.results.forEach((photo) => {
            const img = document.createElement("img");
            img.src = photo.urls.regular;
            img.alt = query;
            imagesDiv.appendChild(img);
        });
    } catch (error) {
        console.error("Error fetching images:", error);
        alert("Something went wrong while fetching the images. Please try again later.");
    }
}

// Функция для случайного выбора танца из списка
function randomDance() {
    const dances = [
        "Ballet",
        "Hip hop dance",
        "Breakdance",
        "Salsa dance",
        "Contemporary dance",
        "Tango",
        "Waltz",
        "Flamenco"
    ];
    const random = dances[Math.floor(Math.random() * dances.length)];

    document.getElementById("danceSelect").value = random;
    document.getElementById("customDance").value = "";

    searchImages(true); // true — чтобы показать только одну картинку
}

// Автоматический поиск при нажатии клавиши Enter в поле ввода
document.addEventListener("DOMContentLoaded", () => {
    document
        .getElementById("customDance")
        .addEventListener("keydown", function(e) {
            if (e.key === "Enter") {
                searchImages(); // Выполняем поиск при нажатии Enter
            }
        });
});
