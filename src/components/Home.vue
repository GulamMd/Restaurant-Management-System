<template>
<Header />
<h1>Hello {{name}}! welcome on Home Page.</h1>
<table border="1">
    <tr>
        <td>Id</td>
        <td>Name</td>
        <td>Address</td>
        <td>Contact</td>
        <td>Actions</td>
    </tr>
    <tr v-for="item in restaurants" :key="item.id">
        <td>{{item.id}}</td>
        <td>{{item.name}}</td>
        <td>{{item.address}}</td>
        <td>{{item.contact}}</td>
        <td>
            <router-link :to="'/update/'+item.id" id="updateButton">Update</router-link>
            <button v-on:click="deleteRestaurant(item.id)" id="deleteButton">Delete</button>
        </td>
    </tr>
</table>
</template>

<script>
import axios from 'axios'
import Header from './Header.vue'
export default {
    name: "Home",
    data() {
        return {
            name: "",
            restaurants: []
        }
    },
    components: {
        Header
    },
    methods: {
        async deleteRestaurant(id) {
            let result = await axios.delete("http://localhost:3000/restaurant/" + id);
            if (result.status == 200) {
                this.loadData();
            }
        },
        async loadData() {
            let user = localStorage.getItem('user-info');
            this.name = JSON.parse(user).name;
            if (!user) {
                this.$router.push({
                    name: 'SignUp'
                })
            }
            let result = await axios.get("http://localhost:3000/restaurant");
            this.restaurants = result.data;
        }
    },
    mounted() {
        this.loadData();
    }
}
</script>

<style scoped>
td {
    width: 180px;
    height: 40px;
}
#updateButton{
    font-size: 14px;
    text-decoration: none;
    color: green;
}
#updateButton:hover{
    text-decoration: underline;
}
#deleteButton{
    color: red;
    margin-left: 10px;
}
</style>
