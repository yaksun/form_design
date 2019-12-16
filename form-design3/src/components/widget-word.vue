<template>
    <div>
     <MyTable />
      {{pageData.words }}
        <draggable
          v-model="pageData.words"
          :group="{ name:'words',put:true}"
          ghostClass="ghost"
          :swapThreshold="0.8"
          :animation="100"
          @add="handleWidgetAdd"
        >

          <template v-for="(item,index) in pageData.words">
            
            <div  :key="item.key">
              <widget-word-list
                :item="item"
                :data="pageData.words"
                :index="index"
              />
            </div>
          </template>
        </draggable>

        
    </div>
</template>
<script>
import {mapState} from 'vuex'
import WidgetWordList from './widget-word-list'
import draggable from 'vuedraggable'
import MyTable from './mytable.vue'
export default {
    computed:{
         
         ...mapState({
      pageData: state => state.common.pageData,
    })
    },
    

    components:{
        WidgetWordList,
        draggable,
           MyTable
    },
    methods:{
        handleWidgetAdd(){
            console.log('添加了')
        }
    }
}
</script>
<style lang="">
    
</style>