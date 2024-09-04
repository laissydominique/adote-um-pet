<script setup>
import { ref, onMounted } from "vue";

const dataDogs = ref({
  id: null,
  dogs: [],
});

const dataCats = ref({
  id: null,
  cats: [],
});

const descriptionsDog = [
  "Olá, sou o Max! Tenho 2 aninhos e sou um verdadeiro companheiro. Adoro passeios no parque e sonecas no sofá. Estou à procura de uma família que me dê muito carinho e amor, e que esteja pronta para compartilhar muitos momentos felizes ao meu lado!",

  "Oi, eu sou a Luna! Sou uma cadelinha de 3 anos, cheia de energia e amor para dar. Gosto de correr e brincar com meus brinquedos favoritos. Se você está buscando uma amiga leal e carinhosa, venha me conhecer!",

  "Olá, meu nome é Toby! Tenho 4 anos e sou super tranquilo e afetuoso. Adoro receber carinhos e fazer companhia. Estou em busca de um lar onde eu possa relaxar e ser amado todos os dias. Vamos ser amigos?",

  "Oi, eu sou a Bella! Tenho 1 aninho e sou uma cachorrinha alegre e amorosa. Gosto de brincar e aprender coisas novas. Procuro uma família que me dê muito amor e atenção, e que esteja disposta a explorar o mundo comigo!",

  "Olá, sou o Charlie! Tenho 2 anos e sou um cãozinho carinhoso e obediente. Adoro fazer novas amizades e brincar com meus humanos. Se você procura um amigo fiel e divertido, estou aqui esperando por você!",

  "Oi, eu sou a Daisy! Tenho 5 anos e sou uma cachorrinha adorável e tranquila. Gosto de passeios relaxantes e de receber carinho. Estou procurando uma família que me ofereça um lar caloroso e cheio de amor!",

  "Olá, meu nome é Rocky! Tenho 3 anos e sou cheio de energia e alegria. Gosto de correr e brincar ao ar livre. Se você está procurando um cãozinho ativo e divertido, venha me conhecer e vamos brincar juntos!",

  "Oi, eu sou a Zoe! Sou uma cachorrinha de 2 anos que adora companhia e carinho. Sou muito leal e gosto de estar perto das pessoas. Procuro um lar onde eu possa ser parte da família e receber muito amor!",

  "Olá, sou o Buddy! Tenho 4 anos e sou um cachorro tranquilo e adorável. Gosto de relaxar e passar tempo com meus humanos. Se você está procurando um amigo leal e carinhoso, eu sou o cãozinho perfeito para você!",

  "Oi, eu sou a Rosie! Tenho 1 ano e sou uma cadelinha meiga e carinhosa. Adoro brincar e receber afeto. Procuro uma família que possa me dar muito amor e que esteja pronta para compartilhar muitos momentos especiais ao meu lado!",
];

const descriptionsCat = [
  "Olá, meu nome é Felix! Tenho 3 anos e sou um gato calmo e carinhoso. Adoro receber carinho e passar tempo ao sol. Estou à procura de um lar onde eu possa relaxar e ser amado. Venha me conhecer!",

  "Oi, eu sou a Mia! Tenho 2 anos e sou uma gatinha cheia de energia e curiosidade. Gosto de explorar e brincar com meus brinquedos. Se você está procurando uma amiga divertida e afetuosa, eu sou a gatinha perfeita!",

  "Olá, sou o Leo! Tenho 4 anos e sou um gato tranquilo e sociável. Gosto de receber carinho e me aninhar no sofá. Procuro uma família que me dê muito amor e um lugar confortável para chamar de lar.",

  "Oi, eu sou a Luna! Sou uma gatinha de 1 ano, meiga e carinhosa. Adoro brincar e receber atenção. Estou procurando uma família que me ofereça muito afeto e que esteja pronta para explorar a vida comigo!",

  "Olá, sou o Oliver! Tenho 5 anos e sou um gato calmo e afetuoso. Gosto de relaxar e ser o centro das atenções. Se você está procurando um gato leal e carinhoso, venha me conhecer!",

  "Oi, eu sou a Bella! Tenho 2 anos e sou uma gatinha alegre e brincalhona. Gosto de correr e brincar com meus brinquedos favoritos. Estou em busca de uma família que me dê muito amor e diversão!",

  "Olá, sou o Max! Tenho 4 anos e sou um gato tranquilo e observador. Adoro ficar no colo e receber carinho. Procuro um lar onde eu possa ser parte da família e desfrutar de muitos momentos agradáveis.",

  "Oi, eu sou a Daisy! Tenho 3 anos e sou uma gata carinhosa e leal. Gosto de ficar perto das pessoas e receber afeto. Estou procurando uma família que me ofereça muito amor e um lar caloroso.",

  "Olá, sou o Rocky! Tenho 1 ano e sou um gato cheio de energia e curiosidade. Adoro brincar e explorar novos lugares. Se você está procurando um amigo divertido e ativo, venha me conhecer!",

  "Oi, eu sou a Zoe! Tenho 2 anos e sou uma gatinha adorável e meiga. Gosto de receber carinho e fazer companhia. Procuro uma família que possa me dar muito amor e atenção, e que esteja pronta para me acolher com carinho!",
];

async function getDog() {
  try {
    const response = await fetch(
      `https://dog.ceo/api/breed/hound/images/random/10`
    );
    const data = await response.json();

    for (const dog of data.message) {
      dataDogs.value.dogs.push({
        imgDog: dog,
      });
    }
  } catch (error) {
    `<p>Não foi possível completar a requisição</p>`;
  }
}

async function getCat() {
  try {
    const response = await fetch(
      `https://api.thecatapi.com/v1/images/search?limit=10`
    );
    const data = await response.json();

    for (const cat of data) {
      dataCats.value.cats.push({
        imgCat: cat.url,
      });
    }
  } catch (error) {
    `<p>Não foi possível completar a requisição</p>`;
  }
}

function getDescriptionDog(descriptionsDog) {
  for (let i = descriptionsDog.length - 1; i > 0; i--) {
    const item = Math.floor(Math.random() * (i + 1));

    [descriptionsDog[i], descriptionsDog[item]] = [
      descriptionsDog[item],
      descriptionsDog[i],
    ];
  }

  return descriptionsDog;
}

function getDescriptionCat(descriptionsCat) {
  for (let i = descriptionsCat.length - 1; i > 0; i--) {
    const item = Math.floor(Math.random() * (i + 1));

    [descriptionsCat[i], descriptionsCat[item]] = [
      descriptionsCat[item],
      descriptionsCat[i],
    ];
  }

  return descriptionsDog;
}

function scrollTo(id) {
  const element = document.getElementById(id);
  if (element) {
    element.scrollIntoView({ behavior: "auto" });
  }
}

onMounted(() => {
  getDog();
  getCat();
  getDescriptionDog(descriptionsDog);
  getDescriptionCat(descriptionsCat);
});
</script>
<template>
  <div class="container">
    <header>
      <div class="icon">
        <img src="../src/image.png" alt="" srcset="" width="75rem" />
        <div class="txt-icon">
          <p>Adote um Pet</p>
          <p class="subtitle">
            Transforme uma vida e encontre um amor incondicional
          </p>
        </div>
      </div>
      <nav>
        <div class="paths animate__animated animate__backInLeft">
          <a @click="scrollTo('title-dogs')"><p>Cachorros</p></a>
          <a @click="scrollTo('title-cats')"><p>Gatos</p></a>
          <a @click="scrollTo('know-more-title')"><p>Fale conosco</p></a>
        </div>
      </nav>
    </header>
    <div class="content">
      <div class="title-dogs" id="title-dogs">
        <div class="one"></div>
        <h1 class="animate__animated animate__backInDown">CACHORROS</h1>
        <div class="two"></div>
      </div>
      <div class="content-dogs">
        <div class="allDogs">
          <div
            class="imagensDogs"
            id="imagensDogs"
            v-for="(item, index) in dataDogs.dogs">
            <div class="imagemDog">
              <img
                :src="item.imgDog"
                alt=""
                srcset=""
                width="360rem"
                height="345rem"/>
            </div>
            <div class="nome">
              <p>{{ descriptionsDog[index] }}</p>
            </div>
          </div>
        </div>
      </div>
      <div class="test">
        <div class="title-cats" id="title-cats">
          <div class="one"></div>
          <h1 class="dog animate__animated animate__backInDown">GATOS</h1>
          <div class="two"></div>
        </div>
      </div>
      <div class="content-cats">
        <div class="allCats">
          <div
            class="imagensCats"
            id="imagensCats"
            v-for="(item, index) in dataCats.cats"
            :key="item">
            <div class="imagemCat">
              <img
                :src="item.imgCat"
                alt="Imagem Gato"
                srcset=""
                width="360rem"
                height="345rem"/>
            </div>
            <div class="nome">
              <p>{{ descriptionsCat[index] }}</p>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="know-more">
      <div class="know-more-title" id="know-more-title">
        <div class="one"></div>
        <h1>CONTATOS</h1>
        <div class="two"></div>
      </div>
      <div class="contacts">
        <div class="email">
          <i class="far fa-envelope"></i> ficticio@adoteumpet.com
        </div>
        <div class="phone"><i class="fas fa-phone"></i>(00) 99999-9999</div>
        <div class="instagram">
          <i class="fab fa-instagram"></i>ficticioadoteumpet
        </div>
      </div>
    </div>
    <footer>
      <div class="footer">
        <div class="ass"><p>Desenvolvido por: Laissy Dominique</p></div>
      </div>
    </footer>
  </div>
</template>
