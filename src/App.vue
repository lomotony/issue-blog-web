<template>
  <div>
    <left-layout/>
    <router-view class="main-container"/>
    <bga-back-top :svgMajorColor="'#7b79e5'" :svgMinorColor="'#ba6fda'" :svgType="'rocket_smoke'"/>
  </div>
</template>
<style lang="scss">
  .main-container {
    position: fixed;
    left: 200px;
    right: 0px;
    bottom: 0px;
    top: 0px;
  }
</style>
<script>
  import LeftLayout from './components/LeftLayout.vue'
  import { mapActions } from 'vuex'

  export default {
    components: {
      LeftLayout
    },
    methods: {
      ...mapActions([
        'setLabels',
        'setGitHubUser'
      ])
    },
    mounted () {
      this.$nextTick(function () {
        this.$gitHubApi.getUserInfo(this).then(this.$http.spread((userResp, labelResp) => {
          this.setGitHubUser(userResp.data)
          this.setLabels(labelResp.data)
        }))
      })
    }
  }
</script>
