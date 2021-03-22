<template>
   <div class="container" v-if="roads !== ''">
       <header class="road-header" >
            <div class="header-column-text">
                <div class="header-content-container">
                        <h2 class="road-header-title">Spływy kajakowe - rzeka {{roads[this.roadsID].title}}</h2>
                        <h3 class="road-header-subtitle">Trasa - {{roads[this.roadsID].subtitle}}</h3>
                        <p class="road-header-lead">
                            {{roads[this.roadsID].description_site}}
                        </p>
                        <a href="tel:696599556" class="road-header-button">Zadzwoń</a>
                </div>
            </div>
            <div class="road-header__column-image">
                    <img class="header-image" :src="linkPrefix + roads[this.roadsID].roads_content[0].image.formats.large.url" alt="">
            </div>
        </header>
        <section class="road-container" data-animation-id="road-content-1">
            <header class="road-content-column road-content-column--text-left" data-animation-id="road-text-1">
                <h2 class="road-content-title">{{roads[this.roadsID].road_content_site[0].title}}</h2>
                <div class="road-content-text" v-html="$md.render(roads[this.roadsID].road_content_site[0].content)">
                </div>
            </header>
            <div class="road-content-column road-content-column--card road-content-column--green" data-animation-id="road-box-1">
               <div class="road-content-card road-content-card--center road-content-card--green">
                   <img :src="linkPrefix + roads[this.roadsID].road_map.url" alt="">
               </div>
               <div class="road-content-card">
                   <h3 class="road-content-card-title">{{roads[this.roadsID].road_price[0].title}}</h3>
                   <ul class="road-content-card-list">
                       <li class="road-content-card-list__item">
                           <p class="card-list-item-text">Poniedziałek-piątek: <span class="card-list-item-content">{{roads[this.roadsID].road_price[0].normal_days}}zł/os</span></p>
                       </li>
                       <li class="road-content-card-list__item">
                           <p class="card-list-item-text">Weekend: <span class="card-list-item-content">{{roads[this.roadsID].road_price[0].weekend_days}}zł/os</span></p>
                       </li>
                   </ul>
               </div>
               <div class="road-content-card">
                    <h2 class="road-content-card-title">Informację szczegółowe</h2>
                   <ul class="road-content-card-list">
                       <li class="road-content-card-list__item">
                           <p class="card-list-item-text">Czas spływu: <span class="card-list-item-content">{{roads[this.roadsID].road_time}}h</span></p>
                       </li>
                       <li class="road-content-card-list__item">
                           <p class="card-list-item-text">Długość odcinka: <span class="card-list-item-content">{{roads[this.roadsID].road_length}}km</span></p>
                       </li>
                       <li class="road-content-card-list__item">
                           <p class="card-list-item-text">Poziom trudności: <span class="card-list-item-content">{{roads[this.roadsID].road_level}}</span></p>
                       </li>
                       <li class="road-content-card-list__item">
                           <p class="card-list-item-text">Przeszkody: <span class="card-list-item-content">{{roads[this.roadsID].road_barriers}}</span></p>
                       </li>
                       <li class="road-content-card-list__item">
                           <p class="card-list-item-text">Przesiadki: <span class="card-list-item-content">{{roads[this.roadsID].road_transfers}}</span></p>
                       </li>
                   </ul>
               </div>
               <div class="road-content-card road-content-card--green">
                   <h3 class="road-content-card-title">{{roads[this.roadsID].road_price[1].title}}</h3>
                   <ul class="road-content-card-list">
                       <li class="road-content-card-list__item">
                           <p class="card-list-item-text">Poniedziałek-piątek: <span class="card-list-item-content">{{roads[this.roadsID].road_price[1].normal_days}}zł/os</span></p>
                       </li>
                       <li class="road-content-card-list__item">
                           <p class="card-list-item-text">Weekend: <span class="card-list-item-content">{{roads[this.roadsID].road_price[1].weekend_days}}zł/os</span></p>
                       </li>
                   </ul>
               </div>
            </div>
        </section>
        <section class="road-container" data-animation-id="road-content-2">
            <div class="road-content-column" data-animation-id="road-box-2">
               <div class="road-content-main-view">
                   <picture>
                                <source media="(min-width: 1300px)" :srcset="linkPrefix + roads[this.roadsID].roads_content[activeGalleryImageId].image.formats.small.url">
                                <source media="(min-width: 850px)" :srcset="linkPrefix + roads[this.roadsID].roads_content[activeGalleryImageId].image.formats.medium.url">
                                <source media="(min-width: 650px)" :srcset="linkPrefix + roads[this.roadsID].roads_content[activeGalleryImageId].image.formats.small.url">
                                <img class="gallery-image" :src="linkPrefix + roads[this.roadsID].roads_content[activeGalleryImageId].image.formats.medium.url" :alt="roads[this.roadsID].roads_content[activeGalleryImageId].image.alternativeText">
                    </picture>
               </div>
               <div class="road-carousel">
                   <div class="road-content-carousel">
                        <div class="road-content-carousel-box" v-for="(contentImage, index) in roads[this.roadsID].roads_content" :key="contentImage.id" @click="activeGalleryImageId = index">
                                <img class="gallery-image" :src="linkPrefix + contentImage.image.formats.thumbnail.url" :alt="contentImage.image.alternativeText">
                            
                        </div>
                    </div>
               </div>
            </div>
            <div class="road-content-column road-content-column--text-right" data-animation-id="road-text-2">
                <h2 class="road-content-title">Dodatkowe informacje odnośnie spływów</h2>
                <p class="road-content-text">Rzeka Zbrzyca znajduje się na terenie Zaborskiego Parku Krajobrazowego. Zbrzyca ma wiele szlaków kajakowych ale najbardziej malowniczym i najczęściej odwiedzanym przez naszych klientów jest odcinek Leśno-Swornegacie. Jest on dobrze oznakowany dlatego też przepłynięcie tej trasy nie powinno stwarzać żadnych problemów.
                </p>
                <p class="road-content-text">Rzeka Zbrzyca znajduje się na terenie Zaborskiego Parku Krajobrazowego. Zbrzyca ma wiele szlaków kajakowych ale najbardziej malowniczym i najczęściej odwiedzanym przez naszych klientów jest odcinek Leśno-Swornegacie. Jest on dobrze oznakowany dlatego też przepłynięcie tej trasy nie powinno stwarzać żadnych problemów.
                </p>
                <p class="road-content-text">Rzeka Zbrzyca znajduje się na terenie Zaborskiego Parku Krajobrazowego. Zbrzyca ma wiele szlaków kajakowych ale najbardziej malowniczym i najczęściej odwiedzanym przez naszych klientów jest odcinek Leśno-Swornegacie. Jest on dobrze oznakowany dlatego też przepłynięcie tej trasy nie powinno stwarzać żadnych problemów.
                </p>
                <p class="road-content-text">Rzeka Zbrzyca znajduje się na terenie Zaborskiego Parku Krajobrazowego. Zbrzyca ma wiele szlaków kajakowych ale najbardziej malowniczym i najczęściej odwiedzanym przez naszych klientów jest odcinek Leśno-Swornegacie. Jest on dobrze oznakowany dlatego też przepłynięcie tej trasy nie powinno stwarzać żadnych problemów.
                </p>
            </div>
        </section>
        <Footer />
   </div>
</template>

<script>
import roadsQuery from "~/apollo/queries/road/road"
import Footer from '~/components/Home/Footer'
import Animation from "~/components/assets/Animation"
export default { 
    head() {
           return {
               title: `Spływy kajakowe rzeką ${this.roadsHead[this.roadsID].title.toLowerCase()}, trasa ${this.roadsHead[this.roadsID].subtitle.toLowerCase()}  | Kajax Lipusz`,
               meta: [
                {
                    hid: 'description',
                    name: 'description',
                    content: this.roadsHead[this.roadsID].description
                }
                ]
           }
        
    },
    components:{
        Footer
    },
    data(){
        return{
            roads:'',
            roadsHead:[
                    {
                        title:'wda',
                        subtitle:'lipusz-wdzydze',
                        description:''
                    }
                ],
            roadsID:'0',
            activeGalleryImageId:0,
            linkPrefix: 'http://192.168.1.50:1337'
        }
    },
    apollo:{
        roads:{
            prefetch: true,
            query: roadsQuery
        },
    },   
    watch:{
        roads(value){
            this.roadsHead = this.roads
            let roadNewId = this.$route.params.road.split('-')[1] -1
            this.roadsID = (this.roads.length - 1 >= roadNewId && roadNewId  >= 0)?  roadNewId  : 0
            },
        activeGalleryImageId(){
            let imageMainView = document.querySelector('.road-content-main-view')
            imageMainView.classList.remove('road-content-main-view--animation')
            imageMainView.offsetWidth
            imageMainView.classList.add('road-content-main-view--animation')
        }
    },
    methods: {
    runAnimation(){
            let roadContent = document.querySelector('[data-animation-id="road-content-1"]')
            let roadContent2 = document.querySelector('[data-animation-id="road-content-2"]')
            let lastKnownScrollPosition = 0;
            document.addEventListener('scroll',()=>{
                lastKnownScrollPosition = window.scrollY
             Animation.methods.addAnimation({
                       element: roadContent,
                       elementToAnimate: roadContent.querySelector('[data-animation-id="road-text-1"]'),
                       classNameNew:'animation--fadeInLeftToRight',
                       classNameOld:'animation--hidden',
                       addSpaceFromTop:100,
                       scrollPosition: lastKnownScrollPosition

                   }) 
            Animation.methods.addAnimation({
                       element: roadContent,
                       elementToAnimate: roadContent.querySelector('[data-animation-id="road-box-1"]'),
                       classNameNew:'animation--fadeInRightToLeft',
                       classNameOld:'animation--hidden',
                       addSpaceFromTop:100,
                       scrollPosition: lastKnownScrollPosition

                   })
            Animation.methods.addAnimation({
                       element: roadContent2,
                       elementToAnimate: roadContent2.querySelector('[data-animation-id="road-text-2"]'),
                       classNameNew:'animation--fadeInUp',
                       classNameOld:'animation--hidden',
                       addSpaceFromTop:100,
                       scrollPosition: lastKnownScrollPosition

                   })
            Animation.methods.addAnimation({
                       element: roadContent2,
                       elementToAnimate: roadContent2.querySelector('[data-animation-id="road-box-2"]'),
                       classNameNew:'animation--fadeInUp',
                       classNameOld:'animation--hidden',
                       addSpaceFromTop:100,
                       scrollPosition: lastKnownScrollPosition

                   })
            })
        }
  },
  mounted(){
      this.$nextTick(() => {
      this.$nuxt.$loading.start()
      setTimeout(() => {
          this.$nuxt.$loading.finish()
        if(this.roads !== ""){
            this.runAnimation()
        }
      }, 500)
    })
  },
    loading: true
    
}
</script>

<style scoped>
    .road-header, .road-container{
        position: relative;
        display: flex;
        align-items: stretch;
        justify-content: stretch;
        height: 100vh;
        width: 100%;
        margin-bottom: 7rem;
    }
    .road-container{
        overflow: hidden;

    }
    .header-column{
        width: 100%;
        max-width: 340px;
        height: 100%;
    }
    .header-column-text{
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
    .header-content-container{
        position: relative;
        max-width: 360px;
        color: #000;
        transition: 1s ease all;
    }
    .road-header-title{
        font-size: 2.5rem;
        font-weight: bold;
        line-height: 100%;
        margin-bottom: 0.5rem;
        text-transform: uppercase;
    }
    .road-header-subtitle{
        font-size: 1.5rem;
        margin-bottom: 1rem;
    }
    .road-header-lead{
        line-height: 150%;
        margin-bottom: 4rem;
        text-transform: uppercase;
    }
    .road-header-button{
        padding: 0.5rem 2rem;
        border:1px solid #000;
        border-radius: 2rem;
    }
    .road-header__column-image{
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
    .road-container{
        position: relative;
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(600px,1fr));
        width: 100%;
        height: auto;
        max-width: calc(1300px + 4rem);
        padding: 0 2rem;
        margin: 0 auto;
        margin-bottom: 7rem;
    }
    .road-content-column{
        width: 100%;
        height: 100%;
        margin: 2rem 0;
    }
    .road-content-column--text-left{
        padding-right: 10rem;
    }
    .road-content-column--text-right{
        padding-left: 10rem;

    }
    .road-content-title{
        margin-bottom: 1.5rem;
        font-size: 1.5rem;
        font-weight: bold;
        text-transform: uppercase;
    }
    .road-content-text{
        margin-bottom: 1rem;
        font-size: 0.9rem;
    }
    .road-content-column--card{
        display: grid;
        grid-template-rows: repeat(2,300px);
        grid-template-columns: repeat(auto-fit,minmax(280px,1fr));
        grid-gap: 2rem;
        width: 100%;
    }
    .road-content-card{
        padding: 2rem;
        background-color: #005492;
        border-radius: 10px;
        color:#FFF;
    }
    .road-content-card--green{
        background-color: #2B6651;
    }
    .road-content-card img{
        position: relative;
        width: 100%;
        height: 100%;
        object-fit: cover;
    }
    .road-content-card-title{
        margin-bottom: 1.5rem;
        font-weight: bold;
        text-transform: uppercase;
    }
    .road-content-card-list__item{
        margin-bottom: 0.5rem;
    }
    .card-list-item-text{
        font-size: 0.9rem;
    }
    .card-list-item-content{
        color:#9AC4DC;
    }
    .road-content-card--green .card-list-item-content{
        color:#FFF;
    }
    .road-content-main-view{
        width: 100%;
        height: 360px;
    }
    .road-content-main-view--animation{
        animation: 0.7s fadeIn 0s both cubic-bezier(.1,.01,.72,.99);
    }
    @keyframes fadeIn {
        from{
            opacity: 0.5;
            transform: scale(0.5);
        }
        to{
            opacity: 1;
            transform: scale(1);
        }
    }
    .road-content-main-view img{
        width: 100%;
        max-height: 360px;
        border-radius: 10px;
    }
    .road-carousel{
        position: relative;
        display: flex;
        width: 100%;
        height: calc(130px + 2rem);
        margin-top: 0.5rem;
        padding: 1rem;
        overflow-x: auto;
        scrollbar-width: thin;
        scrollbar-color: #005492 rgb(192, 192, 192);
    }
    .road-carousel::-webkit-scrollbar {
        height: 12px;
    }

    .road-carousel::-webkit-scrollbar-track {
    background: rgb(192, 192, 192);
    border-radius: 20px;
    }

    .road-carousel::-webkit-scrollbar-thumb {
    background-color: #005492;
    border-radius: 20px;
    }
    .road-content-carousel{
        position: relative;
        display: flex;
        height: 100%;
        margin:-2rem 0 0 -2rem;

    }
    .road-content-carousel-box{
        margin:2rem 0 0 2rem;
        width: 200px;
        height: 100%;
    }
    .gallery-image{
        width: 100%;
        height: 100%;
        object-fit: cover;
        border-radius: 10px;
    }
    @media screen and (max-width:1000px) {
        .road-header__column-image{
            width: 100%;
        }
        .road-header__column-image::after{
            content: '';
            position: absolute;
            top:0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.26);
        }
        .road-content-column--text-left,
        .road-content-column--text-right
        {
            padding: 1rem;
        }
        .header-content-container{
            color:#FFF;
        }
        .road-header-button{
            border-color: #FFF;
        }
    }
    @media screen and (max-width:750px) {
        .road-header-title{
            font-size: 2rem;
        }
        .road-container{
            display: flex;
            flex-direction: column;
        }
        .road-content-column--card{
            justify-content: center;
            grid-template-rows: repeat(4,250px);
            grid-template-columns: 320px;
        }
        .road-content-main-view{
            height: 250px;
        }
    }
    @media screen and (max-width:500px) {
        .header-column-text{
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 0 2rem;
            width: calc(100% - 2rem);
        }
    }
</style>