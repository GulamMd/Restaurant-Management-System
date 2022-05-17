<template>
<Header />
<h1>Hello User! welcome on Update Restaurant Page.</h1>
<form class="update">
    <input type="text" placeholder="Enter Name" v-model="restaurant.name" name="name" />
    <input
      type="text"
      placeholder="Enter Address"
      v-model="restaurant.address"
      name="address"
    />
    <input
      type="text"
      placeholder="Enter Contact"
      v-model="restaurant.contact"
      name="contact"
    />
    <button type="button" v-on:click="updateRestaurant">Update Restaurant</button>
  </form>
</template>

<script>
import axios from 'axios'
import Header from './Header.vue'
export default {
    name: "Update",
    data() {
    return {
      restaurant: {
        name: "",
        address: "",
        contact: "",
      },
    };
  },
    components: {
        Header
    },
    methods:{
      async updateRestaurant(){
        
        let result=await axios.put("http://localhost:3000/restaurant/"+this.$route.params.id,{
            name:this.restaurant.name,
            address:this.restaurant.address,
            contact:this.restaurant.contact,
          });
          if(result.status==200){
            this.$router.push({name:'Home'});
          }
      }
    },
    async mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({
                name: 'SignUp'
            })
        }
        let result = await axios.get("http://localhost:3000/restaurant/"+this.$route.params.id);
        // console.warn(this.$route.params.id);
        //console.warn(result.data);
        this.restaurant=result.data;
    }
}
</script>
