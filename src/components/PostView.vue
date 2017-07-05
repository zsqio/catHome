<template>
  <!-- 上传页 -->
  <form>
    <div class="mdl-grid">
      <div class="mdl-cell mdl-cell--8-col">
        <div class="card-image__picture">
          <img :src="this.catUrl"/>
        </div>
      </div>
      <div class="mdl-cell mdl-cell--4-col mdl-cell--8-col-tablet">
        <div class="mdl-textfield mdl-js-textfield mdl-textfield--floating-label is-upgraded is-dirty">
          <input id="username" v-model="title" type="text" class="mdl-textfield__input"/>
          <label for="username" class="mdl-textfield__label">Describe me</label>
        </div>
        <div class="actions">
          <a @click.prevent="postCat" class="mdl-button mdl-js-button mdl-button--raised mdl-button--colored">
            POST A CAT
          </a>
        </div>
      </div>
    </div>
  </form>
</template>
<script>
  import data from '../data'
  import util from '../common/util.js'
  export default {
    data () {
      return {
        'catId': 0,
        'catUrl': '',
        'title': ''
      }
    },
    computed: {
      isCatLoaded: function () {
        return this.catUrl !== ''
      }
    },
    mounted () {
      this.axios.get('https://thecatapi.com/api/images/get?format=xml&results_per_page=1')
      .then(response => {
        console.log(response.data)
        this.catUrl = this.parse(response.data).root.children['0'].children['0'].children['0'].children['0'].content
        this.catId = data.pictures.length
      })
    },
    methods: {
      postCat () {
        console.log(this.catUrl)
        console.log(this.catId)
        data.pictures.push(
          {
            'id': this.catId,
            'url': this.catUrl,
            'comment': this.title,
            'info': 'Posted by watermelon on Monday',
            'created_at': util.formatDate.format(new Date(), 'yyyy-MM-dd')
          }
        ).then(
          this.$router.push('/')
        )
      }
    }
  }
</script>
<style scoped>
  img {
    width: 100%;
  }
  .mdl-spinner {
    position: relative;
    top: 50%;
    left: 50%;
  }
</style>
