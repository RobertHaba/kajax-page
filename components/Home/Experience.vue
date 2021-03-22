<template>
  <section class="container" data-animation-id="experience">
        <div class="experience-layout">
            <div class="experience-header">
                <h2 class="title">Dlaczego warto spływać z nami?</h2>
                <a href="tel:+48696599556" class="button">Zadzwoń <span>999-999-999</span></a>
            </div>
            <div class="experience-carousel-container">
                <div class="experience-carousele-wrapper" data-animation-id="experience-wrapper">
                    <div class="experience-carousele-item" v-for="experience in experiences" :key="experience.title">
                        <div class="experience-carousele-icon">
                            <img :src='linkPrefix+experience.image.url' alt="">
                        </div>
                        <div class="experience-carousele-content">
                            <h3 class="experience-carousele-content-title">{{experience.title}}</h3>
                            <p class="experience-carousele-content-text">
                                {{experience.description}}
                            </p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
  </section>
</template>

<script>
import experienceQuery from '~/apollo/queries/home/experience'
export default {
    data(){
        return{
            experiences:[],
            linkPrefix: 'http://192.168.1.50:1337'
        }
    },
    apollo:{
        experiences:{
            prefetch:true,
            query:experienceQuery
        }
    }
}
</script>

<style scoped>
.container{
  position: relative;
  z-index: 0;
  min-height: 500px;
  background-color: #F5F5F5;
  padding: 7rem 5rem;
  color:#1E1E1E;
}
.experience-layout{
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    max-width: 1300px;
    height: 100%;
    margin:0 auto;
}
.experience-header{
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    align-items: center;
    width: 100%;
    max-width: 1300px;
    margin:0 auto;
    margin-bottom: 5rem;
}
.title{
    font-size: 1.5rem;
    font-weight: bold;
    text-transform: uppercase;
}
.button{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 190px;
    height: 50px;
    background: #005492;
    color:#FFF;
}
.button span{
    font-size: 0.7rem;
}

.experience-carousel-container{
    position: relative;
    display: flex;
    justify-content: space-between;
    width: 100%;
    max-width: 1300px;
    padding: 1rem 0;
    overflow-x: scroll;
    scrollbar-width: thin;
    scrollbar-color: #2B6651 rgb(192, 192, 192);
}
.experience-carousel-container::-webkit-scrollbar {
    height: 12px;
}

.experience-carousel-container::-webkit-scrollbar-track {
  background: rgb(192, 192, 192);
  border-radius: 20px;
}

.experience-carousel-container::-webkit-scrollbar-thumb {
  background-color: #005492;
  border-radius: 20px;
}
.experience-carousele-wrapper{
    display: flex;
}
.experience-carousele-item{
    position: relative;
    height: 180px;
    width: 340px;
    border: 2px solid #005492;
    margin-right: 3rem;
}
.experience-carousele-icon{
    position: absolute;
    display: flex;
    justify-content: center;
    align-items: center;
    content:'';
    left: 2rem;
    top:-25px;
    width: 50px;
    height: 50px;
    z-index: 1;
    background-color: #F5F5F5;
}
.experience-carousele-icon img{
    width: 25px;
    height: 25px;
}
.experience-carousele-content{
    padding: 30px;
}
.experience-carousele-content-title{
    margin-bottom: 1rem;
    font-weight: bold;
    font-size: 1.1rem;
}
.experience-carousele-content-text{
    font-size: 0.9rem;
}
    @media screen and (max-width:900px) {
    .button{
        margin-top: 1rem;
    }
    }
    @media screen and (max-width:500px) {
    .experience-header{
        justify-content: center;
    }
    .title{
        text-align: center;
    }
    .container{
        padding: 5rem 1rem;
    }
    }
</style>