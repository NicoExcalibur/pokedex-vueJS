<template>
    <div class="detail">
        <div class="detail-view" v-if="show">

        </div>
        <i v-else class="fas fa-spinner fa-spin"></i>
    </div>
</template>

<script>
export default {
    props: [
       'pokemonUrl',
       'imageUrl' 
    ],
    data: () => {
        return {
            show: false,
            pokemon: {}
        }
    },
    methods: {
        fetchData() {
               let request = new Request(this.pokemonUrl);
            fetch(request)
                .then((response) => {
                    if(response.status === 200)
                        return response.json();
                })
                .then((data) => {
                    this.pokemon = data;
                    this.show = true;
                    })
                
                .catch((error) => {
                    console.log(error);
                })
        },
        created() {
            this.fetchData();
        }
    }
}
</script>

<style lang="scss" scoped>
    .detail {
        // TODO https://youtu.be/8pFkiNvxnD0?t=814
    }
</style>
