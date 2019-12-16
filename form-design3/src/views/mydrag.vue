<template>
    <div class="home">
         <el-container>
      <div class="form-edit-wrapper flex">
           <el-aside style="min-width:300px;width:20vw">
                 <draggable
              tag="ul"
              :list="basicList"
              :group="{ name:'words', pull:'clone',put:false}"
              :sort="false"
              ghostClass="ghost" 
            >
              <li  v-for="(item, index) in basicList" :key="index">
                <a>{{item}}</a>
              </li>
            </draggable>
        </el-aside>
        


            <el-container class="center-container" direction="vertical">
          
                <el-main>
                    <widget-word></widget-word>
                </el-main>
        </el-container>
        </div>
    </el-container>
    </div>
    
    
    
</template>
<script>
import Draggable from 'vuedraggable'
import WidgetWord from '../components/widget-word.vue'
export default {
    components:{
        Draggable,
        WidgetWord
    },
    data(){
        return{
            basicList:[
                'id','姓名','年龄','身高'
            ]
        }
    }
}
</script>
<style lang="stylus">
li{
    width 80px;
    height 90px;
    background :#ccc;
    margin-top :20px;
}
@import '../assets/css/index.styl';
@import '../assets/css/widget.styl';
@import '../assets/css/config.styl';
@import '../assets/css/themes.styl';
</style>