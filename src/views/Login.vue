<template>
    <main class="form-signin w-100 m-auto">
        <form @submit.stop.prevent="submit">
            
            <h1 class="h3 mb-3 fw-normal">Please sign in</h1>

            <div class="form-floating">
                <input v-model="email" type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
                <label for="floatingInput">Email address</label>
            </div>

            <div class="form-floating">
                <input v-model="password" type="password" class="form-control" id="floatingPassword" placeholder="Password">
                <label for="floatingPassword">Password</label>
            </div>
            
            <button class="w-100 btn btn-lg btn-primary" type="submit">Sign in</button>

        </form>
    </main>
</template>

<script>

    import Cookie from 'js-cookie';

    export default {
        name: "Login",

        data(){
            return{
                email: '',
                password: ''
            };
        },

        created() {
            Cookie.remove('_myapp_token');
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

                Cookie.set('_myapp_token', data.access_token);

            }
        }
    }
</script>

<style>

    /* html,
    body {
    height: 100%;
    }

    body {
    display: flex;
    align-items: center;
    padding-top: 40px;
    padding-bottom: 40px;
    background-color: #f5f5f5;
    } */

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

</style>