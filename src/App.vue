<template>
    <v-app>
        <Nav v-if="this.$store.state.token !==''"/>
        <router-view/>
    </v-app>
</template>

<script>
    import Nav from "./components/Nav"

    export default {
        components: {Nav},
        data() {
            return {}
        },
        mounted() {
            if (this.$store.state.token !== '' && this.$store.state.userId !== '') {
                setTimeout(() => {
                    console.log(this.$peer.id)
                    let param = {
                        peer_id: this.$peer.id
                    };
                    axios.put('users/user/' + this.$store.state.userId + '/peer', param).then((response) => {
                        console.log(response.status)
                    })

                    axios.put('users/user/' + this.$store.state.userId + '/stream', {onAir: false}).then((response) => {
                        console.log(response.status)
                    })
                }, 100)

            }

            if (this.$store.state.userId !== '') {

            }

        },
        watch: {}
    }
</script>

<style lang="scss">
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
    }

    #nav {
        padding: 30px;

        a {
            font-weight: bold;
            color: #2c3e50;

            &.router-link-exact-active {
                color: #42b983;
            }
        }
    }
</style>