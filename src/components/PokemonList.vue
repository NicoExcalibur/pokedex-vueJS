<template>
    <div class="list">
        <article v-for="(pokemon,index) in pokemons" :key="'pkmn' + index" @click="setPokemonUrl(pokemon.url)">
            <img :src="imageUrl + pokemon.id + '.png'" width="90">
            <h3>{{ pokemon.name }}</h3>
        </article>
        <div id="scroll-trigger" ref="infinitescrolltrigger">
        </div>
    </div>
</template>

<script>
export default {
    props: [
        'imageUrl',
        'apiUrl'
    ],
    data: () => {
        return {
            pokemons: [],
            nextUrl: '',
            currentUrl: ''
        }
    },
    methods: {
        fetchData() {
            let request = new Request(this.currentUrl);
            fetch(request)
                .then((response) => {
                    if(response.status === 200)
                        return response.json();
                })
                .then((data) => {
                    this.nextUrl = data.next;
                    data.results.forEach(pokemon => {
                        pokemon.id = pokemon.url.split('/')
                            .filter(function(part) { return !!part }).pop();
                        this.pokemons.push(pokemon);
                        //console.log(pokemon);
                    })
                })
                .catch((error) => {
                    console.log(error);
                })
        },
        scrollTrigger() {
            const observer = new IntersectionObserver((entries) => {
                entries.forEach(entry => {
                   if (entry.intersectionRatio > 0 && this.nextUrl)  {
                       this.next();
                   }
                });
            })

            observer.observe(this.$refs.infinitescrolltrigger);
        },
        next(){
            this.currentUrl = this.nextUrl;
            this.fetchData();
        },
        setPokemonUrl(url) {
            this.$emit('setPokemonUrl', url);
        }
    },
    created() {
        this.currentUrl = this.apiUrl;
        this.fetchData();
    },
    mounted() {
        this.scrollTrigger();
    }
 }
</script>

<style>
    .list {
        display: flex;
        flex-wrap: wrap;
        justify-content: space-evenly;
    }

    .list article {
        width: 165px;
        margin-bottom: 1em;
        text-align: center;
        background-color: rgb(223, 221, 221);
        text-transform: capitalize;
        border-radius: 10px;
        padding: 1em;
        box-shadow: 0 15px 30px rgba(0, 0, 0, 0.2); 
    }

    #scroll-trigger {
        display: flex;
        justify-content: center;
        align-items: center;
        width: 100%;
        font-size: 2rem;
        color:black;
    }

</style>