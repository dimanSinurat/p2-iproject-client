<template>
  <div>
    <h2>Data of Corona spread <small><em>by name</em></small></h2>
    <p class="text-secondary">updates every 15 minutes</p>
    <div class=" container row w-50 mt-5">
      <div class="col md-12">
        <form @submit.prevent="findName">
          <label class="mb-1">name of nations</label>
          <input type="text" class="form-control glass text-white" placeholder="nation name" v-model="name">
          <button class="glass btn btn-sm bg-white mt-3" type="submit">Search</button>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from '../apis/server'
export default {
  name : 'Content',
  data() {
    return {
      name : ''
    }
  },
  methods: {
    popUp(message){
      this.$vs.notify({
        title:'failed to process input',
        text:`${message}&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`,
        color: 'danger',
        time: 5000,
      })
    },
    findName(){
      let name = this.name
      
      axios({
        url: `/nations/${name}`,
        method: 'POST',
        headers: {
          access_token : localStorage.access_token
        }
      })
        .then(({data})=> {
          if (data.length === 0){
          this.popUp(`keyword is not valid as a name of nation`)
          } else {
            this.$store.commit('GET_NAME', data)
            this.$router.push('/detail')
          }
        })
        .catch((err) => {
          console.log(err.response.data)
          this.popUp(`You haven't entered anything yet`)
        })
    }
  }
}
</script>

<style scoped>
  .glass {
    background-color: rgba(255, 255, 255, 0.06);
    -webkit-backdrop-filter: blur(20px);
    backdrop-filter: blur(20px);
    border: none;
  }
</style>