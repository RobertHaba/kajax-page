<script>
export default {
    methods: {
        addAnimation(animation){
                if((animation.scrollPosition + window.innerHeight) >= (animation.element.offsetTop + animation.addSpaceFromTop)){
                    animation.elementToAnimate.classList.remove(animation.classNameOld)
                    animation.elementToAnimate.classList.add(animation.classNameNew)
                }
                else{
                    animation.elementToAnimate.classList.add(animation.classNameOld)
                    animation.elementToAnimate.classList.remove(animation.classNameNew)
                }
        },
        addAnimationToMoreItems(animation){
            console.log(animation);
                if((animation.scrollPosition + window.innerHeight) >= (animation.element.offsetTop + animation.addSpaceFromTop)){
                    animation.elementsToAnimate.forEach(element => {
                        element.classList.remove(animation.classNameOld)
                        element.classList.add(animation.classNameNew)
                    });
                }
                else{
                    animation.elementsToAnimate.forEach(element => {
                        element.classList.add(animation.classNameOld)
                        element.classList.remove(animation.classNameNew)
                    });
                }
        }
    },
}
</script>