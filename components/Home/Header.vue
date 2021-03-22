<template>
  <header class="home-header" v-if="headers !== ''">
      <div class="home-header__column-text">
          <div class="header-column">
                <h2 class="home-header-title">{{headers[0].Title}}</h2>
                <p class="home-header-lead">
                    {{headers[0].Text}}
                </p>
                <a href="tel:696599556" class="home-header-button">Zadzwoń</a>
          </div>
      </div>
      <div class="home-header__column-image">
              <picture>
                  <img class="header-image"  alt="Ładowanie..." id="header-image">
              </picture>
      </div>
  </header>
</template>

<script>
import headerQuery from '../../apollo/queries/home/header'
export default {
    data(){
        return{
            headers:'',
            imageID:0,
            linkPrefix: 'http://192.168.1.50:1337'
        }
    },
    apollo: {
        headers:{
            prefetch: true,
            query: headerQuery
        }
    },
    methods:{
        changeImage(){
            let imageBox = document.querySelector('#header-image')
            imageBox.src= this.linkPrefix + this.headers[0].image[this.imageID].formats.large.url

            setInterval(()=>{
                imageBox.classList.add('header-image--animation')
                this.imageID = (this.imageID == 0)? 1 : 0;
                imageBox.src= this.linkPrefix + this.headers[0].image[this.imageID].formats.large.url
                imageBox.alt = this.headers[0].image[this.imageID].alternativeText
            },5000)
        }
    },
    mounted() {
        if(this.headers !== ''){
            this.changeImage();
        }
    },
}
</script>

<style scoped>
    .home-header{
        position: relative;
        display: flex;
        flex-wrap: wrap;
        width: 100%;
        height: 100vh;
    }
    .home-header__column-text{
        position: absolute;
        left: 50%;
        bottom: 0px;
        display: flex;
        flex-direction: column;
        width: calc(100% - 10rem);
        max-width: 1300px;
        margin-bottom: 10rem;
        transform: translateX(-50%);
        transition: 1s ease all;
        z-index: 4;
        animation: textFromLeftToRight 1.2s ease-in;
    }
    @keyframes textFromLeftToRight{
        0%{
            opacity: 0;
            left:-25%;
        }
        80%{
            opacity: 0;
        }
        100%{
            opacity: 1;
            left: 50%;
            bottom:0px;
        }
    }
    .header-column{
        width: 100%;
        max-width: 340px;
    }
    .home-header-title{
        font-size: 2.5rem;
        font-weight: bold;
        line-height: 100%;
        margin-bottom: 1.5rem;
        text-transform: uppercase;
    }
    .home-header-lead{
        line-height: 150%;
        margin-bottom: 4rem;
        text-transform: uppercase;
    }
    .home-header-button{
        padding: 0.5rem 2rem;
        border:1px solid #000;
        border-color: #000;
        transition: 1s ease border-color;
        border-radius: 2rem;
    }
    .home-header__column-image{
        position: absolute;
        height: 100vh;
        width: 55%;
        right:0;
        transition: 1s ease all;
    }
    .header-image{
        position: relative;
        height: 100%;
        width: 100%;
        object-fit: cover;
    }
    .header-image--animation{
        animation: fadeImage 5s ease-in infinite;

    }
    @keyframes fadeImage {
        0%{
            opacity: 0;
        }
        20%{
            opacity: 1;
        }
        50%{
            opacity: 1;
        }
        80%{
            opacity: 1;
        }
        100%{
            opacity: 0;
        }
    }
    @media screen and (max-width:1000px) {
        .home-header__column-image{
            width: 100%;
        }
        .home-header__column-image::after{
            content: '';
            position: absolute;
            top:0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.26);
        }
        .home-header__column-text{
            color:#FFF;
        }
        .home-header-button{
            border-color: #FFF;
        }
    }
</style>