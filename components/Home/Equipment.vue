<template>
  <section class="container" id="wypozyczalnia" data-animation-id="equipment" v-if="accessories !== ''">
        <div class="equipment-layout">
            <div class="equipment-header">
                <h2 class="title">Poznaj nasz sprzęt</h2>
            </div>
            <div class="equipment-container">
                <div class="image-view-container" data-animation-id="equipment-main-image" v-if="mainAccesories !== ''">
                    <div class="main-image-box">
                        <picture>
                            <img class="main-image" :src="linkPrefix + mainAccesories.image.formats.small.url" alt="" width="320px" height="320px">
                        </picture>
                    </div>
                </div>
                <div class="equipment-specs-container" data-animation-id="equipment-specs" data-equipment-content="main">
                    <h3 class="equipment-specs-header">
                        {{mainAccesories.title}}
                    </h3>
                    <p class="equipment-specs-content">
                        {{mainAccesories.description}}    
                    </p>
                    <ul class="equipment-specs-list">
                        <li class="equipment-specs-list-item">
                            <p class="equipment-specs-list-item__text">Pojemność: {{mainAccesories.capacity}} os</p>
                        </li>
                        <li class="equipment-specs-list-item">
                            <p class="equipment-specs-list-item__text">Wyposażenie: {{mainAccesories.equipment}}</p>
                        </li>
                    </ul>

                </div>
                <div class="preview-all-container" data-animation-id="equipment-preview">
                    <h3 class="preview-all-header">
                        Zobacz pozostały sprzęt
                    </h3>
                    <div class="preview-all-box">
                        <div class="preview-all-subbox">
                            <div class="peview-item" v-for="equipment in accessories" :key="equipment.id" v-on:click="mainAccesories = equipment, selected = equipment.id" :class="{'preview-item--selected':selected==equipment.id}" >
                                <div class="preview-item-image-box">
                                    <img :src="linkPrefix + equipment.image.formats.thumbnail.url" alt="" width="100px" height="70px">
                                </div>
                                <div class="preview-item-content">
                                    <h4 class="preview-item-content-header">{{equipment.title}}</h4>
                                    <p class="preview-item-content-text">Pojemność: {{equipment.capacity}} os.</p>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
  </section>
</template>

<script>
import equimpentQuery from '~/apollo/queries/home/equipment'
export default {
    data(){
        return{
            accessories: '',
            mainAccesories:'',
            linkPrefix: 'http://192.168.1.50:1337',
            selected:''
            
        }
    },
    apollo:{
        accessories:{
            prefetch:true,
            query: equimpentQuery
        }
    },
    methods: {
        changeContent(){

        },
        buttonFocus(el){
            if(el.target.localName == 'img'){
                console.log(el.target.parentElement);
            el.target.parentElement.classList.add('road-list-button--target')
            }
            else{
                el.target.parentElement.parentElement.querySelector('.preview-item-image-box').classList.add('road-list-button--target')
            } 
        }
    },
    watch:{
        accessories(value){this.mainAccesories = value[0]},
        selected(){
            let contentBox = document.querySelector('[data-equipment-content="main"]')
            contentBox.classList.remove('animation--fadeInUp')
            contentBox.offsetWidth;
            contentBox.classList.add('animation--fadeInUp')
        }
    }
}
</script>

<style scoped>
.container{
  position: relative;
  z-index: 0;
  min-height: 600px;
  background-color: #005492;
  padding: 7rem 5rem;
  color:#FFF;
  overflow: hidden;
}
.equipment-layout{
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    height: 100%;
    margin:0 auto;
}
.equipment-header{
    width: 100%;
    max-width: 1300px;
    margin:0 auto;
    margin-bottom: 5rem;
}
.title{
    font-size: 2.5rem;
    font-weight: bold;
    text-transform: uppercase;
}
.equipment-container{
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    width: 100%;
    max-width: 1300px;
    margin:0 auto;
}
.image-view-container{
    display: flex;
    justify-content: center;
    align-items: center;
    position: relative;
    height: 100%;
    max-height: 400px;
    width: 100%;
    max-width: 400px;
}
.main-image-box{
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;
    height: 400px;
    width: 400px;
    border-radius: 100%;
    background-color: #FFF;
}
.main-image-box::before{
    content: '';
    position: absolute;
    top:-20px;
    left: -20px;
    width: 420px;
    height: 420px;
    border-radius: 100%;
    background-color: #4581B8;
    z-index: -1;
}
.main-image{
    position: relative;
    width: 100%;
    max-width: 320px;
    height: auto;
    z-index: 2;
}
.equipment-specs-container{
    width:100%;
    max-width: 360px;
    padding: 0 1rem;
}
.equipment-specs-header,
.preview-all-header{
    margin-bottom: 1.5rem;
    font-size: 1.3rem;
    text-transform: uppercase;
    font-weight: bold;

}
.equipment-specs-content{
    width: 100%;
    color: #9AC4DC;
    font-size: 0.9rem;

}
.equipment-specs-list{
    position: relative;
    padding: 1rem;
    padding-left: 10px;
    font-size: 0.9rem;
    color: #9AC4DC;
}
.equipment-specs-list-item{
    position: relative;
    margin-bottom: 1rem;
}
.equipment-specs-list-item::before{
    position: absolute;
    content: '';
    left: -10px;
    top: 50%;
    transform: translateY(-50%);
    padding: 10px;
    border-radius: 100%;
    background-color: #4580b89f;
    z-index: -1;

}
.preview-all-container{
    width:100%;
    max-width: 340px;
}
.preview-all-box{
    position: relative;
    width: 100%;
    height: 300px;
    overflow-y: scroll;
    overflow-x: hidden;
}
.preview-all-subbox{
    display: flex;
    flex-direction: column;
    height: auto;
}
.peview-item{
    display: flex;
    width: 100%;
    height: 90px;
    margin-bottom: 1rem;
    padding-right: 1rem;
    cursor:pointer;
}
.peview-item:hover .preview-item-image-box,
.preview-item--selected .preview-item-image-box{
    transform: scale(0.8);
}
.preview-item-image-box{
    position: relative;
    display: flex;
    align-items: center;
    justify-content: center;
    width: 120px;
    height: 80px;
    background-color: #FFF;
    border-radius: 10px;
    transition: 0.8s;
}
.preview-item-image-box img{
    position: relative;
    width: 100%;
    max-width: 100px;
    height: auto;
}
.preview-item-content{
    font-size: 0.9rem;
    margin-left: 1rem;
}
.preview-item-content-header{
    font-weight: bold;
}
.preview-item-content-text{
    color: #9AC4DC;
}
@media screen and (max-width:1270px) {
    .title{
        text-align: center;
    }
    .equipment-container{
        justify-content: space-evenly;
    }
    .equipment-specs-container{
        display: flex;
        flex-direction: column;
        justify-content: center;
    }
    .preview-all-header{
        margin-top: 3rem;
    }
    
}

@media screen and (max-width:860px) {
    .container{
        padding: 5rem 1rem;
    }
    .equipment-specs-container{
        margin-top: 3rem;
    }
    .image-view-container{
        max-width: 420px;
    }
    .main-image-box{
        height: 320px;
        width: 320px;
    }
    .main-image-box::before{
        width: 340px;
        height: 340px;
    }
    .main-image{
        width: 280px;
        max-height: 280px;
    }
}
</style>