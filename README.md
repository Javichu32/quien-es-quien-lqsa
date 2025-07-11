# quien-es-quien-lqsa
<!DOCTYPE html>
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
      { nombre: "amador", img: "https://album.mediaset.es/cimg/1000001/2017/02/14/p1.jpg" },
{ nombre: "carmelito", img: "https://pbs.twimg.com/profile_images/918576762346459136/p0x52UDO_400x400.jpg" },
{ nombre: "raluka", img: "https://static.wikia.nocookie.net/seriesspain/images/3/3f/Raluca.jpg/revision/latest?cb=20231218004613&path-prefix=es" },
{ nombre: "kiamba punko", img: "https://static.wikia.nocookie.net/seriesspain/images/3/30/Dibujo.jpg/revision/latest/scale-to-width-down/327?cb=20140208170653&path-prefix=es" },
{ nombre: "esteso", img: "https://pbs.twimg.com/profile_images/2453025677/image_400x400.jpg" },
{ nombre: "izaskun", img: "https://static.wikia.nocookie.net/seriesspain/images/e/e5/Isazkun_Sagastume.jpg/revision/latest?cb=20111112103237&path-prefix=es" },
{ nombre: "julian", img: "https://static.wikia.nocookie.net/miradordemontepinar/images/b/b3/Miradordemontepinar_wiki_Juli%C3%A1n_Pastor.png/revision/latest?cb=20190825135424&path-prefix=es" },
{ nombre: "justi", img: "https://static.wikia.nocookie.net/seriesspain/images/0/0d/Justi0.jpg/revision/latest?cb=20110427215030&path-prefix=es" },
{ nombre: "raquel", img: "https://album.mediaset.es/cimg/1000001/2017/02/14/vr1.jpg" },
{ nombre: "parrales", img: "https://static.wikia.nocookie.net/seriesspain/images/9/99/Rosario.jpg/revision/latest?cb=20111112091309&path-prefix=es" },
{ nombre: "toñin", img: "https://static.wikia.nocookie.net/miradordemontepinar/images/c/c7/Miradordemontepinar_wiki_To%C3%B1%C3%ADn_Recio.png/revision/latest?cb=20190806161330&path-prefix=es" },
{ nombre: "sergio", img: "https://static.wikia.nocookie.net/miradordemontepinar/images/e/e9/Miradordemontepinar_wiki_Sergio_Arias.png/revision/latest?cb=20190823152034&path-prefix=es" },
{ nombre: "vicente", img: "https://cloudfront-eu-central-1.images.arcpublishing.com/diarioas/A3XM4PTIMRBKVPYF4QFDQW32OA.jpg" },
{ nombre: "amigo indignado", img: "https://static.wikia.nocookie.net/seriesspain/images/6/6d/Indignado_15M.png/revision/latest?cb=20130121163407&path-prefix=es" },
{ nombre: "chavela", img: "https://static.wikia.nocookie.net/seriesspain/images/2/26/Chabela.jpg/revision/latest?cb=20110106131332&path-prefix=es" },
{ nombre: "pascual", img: "https://static.wikia.nocookie.net/seriesspain/images/c/c3/Pascual1.png/revision/latest?cb=20110130152820&path-prefix=es" },
{ nombre: "doña fina", img: "https://static.wikia.nocookie.net/seriesspain/images/3/35/Reconciliaciones-emotivos-reencuentros-nuevos-conflictos_MDSIMA20160401_0180_36.jpg/revision/latest?cb=20160406172058&path-prefix=es" },
{ nombre: "agustin", img: "https://static.wikia.nocookie.net/seriesspain/images/f/f0/Agust%C3%ADn_Gordillo_14.jpg/revision/latest?cb=20231226231949&path-prefix=es" },
{ nombre: "marquesa", img: "https://static.wikia.nocookie.net/seriesspain/images/7/78/Victoria_LQSA_14.jpg/revision/latest?cb=20231227110354&path-prefix=es" },
{ nombre: "coque", img: "https://static.wikia.nocookie.net/seriesspain/images/5/50/Coque_9.PNG/revision/latest?cb=20161126233334&path-prefix=es" },
{ nombre: "mathew", img: "https://static.wikia.nocookie.net/seriesspain/images/9/9e/Matthew-JimmyShaw.png/revision/latest?cb=20150504222332&path-prefix=es" },
{ nombre: "padre alejandro", img: "https://static.wikia.nocookie.net/seriesspain/images/4/4d/Padre_Alejandro.jpg/revision/latest?cb=20101003130752&path-prefix=es" },
{ nombre: "manolo72", img: "https://static.wikia.nocookie.net/seriesspain/images/2/22/Manolo72.jpg/revision/latest?cb=20130726145039&path-prefix=es" },
{ nombre: "puri", img: "https://static.wikia.nocookie.net/seriesspain/images/9/9c/Puri.png/revision/latest?cb=20110415174814&path-prefix=es" },
{ nombre: "pizarro", img: "https://s3.ppllstatics.com/elcomercio/www/multimedia/202103/26/media/avecina-1.jpg" },
{ nombre: "el centollo", img: "https://static.wikia.nocookie.net/seriesspain/images/d/d8/El_centollo.png/revision/latest/scale-to-width-down/200?cb=20110227002354&path-prefix=es" },
{ nombre: "gladys", img: "https://static.wikia.nocookie.net/seriesspain/images/e/e3/Gladys.png/revision/latest/scale-to-width-down/190?cb=20110312142958&path-prefix=es" },
{ nombre: "lorena", img: "https://static.wikia.nocookie.net/seriesspain/images/7/75/Lorena.png/revision/latest/scale-to-width-down/180?cb=20111218170415&path-prefix=es" },
{ nombre: "matias", img: "https://static.wikia.nocookie.net/seriesspain/images/6/66/Mat%C3%ADas.png/revision/latest?cb=20110220132336&path-prefix=es" },
{ nombre: "patri", img: "https://static.wikia.nocookie.net/seriesspain/images/7/76/IMG_20191117_173217.jpg/revision/latest/scale-to-width-down/300?cb=20191117163457&path-prefix=es" },
{ nombre: "teodoro", img: "https://static.wikia.nocookie.net/seriesspain/images/7/75/Teodoro.PNG/revision/latest?cb=20161127000449&path-prefix=es" },
{ nombre: "rogelio", img: "https://static.wikia.nocookie.net/seriesspain/images/4/42/Rogelio.jpg/revision/latest?cb=20200220191657&path-prefix=es" },
{ nombre: "la chusa", img: "https://static.wikia.nocookie.net/seriesspain/images/4/46/Chusa_9.png/revision/latest?cb=20161126230208&path-prefix=es" },
{ nombre: "puta digo patu", img: "https://static.wikia.nocookie.net/lista-de-personajes-de-la-que-se-avecina/images/9/90/Padrescrislqsavl9.jpg/revision/latest?cb=20121111161542&path-prefix=es" },
{ nombre: "ongombo", img: "https://static.wikia.nocookie.net/seriesspain/images/4/46/Ongombo.jpg/revision/latest?cb=20231218003950&path-prefix=es" },
{ nombre: "rosana", img: "https://album.mediaset.es/eimg/2019/03/28/5u4M3HxRrZbfIQgKabFFc7.jpg" },
{ nombre: "logi", img: "https://www.hola.com/horizon/original_aspect_ratio/a6b2e5f4996d-lqsa-8-z.jpg" },
{ nombre: "josito", img: "https://image.tmdb.org/t/p/original/rAoO5CEndwBdw80ZOotDgkqZMl0.jpg" },
{ nombre: "francisco javier", img: "https://static.wikia.nocookie.net/seriesspain/images/0/03/Francisco_Pastor_%285%C2%AA_Temp%29.png/revision/latest?cb=20110430233329&path-prefix=es" },
{ nombre: "maxi", img: "https://static.wikia.nocookie.net/seriesspain/images/9/9a/M%C3%A1ximo_Angulo.jpg/revision/latest?cb=20111112103808&path-prefix=es" },
{ nombre: "goya", img: "https://static.wikia.nocookie.net/seriesspain/images/3/3c/Do%C3%B1a_Croqueta.jpg/revision/latest?cb=20111112104803&path-prefix=es" },
{ nombre: "antonio recio", img: "https://album.mediaset.es/cimg/1000001/2017/02/14/r1.jpg" },
{ nombre: "benito", img: "https://static.wikia.nocookie.net/seriesspain/images/f/f5/Snapshot.jpg/revision/latest/scale-to-width-down/960?cb=20210115194152&path-prefix=es" },
{ nombre: "marilyn", img: "https://static.wikia.nocookie.net/seriesspain/images/3/37/Serpiente_%285x06%29.jpg/revision/latest/scale-to-width-down/250?cb=20220515201138&path-prefix=es" },
{ nombre: "nines", img: "https://album.mediaset.es/cimg/1000001/2017/02/14/cris1.jpg?w=1024" },
{ nombre: "fermin", img: "https://static.wikia.nocookie.net/seriesspain/images/7/7e/Fermin_9.png/revision/latest?cb=20161126232012&path-prefix=es" },
{ nombre: "inspectora", img: "https://static.wikia.nocookie.net/seriesspain/images/8/8c/Marisa_%28LQSA%29.PNG/revision/latest/scale-to-width-down/284?cb=20160923141453&path-prefix=es" },
{ nombre: "miguel", img: "https://static.wikia.nocookie.net/lista-de-personajes-de-la-que-se-avecina/images/0/01/Miguel.jpg/revision/latest/scale-to-width-down/217?cb=20130217101837&path-prefix=es" },
{ nombre: "victor", img: "https://static.wikia.nocookie.net/lista-de-personajes-de-la-que-se-avecina/images/4/40/Captura-Un_carnet_de_tonto_un_delincuente_y_un_porno-chacho-cowb_phixr.jpg/revision/latest?cb=20121226094841&path-prefix=es" },
{ nombre: "azucena", img: "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSkhYOvTPKUn-SVvSgpkvkhEMM47S9wX2hB2Q&s" },
{ nombre: "hector", img: "https://pbs.twimg.com/media/CwsVmkvXcAAJANj.jpg" },
{ nombre: "violeta", img: "https://static.wikia.nocookie.net/miradordemontepinar/images/3/31/Miradordemontepinar_wiki_Violeta_Recio.png/revision/latest?cb=20190809135937&path-prefix=es" },
{ nombre: "charo", img: "https://static.wikia.nocookie.net/miradordemontepinar/images/1/19/Miradordemontepinar_wiki_Do%C3%B1a_Charo.png/revision/latest?cb=20190827171511&path-prefix=es" },
{ nombre: "sulleyman", img: "https://static.wikia.nocookie.net/seriesspain/images/d/dc/Sulleyman.jpg/revision/latest?cb=20130619230744&path-prefix=es" }
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
