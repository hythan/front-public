<template>
  <div>
    <Header />
    <Banner />
      <div>
        <div class="col">
          <div class="container-about">
            <div class="container-text">
              <h1 class="maxi-title">Maxiambiental Treinamentos</h1>
              <p class="paragraph">
                A Maxiambiental Treinamentos, empresa especializada em
                treinamentos na área ambiental, foi fundada em Agosto de 2009 e
                tem sede em Curitiba/PR.
              </p>
              <p class="paragraph">
                Através da realização de treinamentos de curta duração o
                objetivo da empresa é proporcionar o aperfeiçoamento do
                conhecimento técnico-prático e científico de profissionais e
                estudantes que atuam ou pretendem atuar na área ambiental.
              </p>
              <p class="paragraph">
                Os treinamentos são ministrados por profissionais altamente
                especializados e qualificados que possuem conhecimentos práticos
                e aplicados. Desta forma, os cursos são realizados de modo a
                proporcionar aos participantes o conhecimento que estes precisam
                para atuar no mercado, podendo assim ampliar as oportunidades de
                trabalho do profissional.
              </p>
              <p class="paragraph">
                O principal público dos treinamentos são Engenheiros Agrônomos,
                Civis, Ambientais, Florestais, Sanitaristas, Biólogos,
                Geógrafos, Geólogos, Químicos, Cartógrafos, Oceanógrafos, e
                ainda Advogados, Economistas e Administradores.
              </p>
              <p class="paragraph">
                A Maxiambiental mantém convênio e parceria com várias
                instituições e já realizou treinamentos em cidades dos Estados
                do Paraná, Santa Catarina, Rio Grande do Sul, São Paulo, Minas
                Gerais, Goiás, Rio de Janeiro, Mato Grosso, Mato Grosso do Sul,
                Espírito Santo, Distrito Federal, Bahia, Pernambuco, Maranhão,
                Alagoas, Rio Grande do Norte, Rondônia, Pará e Amazonas e busca
                constantemente levar os cursos para novas localidades.
              </p>
              <p class="paragraph">
                Em 10 anos de atuação a Maxiambiental já realizou mais de 150
                turmas de cursos na área ambiental em 16 Estados Brasileiros em
                mais de 30 cidades e capacitou mais de 8.000 profissionais nos
                diferentes Estados onde os treinamentos foram realizados.
              </p>
            </div>
            <div class="container-img">
              <img class="img-about" src="~/assets/imgs/banners/banner.webp" />
            </div>
          </div>
          <div class="container-courses">
            <div class="courses">
              <img class="course-img" src="~/assets/imgs/banners/courses.png" alt="">
              <div class="course-content">
                <p class="course-text">Conheça os nossos treinamentos!</p>
                <a href="/courses" class="button-click-here">Clique Aqui</a>
              </div>

            </div>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'IndexPage',
  data() {
    return {
      courses: [],
    }
  },
  mounted() {
    this.$axios.get('courses').then((response) => {
      this.courses = response.data
    })
  },
}
</script>
<style scoped>
.container-about {
  display: flex;
}

.container-text, .container-img {
  width: auto;
}

.container-text {
  background: #b9e85c;
  padding: 20px;
  border-radius: 8px;
  border-top-right-radius: 0;
}

.img-about {
  width: 500px;
  border: 10px solid #b9e85c;
}

.paragraph {
  font-size: 16px;
  font-weight: 400;
  line-height: 24px;
}

.maxi-title {
  font-size: 26px;
  margin-bottom: 10px;
}

.banner-courses {
  height: 300px;
  width: 100%;
}
.courses {
  margin-top: 10px;
}
.course-content {
  position: relative;
  background: #b9e85c;
  top: -185px;
  z-index: 1;
  width: 250px;
  margin: 0 auto;
  padding: 20px;
  border-radius: 8px;
  display: flex;
  align-items: center;
  flex-direction: column;
}

.course-content .course-text {
  font-size: 22px;
  text-align: center;
  font-weight: 700;
  line-height: 36px;
}

.course-img {
  height: 200px;
  width: 100%;
}

.button-click-here {
  background: white;
  height: 40px;
  width: 120px;
  border-radius: 6px;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 16px;
  color: black;
  text-transform: uppercase;
  text-decoration: none;
  font-weight: bold;
}

.button-click-here:hover {
  background: black;
  color: white;
}

@media only screen and (max-width: 600px){
  .container-about {
    flex-direction: column;
  }

  .container-about .container-text {
    order: 2;
  }

   .container-about .container-img {
    order: 1;
  }

  .img-about {
    width: 100%;
    border-top-left-radius: 8px;
    border-top-right-radius: 8px;
  }

  .container-text {
    border-top-left-radius: 0;
  }
}

</style>
