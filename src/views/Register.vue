<template>
    <main class="form-signin w-100 m-auto">
        <form>
            
            <h1 class="h3 mb-3 fw-normal">Please register</h1>

            <div class="form-floating">
                <input v-model="userName" type="string" class="form-control" id="floatingUserName" placeholder="Marcos Lahen">
                <label for="floatingUserName">User name</label>
            </div>

            <div class="form-floating">
                <input v-model="email" type="email" class="form-control" id="floatingInput" placeholder="name@example.com">
                <label for="floatingInput">Email address</label>
            </div>

            <div class="form-floating">
                <input v-model="password" type="password" class="form-control" id="floatingPassword" placeholder="Password">
                <label for="floatingPassword">Password</label>
            </div>

            <div class="form-floating">
                <input v-model="confirmPassword" type="password" class="form-control" id="floatingConfirmPassword" placeholder="Confirm assword">
                <label for="confirmPassword">Confirm password</label>
            </div>
            
            <button class="w-100 btn btn-lg btn-primary" type="submit">Register</button>

        </form>
    </main>
</template>

<script>

    //import Cookie from 'js-cookie';

    export default {
        name: "Register",

        data(){
            return{
                userName: '',
                email: '',
                password: '',
                confirmPassword: ''
            };
        },

        /* created() {
            Cookie.remove('_myapp_token');
        }, */

        /*methods: {
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
        } */
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

    .form-signin #floatingUserName, .form-signin #floatingInput{
        margin-bottom: -1px;
    }
    .form-signin #floatingUserName {
        border-bottom-right-radius: 0;
        border-bottom-left-radius: 0;
    }

    .form-signin #floatingInput, .form-signin #floatingPassword  {
        border-top-right-radius: 0;
        border-top-left-radius: 0;
        border-bottom-right-radius: 0;
        border-bottom-left-radius: 0;
    }
    
    .form-signin #floatingConfirmPassword {
        margin-bottom: 10px;
        border-top-right-radius: 0;
        border-top-left-radius: 0;
    }

</style>