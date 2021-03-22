<template>
  <section class="about" v-if="abouts !== ''">
      <div class="column-image" >
        <div class="row-image">
            <div class="tile tile--main">
                <h3 class="tile-title">O nas</h3>
            </div>
            <div class="tile" id="about-tile-image-small">
                <img :src="linkPrefix + abouts[0].image[0].formats.small.url" :alt="abouts[0].image[0].alternativeText">
            </div>
        </div>
        <div class="row-image">
            <div class="tile tile--big" id="about-tile-image-big">
                <img :src="linkPrefix + abouts[0].image[1].formats.small.url" :alt="abouts[0].image[1].alternativeText">
            </div>
        </div>
      </div>
      <div class="column-description" id="aboutDescription">
          <div class="about-dot">
              <div class='dot'>

              </div>
          </div>
          <div class="about-text-box">
              <h2 class="about-title">{{abouts[0].title}}</h2>
              <p class="about-description">{{abouts[0].text}}</p>
          </div>
      </div>
  </section>
</template>

<script>
import aboutsQuery from "~/apollo/queries/home/about"
export default {
    data(){
        return{
            abouts:'',
            linkPrefix: 'http://192.168.1.50:1337'
        }
    },
    apollo:{
        abouts:{
            prefetch:true,
            query: aboutsQuery
        }
    },
}
</script>

<style scoped>
.about{
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    min-height: 40vh;
    width: calc(100% - 10rem);
    max-width: 1300px;
    margin: 8rem auto 4rem auto;

}
.column-image{
    display: flex;
    flex-direction: column;
    width: 100%;
    max-width: 425px;
    margin-bottom: 4rem;
}
.row-image{
    display: flex;
    justify-content: center;
}
.tile{
    width: 100%;
    height: 250px;
    border-radius: 0.8rem;
}
.tile img{
    height: 100%;
    width: 0%;
    object-fit: cover;
    border-radius: 0.8rem;
}
.tile--main{
    display: flex;
    align-items: flex-end;
    justify-content: center;
    margin-right: 0.5rem;
    background-color: #4581B8;
}
.tile-title{
    margin-bottom: 2rem;
    font-size: 1.8rem;
    font-weight: bold;
    color: #ffffff;
    text-transform: uppercase;

}
.tile--big{
    height: 200px;
    margin-top: 0.5rem;
}
.tile-animate-full{
    animation: animate 1s ease forwards;
}
.tile-animate-small{
    animation: animateRevers 1s ease forwards;
}
@keyframes animate {
    0%{
        width: 0;
    }
    100%{
        width: 100%;
    }
}
@keyframes animateRevers {
    0%{
        width: 100%;
    }
    100%{
        width: 0;
    }
}
.column-description{
    position: relative;
    display: flex;
    align-items: center;
    height: 100%;
    min-width: 425px;
    margin-bottom: 4rem;
}
.about-text-box{
    position: relative;
    max-width: 600px;
    padding-left: 4rem;
    padding-right: 4rem;
    border-right: 1px solid #E9E9E9;
}
.about-dot{
    position: absolute;
    top:0;
    right: -2px;
    height: 100%;
    z-index: 3;
}
.dot{
    position:-webkit-sticky;
    position: sticky;
    top:100px;
    width: 6px;
    height: 6px;
    background-color: #4581B8;
    border-radius: 100%;
}
.about-title{
    margin-bottom: 1.5rem;
    font-size: 1.5rem;
    font-weight: bold;
}

    @media screen and (max-width:1000px) {
    .about{
        width: 100%;
        padding: 0 1rem;
    }
    .column-description{
        min-width: auto;
        padding: 0 1rem;
    }
    .about-text-box{
        padding: 0;
        width: calc(100% - 6px);
    }
    .about-dot{
        right: 1rem;
        margin-right: 3px;
    }
    .navbar-logo{
        color: #FFF;
    }
    }
</style>