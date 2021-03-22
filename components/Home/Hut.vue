<template>
  <section class="container" v-if="huts !== ''" data-animation-id="hut">
      <div class="column" data-animation-id="hut-content">
            <div class="column-header">
                    <h2 class="hut-title">
                        Wypożycz idealny domek
                    </h2>
                    <p class="hut-subtitle">
                        Zrelaksuj się przy łonie natury  
                    </p>
            </div>
            <ul class="list-hut-info" v-for="hutContent in huts[0].hutContentMainSite" v-bind:key="hutContent.id">
                    <li class="list-hut-info__item"><span class="hut-info-icon"><img :src="linkPrefix + hutContent.icon.url" alt=""></span><p>{{hutContent.description}}</p></li>
            </ul>
            <div class="column-footer">
                <nuxt-link to="/hut" class="column-footer-button">Zobacz ofertę</nuxt-link>
            </div>
      </div>
      <div class="column column--image" data-animation-id="hut-image">
          <div class="hut-box hut-box--big">
              <picture class="hut-image hut-image--big">
                  <img :src="linkPrefix+huts[0].imagesMainSite[0].formats.small.url" alt="">
              </picture>
          </div>
          <div class="hut-box hut-box--small">
              <picture class="hut-image hut-image--small">
                  <img :src="linkPrefix+huts[0].imagesMainSite[1].formats.small.url" alt="">
              </picture>
              <picture class="hut-image hut-image--small">
                  <img :src="linkPrefix+huts[0].imagesMainSite[2].formats.small.url" alt="">
              </picture>
          </div>
      </div>
  </section>
</template>

<script>
import hutQuery from '~/apollo/queries/home/hut'
export default {
    data(){
        return{
            huts:'',
            linkPrefix: 'http://192.168.1.50:1337'
        }
    },
    apollo:{
        huts:{
            prefetch: true,
            query: hutQuery
        }
    },
}
</script>

<style scoped>
.container{
    display: grid;
    grid-template-columns: repeat(2,1fr);
    grid-gap: 1rem;
    justify-items: center;
    max-width: 1300px;
    width: calc(100% - 10rem);
    min-height: 100vh;
    padding: 7rem 0;
    margin:0 auto;
}
.column{
    display: flex;
    flex-direction: column;
    text-transform: uppercase;
}
.column-header{
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    margin-bottom: 7rem;
}
.hut-title{
    margin-bottom: 1rem;
    font-size: 2rem;
    font-weight: bold;
    text-align: center;
}
.list-hut-info{
    width: 100%;
}
.list-hut-info__item{
    display: flex;
    align-items: center;
    width: 100%;
    min-height: 50px;
    padding: 0 2rem;
    margin-bottom: 2rem;
    border-radius: 15px;
    font-size: 0.82rem;
    background-color: #F5F5F5;
}
.hut-info-icon{
    width: 20px;
    height: 20px;
    margin-right: 1rem;
}
.hut-info-icon img{
    width: 100%;
    height: 100%;
}
.column-footer{
    margin-top: 3rem;
}
.column-footer-button{
    display: flex;
    justify-content: center;
    align-items: center;
    height: 60px;
    width: 100%;
    max-width: 280px;
    background-color: #005492;
    color:#FFF;
    font-weight: bold;
    font-size: 0.9rem;
    border-radius: 15px;
}
.hut-box{
    position: relative;
    width: 100%;
    height: 100%;
}
.hut-box--big{
    width: calc(100% - 0.5rem);
    max-height: 400px;
    margin: 0 auto;
}
.hut-box--small{
    display: flex;
    justify-content: space-between;
    max-height: 220px;
    margin-top: 1rem;
}
.hut-image img{
    width: 100%;
    height: 100%;
    object-fit:cover;
    background-color: red;
    border-radius: 15px;
}
.hut-image--small{
    display: flex;
    justify-content: center;
}
.hut-image--small img{
    width: calc(100% - 0.5rem);
}

@media screen and (max-width:1100px) {
    .hut-box--big{
        max-height: 300px;
    }
}
@media screen and (max-width:900px) {
    .container{
        display: flex;
        flex-direction: column-reverse;
        width: calc(100% - 2rem);
    }
    .column--image{
        margin-bottom: 3rem;
    }
    .hut-box--big{
        max-height: none;
    }
    .column-header{
        margin-bottom: 1.5rem;
    }
    .column-footer{
        display: flex;
        justify-content: center;
    }
}
</style>