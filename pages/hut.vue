<template>
   <div class="container" v-if="hutPage !== ''">
       <header class="hut-container hut-container--header" >
            <div class="header-column-text">
                <div class="header-content-container">
                        <h2 class="hut-header-title">{{hutPage.headerTitle}}</h2>
                        <p class="hut-header-lead">
                            {{hutPage.subtitleHeader}}
                        </p>
                        <a href="tel:696599556" class="hut-header-button">Zadzwoń</a>
                </div>
            </div>
            <div class="hut-header__column-image">
                <picture> 
                    <source :srcset="linkPrefix + hutPage.headerImage.formats.large.url" media="(min-width: 1000px)">
                    <img class="header-image" :src="linkPrefix + hutPage.headerImage.formats.medium.url" :alt="hutPage.headerImage.alternativeText">
                </picture>
            </div>
        </header>
        aaasa
   </div>
</template>

<script>
import hutQuery from '~/apollo/queries/page/hut'
export default {
    name:'hut',
    data(){
        return{
            hutPage:'',
            linkPrefix: 'http://192.168.1.50:1337',
        }
    },
    apollo:{
        hutPage:{
            prefetch: true,
            query: hutQuery
        },
    },
  
}
</script>

<style scoped>
.container{
        overflow-x: hidden;
}
    .hut-container{
        position: relative;
        display: flex;
        align-items: stretch;
        justify-content: stretch;
        width: 100%;
        padding: 7rem;
    }
    .hut-container--column{
        position: relative;
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(500px,1fr));
        grid-gap: 4rem;
        justify-items: center;
        width: 100%;
        height: auto;
        max-width: calc(1300px + 4rem);
        padding: 7rem 2rem;
        margin: 0 auto;
    }
    .hut-container--blue{
        height: auto;
        padding: 8rem;
        color:#FFF;
        background-color: #005492;
        z-index: 4
    }
    @media screen and (max-width:950px) {
        .hut-container{
            padding: 7rem 2rem;
        }
    }
    .hut-container--header{
        padding: 0;
        height: 100vh;
    }
    .hut-container--gray{
        margin-bottom: 0;
        padding-bottom: 8rem;
        background-color: #F4F4F4;
    }
    @media screen and (max-width:750px) {
        .hut-header-title{
            font-size: 1.5rem;
        }
        .hut-container--column{
            display: flex;
            flex-direction: column;
        }
    }
    @media screen and (max-width:1150px) {
        .hut-container--left{
            display: flex;
            align-items: center;
            flex-direction: column-reverse;
        }
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
    .hut-header-title{
        font-size: 2.5rem;
        font-weight: bold;
        line-height: 100%;
        margin-bottom: 0.5rem;
        text-transform: uppercase;
    }
    .hut-header-subtitle{
        font-size: 1.5rem;
        margin-bottom: 1rem;
    }
    
    @media screen and (max-width:750px) {
        .header-column-text{
            display: flex;
            flex-direction: column;
            justify-content: center;
            align-items: center;
            padding: 0 2rem;
            width: calc(100% - 2rem);
        }
        .hut-header-title{
            font-size: 2rem;
        }
    }
    .hut-header-lead{
        line-height: 150%;
        margin-bottom: 4rem;
        text-transform: uppercase;
    }
    .hut-header-button{
        padding: 0.5rem 2rem;
        border:1px solid #000;
        border-radius: 2rem;
    }
    .hut-header__column-image{
        position: absolute;
        height: 100vh;
        width: 50%;
        right:0;
        transition: 1s ease all;
    }
    .header-image{
        position: relative;
        height: 100%;
        width: 100%;
        object-fit: cover;
    }
    
    @media screen and (max-width:1000px) {
        .hut-header__column-image{
            width: 100%;
        }
        .hut-header__column-image::after{
            content: '';
            position: absolute;
            top:0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.356);
        }
        .hut-content-column--text-left,
        .hut-content-column--text-right
        {
            padding: 1rem;
        }
        .header-content-container{
            color:#FFF;
        }
        .hut-header-button{
            border-color: #FFF;
        }
    }
    .content-column{
        max-width: 650px;
        position: relative;
        margin:2rem 0;
        z-index: 1;
    }
    .content-column--left.content-column--image::before{
        content: '';
        position: absolute;
        left: -50%;
        top:-10%;
        width: 100%;
        height: 120%;
        background-color: #F8F8F8;
        z-index: -1;
        border-radius: 15px;
    }
    .content-column--right.content-column--image::before{
        content: '';
        position: absolute;
        left: 50%;
        top:-10%;
        width: 100%;
        height: 120%;
        background-color: #F8F8F8;
        z-index: -1;
        border-radius: 15px;
    }
    @media screen and (max-width:520px) {
        .content-column--right.content-column--image::before,
        .content-column--left.content-column--image::before{
            display: none;
        }
    }
    .content-column--image img{
        width: 100%;
        height: 100%;
        border-radius: 15px;
    }
    .content-column__title{
        margin-bottom: 1.5rem;
        font-size: 1.5rem;
        font-weight: bold;
        text-transform: uppercase;
    }
    .hut-layout{
        display: flex;
        flex-direction: column;
        width: 100%;
        max-width: 1300px;
        height: 100%;
        margin:0 auto;
        z-index: 1;
    }
    .hut-layout--column{
        flex-wrap: wrap;
    }
    .hut-layout-header{
        width: 100%;
        margin-bottom: 5rem;
    }
    .hut-layout-header__title{
        font-size: 2.5rem;
        font-weight: bold;
        text-transform: uppercase;
    }
    .hut-layout-header__subtitle{
        margin-top: 0.5rem;
        font-size: 1.2rem;
        text-transform: uppercase;
    }
    
    @media screen and (max-width:950px) {
       .hut-layout-header__title,
       .hut-layout-header__subtitle{
           text-align: center;
        }
        .hut-layout-header__title{
            font-size: 1.5rem;
           }
    }
    .hut-layout-content{
        display: flex;
        flex-wrap: wrap;
        justify-content: space-evenly;
    }
    .hut-layout-content--blue::before{
        content: "";
        position: absolute;
        bottom: 10%;
        left: 5%;
        width: 80%;
        height: 50%;
        z-index: -1;
        background-color: #005B9D;
        border-radius: 15px;
    }
    .hut-layout-content--gallery{
        flex-direction: column;
    }
    .hut-layout-content--price-section{
        width: 100%;
        height: auto;
        display: flex;
        flex-direction: row;
    }
    .hut-card{
        display: flex;
        flex-direction: column;
        align-items: center;
        width: 270px;
        height: 160px;
        padding: 1rem;
        margin: 2rem 1rem;
        background-color: #FFF;
        border-radius: 10px;
        color:#000;
        text-align: center;
    }
    .hut-card__img{
        width: 40px;
        height: 40px;
    }
    .hut-card__title{
        margin: 0.3rem;
        box-sizing: border-box;
        font-size: 0.9rem;
        font-weight: bold;
        text-transform: uppercase;
    }
    .hut-card__text{
        margin: 0;
        font-size: 0.9rem;
    }
    /* Furnishings section*/
    .furnishings-box{
        display: flex;
        flex-direction: column;
        width: 100%;
        min-width: 320px;
        max-width: 50%;
        margin-bottom: 2rem;
    }
    .furnishings-box-header{
        display: flex;
        width: 100%;
        margin-bottom: 1.5rem;
    }
    .furnishings-box-header__title{
        position: relative;
        padding: 0.5rem 2.5rem;
        font-size: 1rem;
        background-color: #FFF;
        color: #000;
        font-weight: bold;
        text-transform: uppercase;
        border-radius: 40px;
    }
    .furnishings-box-list{
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(300px,1fr));
        grid-row-gap: 0.3rem;
        padding: 0 0.5rem;
    }
    .furnishings-box-list__item{
        font-size: 0.9rem;
    }
    .furnishings-box-list__item::before{
        content: '';
        display: inline-block;
        height: 0.5rem;
        width: 0.5rem;
        background-image: url('../assets/check.svg');
        background-size: 100%;
        background-position: center;
        background-repeat: no-repeat;

    }
    /* Price section */
    .price-card{
        position: relative;
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: stretch;
        width: 100%;
        max-width: 380px;
        padding: 2rem;
        margin: 1rem 0;
        background-color: #FFF;
        border-radius: 10px;
        box-shadow: 0px 4px 10px 2px rgba(193, 193, 193, 0.25);
    }
    .price-card-header{
        margin-bottom: 2rem;
        text-align: center;
    }
    .price-card-header__title{
        font-size: 1.3rem;
        font-weight: bold;
    }
    .price-card-variants{
        display: flex;
        width: 100%;
        font-size: 0.8rem;
    }
    .price-card-variants__content{
        margin-bottom: 1.5rem;
    }
    .price-card-variants__content p{
        margin: 0.3rem 0;
    }
    .price-card-variants__img-box{
        display: flex;
        justify-content: center;
        align-items: center;
        width: 60px;
        height: 60px;
        margin-right: 1.5rem;
        border:1px solid #005492;
        border-radius: 100px;
    }
    .card-variants-img{
        width: 35px;
        height: 35px;
    }
    .card-variants-title{
        font-size: 1rem;
        font-weight: bold;
    }
    .price{
        color:#005492;
        font-size: 1.2rem;
        font-weight: bold;
    }
    .price--old{
        color:#ACACAC;
        text-decoration-line: line-through;
    }
    .price--promotion{
        color: #EB4132;
    }
    .price-button{
        padding: 0.5rem 0;
        font-weight: bold;
        font-size: 0.9rem;
        text-align: center;
        color:#005492;
        border:1px solid #005492;
    }
    /* Additional */
    .additional-information{
        margin-top: 5rem;
        padding: 2rem;
        background-color: #FFF;
        border-radius: 10px;
        box-shadow: 0px 4px 10px 2px rgba(193, 193, 193, 0.25);
    }
    .additional-information__title{
        margin-bottom: 1rem;
        font-size: 1.2rem;
        font-weight: bold;
    }
    /* Gallery */
    .gallery-header{
        display: flex;
        margin-bottom: 3rem;
    }
    .gallery-thumbnails-card{
        width:100%;
        max-width: 180px;
        height: 130px;
        margin: 0 1.5rem;
    }
    .gallery-thumbnails-card--active{
        font-weight: bold;
    }
    .gallery-thumbnails-card__img{
        width: 100%;
        height: 100px;
        border-radius: 10px;
    }
    .gallery-thumbnails-card__title{
        margin-top: 0.5rem;
        text-align: center;
    }
    .gallery-content{
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(440px,1fr));
        grid-gap: 1rem;
    }
    .gallery-content__column--big{
        display: flex;
        flex-direction: column;
        justify-content: space-between;

    }
    .gallery-content__column--tile{
        display: grid;
        grid-template-columns: repeat(auto-fit, minmax(210px,1fr));
        grid-gap: 1rem;
    }
    
    .gallery-image{
        width: 100%;
        height: 100%;
        max-height: 220px;
        border-radius: 10px;
    }
    .gallery-image--big{
        height: 360px;
        max-height: 360px;
    }
    .gallery-subtitle{
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100%;
        min-height: 80px;
        height: 100%;
        font-size: 1.1rem;
        font-weight: bold;

    }
    @media screen and (max-width:1136px) {
        .hut-layout-header{
            margin-bottom: 1.5rem;
        }
        .gallery-header{
            margin-bottom: 1rem;
        }
        .gallery-thumbnails-card{
            max-width: 70px;
            height: 100px;
            margin: 0.5rem;

        }
        .gallery-thumbnails-card__img{
            object-fit: cover;
            height: 70px;
            border-radius: 100%;
        }
        .gallery-thumbnails-card__title{
            font-size: 0.8rem;
        }
        .gallery-image--big{
            height: 440px;
            max-height:440px;
        }
        .gallery-content{
            display: flex;
            align-items: stretch;
            flex-direction: column;
            padding: 0 1rem;
        }
        .gallery-content__column--big{
            flex-direction: column-reverse;
        }
    }
    @media screen and (max-width: 770px) {
        .gallery-content__column--big{
            margin-bottom: 1rem;
        }
        .gallery-image--big{
            height: auto;
            max-height:320px;
        }
    }
</style>