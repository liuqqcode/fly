<template>
    <div class="fly" @keydown="show($event)">
        <div class="diji" v-for="item in dj" :key>
            <img :class="'diji' + item.left" :style="{left:item.left + '%',bottom:djBottom + 'px'}" src="../assets/diji.png" alt="">
        </div>
        <!-- <div v-for="item in 6" :key>
            <img :class="'item' + item" :style="{bottom:zdBottom + 'px',left:zdLeft + item + '%'}" class="bullet" src="../assets/feiji.png" alt="">
        </div> -->
        <img class="bullet" :style="{bottom:zdBottom + 'px',left:zdLeft + '%'}" src="../assets/feiji.png" alt="">
        <img class="aircraft" ref="topInfo" :style="{bottom:numBottom + 'px',left:numLeft + '%'}"  src="../assets/fly.png" alt="" srcset="">
        <input type="text" autofocus >
    </div>
</template>
<script>
export default { 
    data(){
        return{
            numBottom:10,   //我的飞机距离底边
            numLeft:50,     //我的飞机距离左边
            zdBottom:100,   //子弹底边
            zdLeft:50,      //子弹左边
            djBottom:900,   //敌机底边
            dj:[            //敌机数量 敌机距离左边
                {
                    left:Math.floor( Math.random() * 100)
                }
                // ,{
                //     left:Math.random() * 100
                // },{
                //     left:Math.random() * 100
                // },{
                //     left:Math.random() * 100
                // },{
                //     left:Math.random() * 100
                // },{
                //     left:Math.random() * 100
                // }
            ]
        }
    },
    mounted(){
        setInterval(() => {
            this.zidan() 
                      
        }, 30);
        setInterval(() => {
            this.diji() 
        }, 100);
        this.zidanZdiji()

    },
    created(){
        
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
        },
        diji(){
            if(this.djBottom <= 900 && this.djBottom > 100){
                this.djBottom -= 10
            }else{
                this.djBottom = 900;
                for (let djnum = 0; djnum < this.dj.length; djnum++) {
                    this.$set(this.dj[djnum], `left`, Math.floor( Math.random() * 100))
                }
            }
        },
        zidanZdiji(){
                console.log(this.djBottom);
                console.log(this.zdBottom);
                console.log(this.dj[0].left); 
                console.log(this.zdLeft);  
            if(this.djBottom > this.zdBottom && this.dj[0].left + 13 > this.zdLeft && this.dj[0].left - 13 < this.zdLeft){
                console.log("撞上了");
                console.log(this.djBottom);
                console.log(this.zdBottom);
                console.log(this.dj[0].left); 
                console.log(this.zdLeft);  
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
    margin-left: -25px;
    position: absolute;
}
</style>
