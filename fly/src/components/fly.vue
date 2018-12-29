<template>
    <div class="fly">
        <div class="diji" v-for="item in 10" :key>
            <img :class="'diji' + item" :style="{left:Math.random() * 96 + '%',bottom:djBottom + 'px'}" src="../assets/diji.png" alt="">
        </div>
        <!-- <div v-for="item in 6" :key>
            <img :class="'item' + item" :style="{bottom:zdBottom + 'px',left:zdLeft + item + '%'}" class="bullet" src="../assets/feiji.png" alt="">
        </div> -->
        <img class="bullet" :style="{bottom:zdBottom + 'px',left:zdLeft + '%'}" src="../assets/feiji.png" alt="">
        <img class="aircraft" ref="topInfo" :style="{bottom:numBottom + 'px',left:numLeft + '%'}"  src="../assets/fly.png" alt="" srcset="">
        <input type="text" autofocus @keydown="show($event)">
    </div>
</template>
<script>
export default {
    data(){
        return{
            numBottom:10,
            numLeft:50,
            zdBottom:100,
            zdLeft:50,
            djLeft:50,
            djBottom:900
        }
    },
    mounted(){
        setInterval(() => {
            this.zidan()            
        }, 30);
    },
    created(){
        this.djLeft = Math.random() * 100
    },
    methods:{
        
        show: function (ev) {
            if(ev.keyCode == 38 && this.numBottom < 500){
                this.numBottom += 10;
                console.log(this.numLeft)

                return this.numLeft;
            }
            if(ev.keyCode == 40 && this.numBottom > 0){
                this.numBottom -= 10;
                console.log(this.numLeft)

                return this.numLeft;

            }
            if(ev.keyCode == 37 && this.numLeft > 2){
                this.numLeft -= 3;
                console.log(this.numLeft)

                return this.numLeft;

            }
            if(ev.keyCode == 39 && this.numLeft < 96){
                this.numLeft += 3;
                console.log(this.numLeft)

                return this.numLeft;

            }
        },
        zidan(){
            if(this.zdBottom < 1000){
                this.zdBottom += 10
                this.zdLeft = this.numLeft 

            }else{
                this.zdBottom = 100
            }
        }
    }
}
</script>
<style scoped>
.fly{
    width: 100%;
}
.bullet{
    position: absolute;
    width: 36px;
    margin-left: -18px;

}
.item1{
    bottom: 100px
}
.aircraft{
    position: absolute;
    margin-left: -40px;
    width: 80px;
}
.diji>img{
    width: 50px;
    position: absolute;
}
</style>
