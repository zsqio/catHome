<template>
  <!-- 详情页 -->
  <div>
    <div class="mdl-cell mdl-cell--8-col">
      <div class="picture">
        <img :src="this.$data.pictures[$route.params.id].url" />
      </div>
      <div class="info">
        <span>{{ this.$data.pictures[$route.params.id].info }}</span>
      </div>
      <div class="createdTime">
        <span>{{this.pictures[$route.params.id].created_at}}</span>
      </div>
    </div>
    <div class="mdl-cell mdl-cell--4-col mdl-cell--8-col-tablet">
      <div class="comment">
        <span>{{this.pictures[$route.params.id].comment}}</span>
      </div>
      <div class="actions">
        <router-link to="/post" class="mdl-button mdl-js-button mdl-button--raised mdl-button--colored">ANSWER</router-link>
      </div>
    </div>
  </div>
</template>

<script>
import data from '../data'
export default {
  data () {
    return {
      'pictures': data.pictures
    }
  },
  mounted () {
    console.log(this.$route.params.id)
  }
}
</script>

<style lang="css">
.picture > img {
   color: #fff;
   width:100%;
 }
 .createdTime,.info {
   text-align: right;
   padding: 5px;
   color: #555;
   font-size: 10px;
 }
 .comment {
   padding: 10px;
   color: #555;
 }
 .actions {
   text-align: center;
 }
</style>
