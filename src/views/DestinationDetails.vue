<template>
    <div>
        <GoBack />
       <section class="destination">
           <h1>{{destination.name}}</h1>
           <div class="destination-details">
                <img :src="require(`@/assets/${destination.image}`)" :alt="destination.name">
                <p>{{destination.description}}</p>
           </div>
       </section>
        <section class="experiences">
            <h2>Top experiences in {{destination.name}}</h2>
            <div class="cards" id="experience">
                <div v-for="experience in destination.experiences" :key="experience.slug" class="card">
                   
                   <router-link :to="{
                       name: 'ExperienceDetails',
                       params:  { experienceSlug: experience.slug },
                       hash:'#experience',
                       }"> 

                    <img :src="require(`@/assets/${experience.image}`)" :alt="experience.name">
                    <span class="card-text">
                        {{experience.name}}
                    </span>
                     </router-link>
                </div>
            </div>
            <router-view :key="$route.path"></router-view>
        </section>

    </div>
</template>

<script>
import store from "@/store.js";
import GoBack from "@/components/GoBack";

export default {
    components: {
        GoBack,
    },
    props: {
        slug: {
        type:String,
        required: true
        }
    },
    computed: {
        destination() {
            return store.destinations.find(destination => destination.slug === this.slug);
        }
    }

}
</script>
<style scoped>
img {
    height: auto;
    width: 100%;
    max-height: 400px;
    max-width: 600px;
}
.destination-details {
    display: flex;
}
.experiences {
    padding: 40px 0;
}
.destination-details p {
    margin: 0 40px;
    text-align: left;
    font-size: 20px;
}
.cards {
    display: flex;
}
.cards img {
    max-height: 200px;
}
.card {
    padding: 0 20px;
    position: relative;
}
.card-text {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: white;
    font-size: 25px;
    font-weight: bold;
    text-decoration: none;
}
</style>
    