<template>

    <Navbar />

    <main class="form-signin w-100 m-auto">
        <form @submit.stop.prevent="submit">
            
            <h1 class="h3 mb-3 fw-normal">Please sign in</h1>

            <Message v-if="msg" :msg="msg" />

            <div class="form-floating">
                <input v-model="email" type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
                <label for="floatingInput">Email address</label>
            </div>

            <div class="form-floating">
                <input v-model="password" type="password" class="form-control" id="floatingPassword" placeholder="Password">
                <label for="floatingPassword">Password</label>
            </div>

            <div id="btn-register">
                <span>Não tem conta?</span>
                <button type="button" @click="loadRegister">Cadastre-se.</button>
            </div>
            
            
            <button class="w-100 btn btn-lg btn-primary" type="submit">Sign in</button>

        </form>
    </main>
</template>

<script>

    import Cookie from 'js-cookie';
    import Navbar from '../components/Navbar.vue';
    import Message from '../components/Message.vue';

    export default {
        name: "Login",

        data(){
            return{
                email: '',
                password: '',
                msg: ''
            };
        },

        components: {
            Navbar,
            Message
        },

        methods: {
             async submit() {
                const playload = {
                    email: this.email,
                    password: this.password
                };

                const req =  await fetch('http://localhost:8000/api/login', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'Access': 'application/json'
                    },
                    body: JSON.stringify(playload)
                });

                const data = await req.json();

                
                if( data.access_token ){
                    Cookie.set('_myapp_token', data.access_token);
                    this.msg = "Login realizado com sucesso";

                    setTimeout( () => {
                        this.msg = "";
                        this.$router.push('/');

                    }, 3000);
                }else{
                    setTimeout( () => {
                        this.msg = "Login não realizado, por favor, verifique o e-mail e/ou senha";

                        this.email = "";
                        this.password = "";

                    }, 3000);
                }

            },
            loadRegister(){
                this.$router.push('/register');
            },
            checkingLogin(){
                const token = Cookie.get("_myapp_token");

                if(token){
                    this.$router.push('/');
                }
            }
        },
        beforeMount() {
            this.checkingLogin()
            
        }
    }
</script>

<style scoped>

    .form-signin {
    max-width: 330px;
    padding: 15px;
    }

    .form-signin .form-floating:focus-within {
    z-index: 2;
    }

    .form-signin input[type="email"] {
    margin-bottom: -1px;
    border-bottom-right-radius: 0;
    border-bottom-left-radius: 0;
    }

    .form-signin input[type="password"] {
    margin-bottom: 10px;
    border-top-left-radius: 0;
    border-top-right-radius: 0;
    }

    #btn-register{
        margin: 15px 0;
    }

    #btn-register button{
        background-color: #fff;
        border: none;
        color: #0b5ed7;
    }

    #btn-register button:hover{
        color: #0c49a5;
    }

</style>