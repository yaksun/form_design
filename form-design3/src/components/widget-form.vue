<template>
  <div class="widget-form-wrapper">
    <div
      class="widget-form-container"
      :class="pageData.theme"
      :style="{...pageData.style,backgroundImage:`url(${pageData.style.backgroundImage})`}"
    >
    {{pageData.list }}
      <div :class="pageData.template">
        <draggable
          v-model="pageData.list"
          :group="{ name:'widget',put:true}"
          ghostClass="ghost"
          :swapThreshold="0.8"
          :animation="100"
          class="widget-form-list"
          :class="{'widget-empty': pageData.list.length === 0&&!pageData.style.backgroundImage}"
        >
          <template v-for="(item,index) in pageData.list">
            
            <div  :key="item.key">
              <widget-form-list
                :item="item"
                :data="pageData.list"
                :index="index"
                @click.native.stop="handleSelectWidget(pageData.list[index])"
              />
            </div>
          </template>
        </draggable>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from 'vuex';
import Draggable from 'vuedraggable'
import WidgetFormList from './widget-form-list'

export default {
  components: {
    WidgetFormList, Draggable
  },
  data() {
    return {
    }
  },
  computed: {
    ...mapState({
      selectWg: state => state.common.selectWg,
      pageData: state => state.common.pageData,
    })
  },
  methods: {
    handleWidgetDelete(data, index) {
      if (data.length - 1 === index) {
        if (index === 0) {
          this.$store.commit('setSelectWg', {})
        } else {
          this.$store.commit('setSelectWg', data[index - 1])
        }
      } else {
        this.$store.commit('setSelectWg', data[index + 1])
      }
      this.$nextTick(() => {
        data.splice(index, 1)
      })
    },
    handleSelectWidget(select_wg) {
      this.$store.commit('setSelectWg', select_wg);
      this.$store.commit('setConfigTab', "widget");
    },
    handleWidgetAdd(evt) {
      console.log(evt);
      const newIndex = evt.newIndex;
      let newObj = this.$util.deepClone(this.pageData.list[newIndex]);
      newObj.key = newObj.type + '_' + Date.now() + '_' + Math.ceil(Math.random() * 1000000);
      this.$set(this.pageData.list, newIndex, newObj);
      this.$store.commit('setSelectWg', newObj);
      this.$store.commit('setConfigTab', "widget");
    },
    formWidgetAdd(evt) {
      // console.log(evt);
      const formIndex = this.pageData.list.findIndex(item => item.type === 'formList');
      const newIndex = evt.newIndex;
      let newObj = this.$util.deepClone(this.pageData.list[formIndex].list[newIndex]);
      newObj.key = newObj.type + '_' + Date.now() + '_' + Math.ceil(Math.random() * 1000000);
      this.$set(this.pageData.list[formIndex].list, newIndex, newObj);
      this.$store.commit('setSelectWg', newObj);
      this.$store.commit('setConfigTab', "widget");
    },
    setConfigTab() {
      this.$store.commit("setConfigTab", "page");
    }
  }
}
</script>
