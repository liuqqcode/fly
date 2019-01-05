<template>
    <div class="fly">
        <div class="diji" v-for="item in dj" :key>
            <img :class="'diji' + item.left" :style="{left:item.left + '%',bottom:djBottom + 'px'}" src="../assets/diji.png" alt="">
            敌机{{item.left}}底边{{djBottom}}
        </div>
        <div v-for="item in zd" :key>
            <img :class="'item' + item.id" :style="{bottom:item.zdBottom + zdBottom + 'px',left:zdLeft +'%'}" class="bullet" src="../assets/feiji.png" alt="">
        </div>
        <!-- <img class="bullet" :style="{bottom:zdBottom + 'px',left:zdLeft + '%'}" src="../assets/feiji.png" alt=""> -->
        <p>子弹{{zdLeft}}底边{{zdBottom}}</p>
        <img class="aircraft" ref="topInfo" :style="{bottom:numBottom + 'px',left:numLeft + '%'}"  src="../assets/fly.png" alt="" srcset="">
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
                },{
                    left:Math.floor( Math.random() * 100)
                },{
                    left:Math.floor( Math.random() * 100)
                },{
                    left:Math.floor( Math.random() * 100)
                }

            ],
            zd:[
                {
                    id:1,
                    zdBottom:100
                },
                {   
                    id:2,
                    zdBottom:200
                },
                {
                    id:3,
                    zdBottom:300
                }
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
        let that = this;
        document.onkeydown = function (e) {
            let key = window.event.keyCode;
            console.log(key);
            
            if(key == 38 && that.numBottom < 500){
                that.numBottom += 10;
                console.log(that.numLeft);
                return that.numLeft;
            }
            if(key == 40 && that.numBottom > 0){
                that.numBottom -= 10;
                console.log(that.numLeft);
                return that.numLeft;

            }
            if(key == 37 && that.numLeft > 2){
                that.numLeft -= 3;
                console.log(that.numLeft);
                return that.numLeft;

            }
            if(key == 39 && that.numLeft < 96){
                that.numLeft += 3;
                console.log(that.numLeft);
                return that.numLeft;

            }
        }
    },
    methods:{
        zidan(){
            if(this.zdBottom < 1000){
                this.zdBottom += 10;
                this.zdLeft = this.numLeft ;

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
