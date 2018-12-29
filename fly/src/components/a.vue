<template>
  　<el-table border style="width: 100%" ref="table">
    <el-table-column align="center" prop="name" label="名称" width="150">
    </el-table-column>
    <el-table-column align="center" label="正常">
      <el-table-column align="center" sortable prop="normalB" label="笔数">
        <template scope="scope">
          <span>
            <el-input style="width: 90px" placeholder="笔数" v-model="scope.row.normalB" @change="handleCreditChange()"
              class="table_input normalB_input" @keyup.native="show($event,scope.$index)"></el-input>
          </span>
        </template>
      </el-table-column>
      <el-table-column align="center" sortable prop="normalY" label="余额(万元)">
        <template scope="scope">
          <span>
            <el-input style="width: 90px" placeholder="余额" v-model="scope.row.normalY" @change="handleCreditChange()"
              @blur="handleBalanceBlur($event)" @focus="handleBalanceClear($event)" class="table_input normalY_input"
              @keyup.native="show($event,scope.$index)"></el-input>
          </span>
        </template>
      </el-table-column>
    </el-table-column>
    <el-table-column align="center" label="关注">
      <el-table-column align="center" sortable prop="focusB" label="笔数">
        <template scope="scope">    
          <span>
            <el-input style="width: 90px" placeholder="笔数" v-model="scope.row.focusB" @change="handleCreditChange()"
              class="table_input focusB_input" @keyup.native="show($event,scope.$index)"></el-input>
          </span>
        </template>
      </el-table-column>
      <el-table-column align="center" sortable prop="focusY" label="余额(万元)">
        <template scope="scope">
          <span>
            <el-input style="width: 90px" placeholder="余额" v-model="scope.row.focusY" @change="handleCreditChange()"
              @blur="handleBalanceBlur($event)" @focus="handleBalanceClear($event)" class="table_input focusY_input"
              @keyup.native="show($event,scope.$index)"></el-input>
          </span>
        </template>
      </el-table-column>
    </el-table-column>
    <el-table-column align="center" label="不良">
      <el-table-column align="center" sortable prop="badB" label="笔数">
        <template scope="scope">
          <span>
            <el-input style="width: 90px" placeholder="笔数" v-model="scope.row.badB" @change="handleCreditChange()"
              class="table_input badB_input" @keyup.native="show($event,scope.$index)"></el-input>
          </span>
        </template>
      </el-table-column>
      <el-table-column align="center" sortable prop="badY" label="余额(万元)">
        <template scope="scope">
          <span>
            <el-input style="width: 90px" placeholder="余额" v-model="scope.row.badY" @change="handleCreditChange()"
              @blur="handleBalanceBlur($event)" @focus="handleBalanceClear($event)" class="table_input badY_input"
              @keyup.native="show($event,scope.$index)"></el-input>
          </span>
        </template>
      </el-table-column>
    </el-table-column>
    <el-table-column align="center" prop="amountY" sortable label="余额(万元)">
      <template scope="scope">
        <span>{{scope.row.amountY}}</span>
      </template>
    </el-table-column>
  </el-table>
</template>
<script>
export default {
    data(){
        return{

        }
    },
    methods:{
        //键盘触发事件
        show(ev,index){
            
            let newIndex ;
            
            //通过ev 获取 当前input 名称 用于判断属于哪列
            let clssName = ev.target.offsetParent.className;
            
            //每一列
            if(clssName.indexOf('normalB_input') != -1){
                
                newIndex = index*6 ;
                
            } else if (clssName.indexOf('normalY_input') != -1) {
                
                newIndex = index*6 + 1 ;
                
            } else if (clssName.indexOf('focusB_input') != -1) {
                
                newIndex = index*6 + 2;
                
            } else if (clssName.indexOf('focusY_input') != -1) {
                
                newIndex = index*6 + 3;
                
            } else if (clssName.indexOf('badB_input') != -1) {
                
                newIndex = index*6 + 4;
                
            } else if (clssName.indexOf('badY_input') != -1) {
                
                newIndex = index*6 + 5;
                
            }
            
            //获取每一列的input名称
            let normalB_input = document.getElementsByClassName('normalB_input')
            let normalY_input = document.getElementsByClassName('normalY_input')
            let focusB_input = document.getElementsByClassName('focusB_input')
            let focusY_input = document.getElementsByClassName('focusY_input')
            let badB_input = document.getElementsByClassName('badB_input')
            let badY_input = document.getElementsByClassName('badY_input')
            
            //获取54个input
            let inputAll = document.querySelectorAll('.table_input input');

            //向上 =38
            if(ev.keyCode == 38){
                //当焦点在第一行的时候 按向上的时候焦点要聚焦到前一列的最后一个
                if(newIndex >=1 && newIndex<=5){
                    newIndex = newIndex + 47;
                } else {
                    newIndex -= 6 ;
                }

                
                if( inputAll[newIndex] ){
                    
                    inputAll[newIndex].focus();
                    
                }
                
            }
                
            //下 = 40
            if(ev.keyCode == 40){
                
                //当newIndex 在最后一行的时候 焦点要聚焦到 下一列的第一个
                if(newIndex>= 48 && newIndex<53){
                    
                newIndex =  (newIndex%8) + 1
                }else {
                    newIndex += 6 ;
                }
                
                
                if( inputAll[newIndex] ){
                    
                    inputAll[newIndex].focus();
                    
                }
                
            }
            
            //左 = 37
            if(ev.keyCode == 37){
                
            newIndex -= 1 ;
            
                if( inputAll[newIndex] ){
                    
                    inputAll[newIndex].focus();
                    
                }
            }
            
            //右 = 39
            if(ev.keyCode == 39){
                
                newIndex += 1 ;
                
                if( inputAll[newIndex] ){
                    
                    inputAll[newIndex].focus();
                    
                }
            }                
        },
    }
}
</script>