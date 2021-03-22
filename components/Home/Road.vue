<template>
  <section class="container container--road" :style="'background-image: url(' + linkPrefix + roadContent.roads_content[0].image.formats.small.url +')'" id="road" v-if="roadContent !== ''">
      <div class="road-layout">
            <div class="road-header">
                <h2 class="title">Trasy, Rzeki, Jeziora</h2>

            </div>
            <div class="road-container">
                    <ul class="road-list">
                        <li class="road-list__item" v-for="road in roads" :key="road.id">
                            <button class="road-list-button" v-on:click="roadContent = road; buttonFocus($event); runAnimationOnClick()" v-bind:class="{ 'road-list-button--target' : road.id == 1}">
                                <h3 class="road-list-title">{{road.title}}</h3>
                                <p class="road-list-description"> {{road.subtitle}}</p>
                            </button>
                        </li>
                    </ul>
                    <div class="road-slider">
                        <div class="road-view">
                            <div class="road-view-box card-animate" >
                                <div class="road-view-box__header">
                                    <h4 class="road-view-box-title road-view-box-title--main">
                                        {{roadContent.title}}
                                    </h4>
                                </div>
                                <div class="road-view-box__tile road-view-box__tile--main">
                                    <ul class="road-view-content-list">
                                        <li class="road-view-content-list__item">
                                            <p>Czas spływu: <span>{{roadContent.road_time}}h</span></p>
                                        </li>
                                        <li class="road-view-content-list__item">
                                            <p>Długość odcinka: <span>{{roadContent.road_length}}km</span></p>
                                        </li>
                                        <li class="road-view-content-list__item">
                                            <p>Poziom trudności: <span>{{roadContent.road_level}}</span></p>
                                        </li>
                                        <li class="road-view-content-list__item">
                                            <p>Przeszkody: <span>{{roadContent.road_barriers}}</span></p>
                                        </li>
                                        <li class="road-view-content-list__item">
                                            <p>Przesiadki: <span>{{roadContent.road_transfers}}</span></p>
                                        </li>
                                    </ul>
                                    <div class="road-view-content__image">
                                        <img :src="linkPrefix + roadContent.road_map.formats.thumbnail.url" alt="">
                                    </div>
                                </div>
                            </div>
                            <div class="road-view-box card-animate" v-for="img in roadContent.roads_content" :key="img.title">
                                <div class="road-view-box__header">
                                    <h4 class="road-view-box-title">
                                        {{img.title}}
                                    </h4>
                                </div>
                                <div class="road-view-box__tile">
                                    <picture> 
                                        <img :src="linkPrefix + img.image.formats.small.url" alt="">
                                    </picture>
                                </div>
                            </div>
                        </div>
                    </div>
                    
            </div>
            <div class="road-footer">
                <nuxt-link :to="`road/${roadContent.title}-${roadContent.id}`" class="road-footer__link" >Zobacz opis trasy</nuxt-link>
            </div>
      </div>
  </section>
</template>

<script>
import roadsQuery from "~/apollo/queries/home/road"
export default {
    data(){
        return{
            roads:'',
            roadContent:'',
            linkPrefix: 'http://192.168.1.50:1337'
        }
    },
    apollo:{
        roads:{
            prefetch: true,
            query: roadsQuery
        },
    },
    methods: {
        runAnimation(){
            let roadContainer = document.querySelector('#road')
            let lastKnownScrollPosition = 0;
            console.log(roadContainer.offsetTop);
            function scrollAnimation(){
                    lastKnownScrollPosition = window.scrollY
                if((lastKnownScrollPosition + window.innerHeight) >= (roadContainer.offsetTop + 300)){
                    for(let card of roadContainer.querySelectorAll('.road-view-box')){
                        card.classList.add('card-animate')
                    }
                    document.removeEventListener('scroll', scrollAnimation);
                    console.log('asdasd');
                }
            }
            document.addEventListener('scroll',scrollAnimation)
        },
        runAnimationOnClick(){
            for(let card of document.querySelectorAll('.road-view-box')){
                card.classList.remove('card-animate')
                setTimeout(function(){
                    card.classList.add('card-animate')
                },50)
            }  
        },
        buttonFocus(el){
            let buttons = document.querySelectorAll('.road-list-button')
            for(let button of buttons){
                button.classList.remove('road-list-button--target')
            }
            el.target.parentElement.classList.add('road-list-button--target')

            if(el.target.localName == 'button'){
            el.target.classList.add('road-list-button--target')  } 
            else{
            el.target.parentElement.classList.add('road-list-button--target')}
        }
    },
    watch:{
        roads(value){
            this.roadContent = value[0]
            }
    },
    mounted() {
        if(this.roadContent !== ''){
            this.runAnimation()
        }
    },
            
    
}
</script>

<style scoped>
.container{
    position: relative;
    width: 100%;
    min-height: 100vh;
    background-size: cover;
    background-repeat: no-repeat;
    color:#FFF;
    z-index: 0;
}
@-moz-document url-prefix() {
    .container--road::before{
        content:'';
        position: absolute;
        top:0;
        left:0;
        width: 100%;
        height: 100%;
        z-index: -1;
        background-color: rgba(0, 0, 0, 0.644);
    }
}

.road-layout{
    position: relative;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    min-height: 100vh;
    margin:0 auto;
    padding: 5rem 0;
    z-index: 1;
    backdrop-filter: blur(10px);
}
.road-header{
    width: calc(100% - 10rem);
    max-width: 1300px;
    margin:0 auto;
}
.title{
    font-size: 2.5rem;
    font-weight: bold;
    text-transform: uppercase;
}
.road-container{
    display: flex;
    align-items: center;
    margin: 3rem 0;
}
.road-list{
    height: auto;
    width: 100%;
    max-width: 380px;
    margin-left: 12rem;
    padding: 2rem 0;
    padding-left: 3rem;
    border-left: 1px solid rgba(255,255,255,0.4);
}
.road-list__item{
    margin: 2rem 0;
}
.road-list-title{
    font-size: 1.5em;
}
.road-list-description{
    font-size: 0.8em;
}
.road-list-button{
    display: flex;
    flex-direction: column;
}
.road-list-button:focus{
    outline: none;
}
.road-list-button--target{
    font-size: 1.1rem;
    font-weight: bold;
}
.road-slider{
    position: relative;
    display: flex;
    width: 100%;
    overflow-x: auto;
    overflow-y:hidden;
    padding-bottom: 1rem;
    scrollbar-width: thin;
    scrollbar-color: #2B6651 rgb(192, 192, 192);
}
.road-slider::-webkit-scrollbar {
    height: 12px;
}

.road-slider::-webkit-scrollbar-track {
  background: rgb(192, 192, 192);
  border-radius: 20px;
}

.road-slider::-webkit-scrollbar-thumb {
  background-color: #2B6651;
  border-radius: 20px;
}
.road-view{
    position: relative;
    display: flex;
    transform-style: preserve-3d;
    
}
.road-view-box{
    display: flex;
    flex-direction: column;
    width: 100%;
    max-width: 300px;
    margin-right: 2rem;
    transform: rotateY(-180deg);
    backface-visibility: hidden;
}
.card-animate{
    animation: flipCard 1s ease forwards;
}
@keyframes flipCard {
    0%{
    transform: rotateY(-180deg);

    }
    100%{
    transform: rotateY(0);

    }
}
.road-view-box__header{
    height: 50px;

}
.road-view-box-title{
    font-weight: bold;
    text-transform: uppercase;
}
.road-view-box-title--main{
    font-size: 1.3rem;
}
.road-view-box__tile{
    width: 100%;
    min-width: 300px;
    height: 360px;
    background-color:#FFF;
    border-radius: 10px;
}

.road-view-box__tile--main{
    display: flex;
    align-items: center;
    flex-direction: column;
    padding: 2rem;
    background-color: #2B6651;
}
.road-view-content-list{
    width: 100%;
}
.road-view-content-list__item{
    margin-bottom: 0.8rem;
    font-size: 1rem;
}
.road-view-content-list__item span{
    font-weight: 200;
}
.road-view-content__image{
    position: relative;
    width: 130px;
    height: 130px;
}
.road-view-box__tile img, .road-view-content__image img{
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 10px;
}
.road-footer{
    display: flex;
    justify-content: center;
    width: 100%;
}
.road-footer__link{
    padding: 1rem 3rem;
    border:1px solid #FFF;
    border-radius: 10px;
    text-transform: uppercase;
}
@media screen and (max-width:1000px) {
    .container{
        height: auto;
    }
    .road-container{
        flex-direction: column;
    }
    .road-header{
        text-align: center;
    }
    .road-list{
        display: flex;
        justify-content: space-evenly;
        padding: 2rem 0;
        margin: 0;
        max-width: 100%;
        border-left: 0;
    }
    .road-view{
        padding-left: 5rem;
    }
    .road-footer{
        margin-top: 4rem;
    }
}
@media screen and (max-width: 500px) {
    .road-header{
        width: 100%;
        padding: 0 1rem;
    }
    .title{
        font-size: 2rem;
    }
    .road-view{
        padding-left: 1rem;
    }
}
</style>