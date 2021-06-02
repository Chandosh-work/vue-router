<template>
    <div>
        <h1>Hello {{userName}}</h1>
        <p>
            <router-link :to="{name: 'invoice'}">Invoices</router-link>
        </p>
        <button @click="logout" class="btn">Logout</button>
    </div>
</template>

<script>
import store from "@/store.js";
export default {
    data() {
        return {
            userName: store.user
        }
    },
    methods: {
        logout() {
            store.user = "";
            this.$router.push("/");
        }
    }
    
}
</script>