<template>
  <div class="light">
    <Header />
    <section id="portCont">
      <div class="container">
        <div class="wrap__title">
          <h2><strong>portfolio</strong><em>Site</em></h2>
        </div>
        <div class="port__cont">
          <div class="port" v-for="port in ports" :key="port.id">
            <a :href="port.link" target="_blank">
              <div class="pImg">
                <img :src="port.image" :alt="port.title" />
              </div>
              <div class="pText">
                <h3>{{port.title}}</h3>
                <p>{{port.category}}</p>
              </div>
            </a>
          </div>
        </div>
      </div>
    </section>
    <Footer />
    <ContInfo />
  </div>
</template>

<script>
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
import ContInfo from "@/components/ContInfo.vue";
import { ref } from 'vue';

export default {
  components: {
    Header,
    Footer,
    ContInfo,
  },

  setup(){
    const ports = ref([])

    const Portfolios = () => {
      fetch(
        'https://webstoryboy.github.io/react5001/src/assets/json/portfolio.json'
      )
      .then((response) => response.json())
      .then((data) => {
        // console.log(data.data.ports);
        ports.value = data.data.ports;
      })
    };

     setTimeout(() => {
      Portfolios();
    }, 2000);

    return {
      ports,
      Portfolios,
  };
},


};
</script>

<style lang="scss">
#portCont {
  background-color: #000;
  color: #fff;
}
.port__cont {
  color: #fff;
  width: 100%;
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  padding-bottom: 300px;

  .port {
    width: 32%;
    margin-bottom: 2%;
    
    .pText {
      padding: 35px;
      background: #151517;

      h3 {
        font-family: "saol";
        font-size: 50px;
        line-height: 47px;
      }
      p {
        font-size: 12px;
        color: #b0aead;
      }
    }
  }
}
.light #portCont {
  background-color: #f0eeeb;
  color: #000;
}
</style>
