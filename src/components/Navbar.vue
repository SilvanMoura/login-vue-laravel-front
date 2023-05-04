<template>
    <nav>
        <router-link to="/">Home</router-link>
        <router-link to="/about">Sobre Nós</router-link>
    </nav>
</template>

<script>
    export default{
        name: "Navbar",
    }
</script>

<style scoped>
    nav{
        background-color: #0b5ed7;
        border-bottom: 2px solid #4388ee;
        padding: 15px 50px;
        display: flex;
        justify-content: flex-end;
        align-items: center;
    }

    nav #logo-url{
        margin: auto;
        margin-left: 0;
    }

    #logo{
        width: 40px;
        height: 40px;
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