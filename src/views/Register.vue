<template>

    <main class="form-signin w-100 m-auto">
        <form @submit.stop.prevent="submit">
            
            <h1 class="h3 mb-3 fw-normal">Please register</h1>

            <Message v-if="msg" :msg="msg" />

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

    import Message from '../components/Message.vue';

    export default {
        name: "Register",

        data(){
            return{
                userName: '',
                email: '',
                password: '',
                confirmPassword: '',
                msg: ''
            };
        },

        components: {
            Message,
        },

        methods: {
            async submit() {
                const payload = {
                    name: this.userName,
                    email: this.email,
                    password: this.password
                };

                const req =  await fetch('http://localhost:8000/api/register', {
                    method: 'POST',
                    headers: {
                        'Content-Type': 'application/json',
                        'Access': 'application/json'
                    },
                    body: JSON.stringify(payload)
                });

                const data = await req.json();

                if( data == "success" ){
                    this.msg = "Usuário cadastrado com sucesso";

                    setTimeout( () => {
                        this.msg = "";
                        this.$router.push('/login');

                    }, 3000);
                }else{
                    setTimeout( () => {
                        this.msg = "";

                        this.userName = "";
                        this.email = "";
                        this.password = "";
                        this.confirmPassword = "";

                    }, 3000);
                }

            }
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