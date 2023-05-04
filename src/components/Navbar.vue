<!-- <template>
    <nav>
            <router-link to="/">Home</router-link>
        <router-link to="/">Home</router-link>
        <router-link to="/about">Sobre Nós</router-link>
    </nav>
</template> -->

<template>
    <nav>
        
        <p>LOGO</p>
    
        <div>
            <router-link to="/">Pagina inicial</router-link>
            <router-link to="/about">Sobre nós</router-link>
        </div>
    
        <router-link v-if="link" to="/login">Entrar</router-link>
        <a v-if="!link" href="/" @click="logout">Sair</a>

    </nav>
</template>

<script>
    import Cookies from 'js-cookie';

    export default{
        name: "Navbar",

        data(){
            return{
                link: true
            }
        },

        methods: {
            loadPage(){
                const token = Cookies.get("_myapp_token");

                !token ? this.link=true : this.link=false ;
            },
            logout(){
                Cookies.remove("_myapp_token");
            }
        },
        mounted() {
            this.loadPage()
        }

    }
</script>

<style scoped>
    nav{
        display: flex;
        justify-content: space-between;
        background-color: #0b5ed7;
        border-bottom: 2px solid #4388ee;
        padding: 15px 50px;
        
    }

    nav p, div{
        margin-top: 12px;
    }

    nav a{
        color: #f7fafa;
        text-decoration: none;
        margin: 12px;
        transition: .5s;
    }

    nav a:hover{
        color: #292821;
    }
</style>