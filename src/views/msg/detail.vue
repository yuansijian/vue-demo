<template>
  <div class="panel panel-default">
    <div class="panel-heading clearfix">
      标题：<strong>{{ msg.title }}</strong>
      <span class="badge pull-right">
        {{ msg.ctime | dateTimeFormatter }}
      </span>
      <br>
      发布者：
      <a v-link="`/msg?authors=${msg.author}`">
        {{ msg.author }}
      </a>
    </div>
    <div class="panel-body min-h-160 max-h-300 overflow-fix">
      <p class="lead">{{ msg.content }}</p>
    </div>
    <div class="clearfix">
      <div class="pull-right m-t-5">
        <opt-btn-group
          :msg="msg" :auto-jump="true">
        </opt-btn-group>
      </div>
    </div>
  </div>
</template>
<script>
import OptBtnGroup from './_components/OptBtnGroup'
import autoLoadByParams from './_mixins/autoLoadByParams'

export default {
  mixins: [autoLoadByParams],
  components: { OptBtnGroup },
  data: () => ({ msg: {} }),
  computed: {
    isMine () {
      const { author } = this.msg
      const { userData } = this.$root
      if (!author || !userData) return
      return author === userData.username
    }
  }
}
</script>
<style>
.min-h-160 {
  min-height: 160px;
}
.max-h-300 {
  max-height: 300px;
}
.overflow-fix {
  overflow-x: hidden;
  overflow-y: auto;
}
</style>
