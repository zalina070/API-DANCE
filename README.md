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
