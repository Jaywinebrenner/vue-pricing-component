<template>
  <div class="about">
    <h1>This is an about page</h1>
    <input 
    class="mainInput" 
    type="text" autocomplete="off" 
    v-model="state" 
    @focus="modal = true"  
    placeholder="Enter a State" 
    @input="filterStates">


    <div class="filteredCardWrapper" v-if="filteredStates && modal">
     
        <div 
        class="filteredCard"
        v-for="(filteredState) in filteredStates" 
        :key="filteredState.id"
        @click="setState(filteredState)"
        >  {{filteredState}}
        </div>
    </div>


        <button @click="postsVisible = ! postsVisible">Show the posts</button>
    <div v-if="postsVisible">
        <div v-for="post in posts" :key="post">{{ post.title }} </div>
    </div>


  </div>
</template>

<script>
import axios from 'axios';




  


export default {

  data: function () {
    return {
      postsVisible: false,
      state: '',
      posts: [],
      post: '',
      states: [
        "Florida", "Alabama", "Illinois", "Oregon", "New York", "Alaska", "Indiana"
      ],
      filteredStates: [],
      modal: false,
    }
  },



  mounted() {
    this.filterStates();



    axios.get(`http://jsonplaceholder.typicode.com/posts`)
    .then(response => {
      // JSON responses are automatically parsed.
      this.posts = response.data
      console.log("posts", this.posts);
      
    })
    .catch(e => {
      this.errors.push(e)
    })
  },

  methods: {



    filterStates() {
      if(this.state.length == 0) {
        this.filteredStates = this.states
      }

      this.filteredStates = this.states.filter(state => {
        return state.toLowerCase().startsWith(this.state.toLowerCase())
      })
    },
    setState(state) {
      this.state = state
      this.filteredStates = []
    },
    
  },

  watch: {
    state() {
      this.filterStates();
    }
  }
}

</script>

<style scoped>
</style>
