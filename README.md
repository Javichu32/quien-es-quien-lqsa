<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Quién es Quién - LQSA</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background: #f0f0f0;
      margin: 0;
      padding: 20px;
    }
    h1 {
      text-align: center;
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(9, 1fr);
      gap: 10px;
      max-width: 100%;
    }
    .card {
      background: white;
      border: 2px solid #ccc;
      border-radius: 8px;
      overflow: hidden;
      cursor: pointer;
      text-align: center;
      transition: all 0.2s ease;
    }
    .card img {
      width: 100%;
      height: 120px;
      object-fit: cover;
    }
    .card p {
      margin: 0;
      padding: 5px;
      font-size: 14px;
      background: #004d7a;
      color: white;
    }
    .card.tachado {
      opacity: 0.3;
      filter: grayscale(100%);
    }
    .controls {
      text-align: center;
      margin: 20px 0;
    }
    .controls button {
      padding: 10px 20px;
      font-size: 16px;
      background: #004d7a;
      color: white;
      border: none;
      border-radius: 5px;
      cursor: pointer;
    }
  </style>
</head>
<body>
  <h1>Quién es Quién - LQSA</h1>
  <div class="controls">
    <button onclick="resetTablero()">Reiniciar Tablero</button>
  </div>
  <div class="grid" id="tablero"></div>

  <script>
    const personajes = [
{ nombre: "amador", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://album.mediaset.es/cimg/1000001/2017/02/14/p1.jpg") },
{ nombre: "carmelito", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://pbs.twimg.com/profile_images/918576762346459136/p0x52UDO_400x400.jpg") },
{ nombre: "raluka", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/3/3f/Raluca.jpg") },
{ nombre: "kiamba punko", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/3/30/Dibujo.jpg") },
{ nombre: "esteso", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://pbs.twimg.com/profile_images/2453025677/image_400x400.jpg") },
{ nombre: "izaskun", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/e/e5/Isazkun_Sagastume.jpg") },
{ nombre: "julian", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/miradordemontepinar/images/b/b3/Miradordemontepinar_wiki_Juli%C3%A1n_Pastor.png") },
{ nombre: "justi", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/0/0d/Justi0.jpg") },
{ nombre: "raquel", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://album.mediaset.es/cimg/1000001/2017/02/14/vr1.jpg") },
{ nombre: "parrales", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/9/99/Rosario.jpg") },
{ nombre: "toñin", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/miradordemontepinar/images/c/c7/Miradordemontepinar_wiki_To%C3%B1%C3%ADn_Recio.png") },
{ nombre: "sergio", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/miradordemontepinar/images/e/e9/Miradordemontepinar_wiki_Sergio_Arias.png") },
{ nombre: "vicente", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://cloudfront-eu-central-1.images.arcpublishing.com/diarioas/A3XM4PTIMRBKVPYF4QFDQW32OA.jpg") },
{ nombre: "amigo indignado", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/6/6d/Indignado_15M.png") },
{ nombre: "chavela", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/2/26/Chabela.jpg") },
{ nombre: "pascual", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/c/c3/Pascual1.png") },
{ nombre: "doña fina", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/3/35/Reconciliaciones-emotivos-reencuentros-nuevos-conflictos_MDSIMA20160401_0180_36.jpg") },
{ nombre: "agustin", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/f/f0/Agust%C3%ADn_Gordillo_14.jpg") },
{ nombre: "marquesa", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/7/78/Victoria_LQSA_14.jpg") },
{ nombre: "coque", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/5/50/Coque_9.PNG") },
{ nombre: "mathew", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/9/9e/Matthew-JimmyShaw.png") },
{ nombre: "padre alejandro", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/4/4d/Padre_Alejandro.jpg") },
{ nombre: "manolo72", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/2/22/Manolo72.jpg") },
{ nombre: "puri", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/9/9c/Puri.png") },
{ nombre: "pizarro", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://s3.ppllstatics.com/elcomercio/www/multimedia/202103/26/media/avecina-1.jpg") },
{ nombre: "el centollo", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/d/d8/El_centollo.png") },
{ nombre: "gladys", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/e/e3/Gladys.png") },
{ nombre: "lorena", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/7/75/Lorena.png") },
{ nombre: "matias", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/6/66/Mat%C3%ADas.png") },
{ nombre: "patri", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/7/76/IMG_20191117_173217.jpg") },
{ nombre: "teodoro", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/7/75/Teodoro.PNG") },
{ nombre: "rogelio", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/4/42/Rogelio.jpg") },
{ nombre: "la chusa", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/4/46/Chusa_9.png") },
{ nombre: "puta digo patu", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/lista-de-personajes-de-la-que-se-avecina/images/9/90/Padrescrislqsavl9.jpg") },
{ nombre: "ongombo", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/4/46/Ongombo.jpg") },
{ nombre: "rosana", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://album.mediaset.es/eimg/2019/03/28/5u4M3HxRrZbfIQgKabFFc7.jpg") },
{ nombre: "logi", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://www.hola.com/horizon/original_aspect_ratio/a6b2e5f4996d-lqsa-8-z.jpg") },
{ nombre: "josito", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://image.tmdb.org/t/p/original/rAoO5CEndwBdw80ZOotDgkqZMl0.jpg") },
{ nombre: "francisco javier", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/0/03/Francisco_Pastor_%285%C2%AA_Temp%29.png") },
{ nombre: "maxi", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/9/9a/M%C3%A1ximo_Angulo.jpg") },
{ nombre: "goya", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/3/3c/Do%C3%B1a_Croqueta.jpg") },
{ nombre: "antonio recio", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://album.mediaset.es/cimg/1000001/2017/02/14/r1.jpg") },
{ nombre: "benito", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/f/f5/Snapshot.jpg") },
{ nombre: "marilyn", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/3/37/Serpiente_%285x06%29.jpg") },
{ nombre: "nines", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://album.mediaset.es/cimg/1000001/2017/02/14/cris1.jpg") },
{ nombre: "fermin", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/7/7e/Fermin_9.png") },
{ nombre: "inspectora", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/8/8c/Marisa_%28LQSA%29.PNG") },
{ nombre: "miguel", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/lista-de-personajes-de-la-que-se-avecina/images/0/01/Miguel.jpg") },
{ nombre: "victor", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/lista-de-personajes-de-la-que-se-avecina/images/4/40/Captura-Un_carnet_de_tonto_un_delincuente_y_un_porno-chacho-cowb_phixr.jpg") },
{ nombre: "azucena", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSkhYOvTPKUn-SVvSgpkvkhEMM47S9wX2hB2Q&s") },
{ nombre: "hector", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://pbs.twimg.com/media/CwsVmkvXcAAJANj.jpg") },
{ nombre: "violeta", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/miradordemontepinar/images/3/31/Miradordemontepinar_wiki_Violeta_Recio.png") },
{ nombre: "charo", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/miradordemontepinar/images/1/19/Miradordemontepinar_wiki_Do%C3%B1a_Charo.png") },
{ nombre: "sulleyman", img: "https://images.weserv.nl/?url=" + encodeURIComponent("https://static.wikia.nocookie.net/seriesspain/images/d/dc/Sulleyman.jpg") }
    ];

    const tablero = document.getElementById("tablero");

    personajes.forEach(p => {
      const card = document.createElement("div");
      card.className = "card";
      card.onclick = () => card.classList.toggle("tachado");
      card.innerHTML = `
        <img src="${p.img}" alt="${p.nombre}" />
        <p>${p.nombre}</p>
      `;
      tablero.appendChild(card);
    });

    function resetTablero() {
      document.querySelectorAll('.card').forEach(c => c.classList.remove('tachado'));
    }
  </script>
</body>
</html>
