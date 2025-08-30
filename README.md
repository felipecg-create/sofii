<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Botones con Corazones</title>
  <style>
    body {
      margin: 0;
      padding: 0;
      font-family: Arial, sans-serif;
      height: 100vh;
      display: flex;
      justify-content: center;
      align-items: center;
      background: pink;
      overflow: hidden;
    }

    /* Fondo de corazones animados */
    body::before {
      content: "";
      position: absolute;
      top: 0; left: 0;
      width: 100%; height: 100%;
      background: url('https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQZ1ltBxu9fwnskcJ02q2eusm0mNwbPDNPGOQ&s'); /* imagen de corazón */
      background-size: 100px 100px;
      opacity: 0.2;
      animation: mover 20s linear infinite;
    }

    @keyframes mover {
      0% { background-position: 0 0; }
      100% { background-position: 1000px 1000px; }
    }

    .container {
      position: relative;
      z-index: 2;
      text-align: center;
    }

    .buttons {
      display: grid;
      grid-template-columns: repeat(5, 100px);
      gap: 15px;
      justify-content: center;
      margin-bottom: 30px;
    }

    button {
      padding: 10px;
      border: none;
      border-radius: 10px;
      background-color: #ff4d6d;
      color: white;
      font-weight: bold;
      cursor: pointer;
      transition: transform 0.2s, background 0.2s;
    }

    button:hover {
      background-color: #ff1f4d;
      transform: scale(1.1);
    }

    /* Imagen y texto emergente */
    .popup {
      display: none;
      position: fixed;
      top: 50%; left: 50%;
      transform: translate(-50%, -50%);
      background: white;
      padding: 20px;
      border-radius: 20px;
      box-shadow: 0 0 15px rgba(0,0,0,0.3);
      text-align: center;
      z-index: 10;
    }

    .popup img {
      max-width: 250px;
      border-radius: 15px;
      margin-bottom: 10px;
    }

    .popup p {
      font-size: 18px;
      font-weight: bold;
      color: #ff1f4d;
    }

    .close {
      margin-top: 10px;
      padding: 8px 15px;
      border: none;
      border-radius: 8px;
      background: #ff4d6d;
      color: white;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <div class="container">
    <div class="buttons">
      <button onclick="mostrar(1)">Botón 1</button>
      <button onclick="mostrar(2)">Botón 2</button>
      <button onclick="mostrar(3)">Botón 3</button>
      <button onclick="mostrar(4)">Botón 4</button>
      <button onclick="mostrar(5)">Botón 5</button>
      <button onclick="mostrar(6)">Botón 6</button>
      <button onclick="mostrar(7)">Botón 7</button>
      <button onclick="mostrar(8)">Botón 8</button>
      <button onclick="mostrar(9)">Botón 9</button>
      <button onclick="mostrar(10)">Botón 10</button>
    </div>
  </div>

  <div class="popup" id="popup">
    <img id="popup-img" src="" alt="">
    <p id="popup-text"></p>
    <button class="close" onclick="cerrar()">Cerrar</button>
  </div>

  <script>
    const imagenes = [
      "https://fv5-3.files.fm/thumb_show.php?i=ymfzawgmtt&view&v=1&PHPSESSID=7b4e852cd064525d2e11e5322c2bc16b1746610f.jpg",
      "https://fv5-3.files.fm/thumb_show.php?i=dzxz8btyte&view&v=1&PHPSESSID=7b4e852cd064525d2e11e5322c2bc16b1746610f.jpg",
      "https://fv5-2.files.fm/thumb_show.php?i=pnekrymv9b&view&v=1&PHPSESSID=7b4e852cd064525d2e11e5322c2bc16b1746610f.jpg",
      "https://fv5-2.files.fm/thumb_show.php?i=sx5f9zh9q4&view&v=1&PHPSESSID=7b4e852cd064525d2e11e5322c2bc16b1746610f.jpg",
      "https://fv5-2.files.fm/thumb_show.php?i=tvh789xxpd&view&v=1&PHPSESSID=7b4e852cd064525d2e11e5322c2bc16b1746610f",
      "https://fv5-2.files.fm/thumb_show.php?i=5rbcwhp7rm&view&v=1&PHPSESSID=7b4e852cd064525d2e11e5322c2bc16b1746610f.jpg",
      "https://fv5-2.files.fm/thumb_show.php?i=kd52pxfm8z&view&v=1&PHPSESSID=7b4e852cd064525d2e11e5322c2bc16b1746610f.jpg",
      "https://fv5-2.files.fm/thumb_show.php?i=v85myzf273&view&v=1&PHPSESSID=7b4e852cd064525d2e11e5322c2bc16b1746610f.jpg",
      "https://fv5-2.files.fm/thumb_show.php?i=au68svyqf8&view&v=1&PHPSESSID=7b4e852cd064525d2e11e5322c2bc16b1746610f.jpg",
      "https://fv5-2.files.fm/thumb_show.php?i=wgdtae9vvb&view&v=1&PHPSESSID=7b4e852cd064525d2e11e5322c2bc16b1746610f.jpg"
    ];

    const textos = [
      "te amo tanto que recordar ese dia me llena de alegria ❤️",
      "Eres increíble y el besarte me manda a las estrellas ✨",
      "Siempre contigo 💕",
      "hermosa de ves de blanco y junto a mi🌸",
      "tenerte en mi vida la hace más hermosa,me encantas 😍",
      "me iluminas la vida🌟",
      "llevo tanto amandote que fuiste la primera vez que me habia enamorado 💖",
      "el amarte me a dado lo mejor de mi vida y nunca me voy a rendir amore🌹",
      "Eres mi inspiración,mi fuerza,mi luz,MI TODO 💕",
      "Siempre te voy a amar hasta el dia que me muera
	  💞"
    ];

    function mostrar(i) {
      document.getElementById("popup-img").src = imagenes[i-1];
      document.getElementById("popup-text").innerText = textos[i-1];
      document.getElementById("popup").style.display = "block";
    }

    function cerrar() {
      document.getElementById("popup").style.display = "none";
    }
  </script>
</body>
</html>
