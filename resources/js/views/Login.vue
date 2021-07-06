<template>
    <div class="login-page">
        <div class="login">
            <div class="login-container auth-container">
                <div class="login-form-column">
                    <form v-on:submit.prevent="authLoginAppUser">
                        <h3>Olá!</h3>
                        <div class="form-wrapper">
                            <label>Usuário</label>
                            <input type="text" name="username" id="username" v-model="username" placeholder="Digite seu usuário" class="form-control" required>
                        </div>

                        <div class="form-wrapper">
                            <label for="password">Senha</label>
                            <input type="password" name="password" id="password" placeholder="*******" class="form-control" required>
                        </div>
                        <button type="submit" class="mt-3">Entrar &nbsp;&nbsp;<span v-if="showSpinner" class="fa fa-spin fa-spinner"></span></button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import { CometChat } from "@cometchat-pro/chat";
    export default {
        data(){
            return {
                username: "",
                password:'',
                showSpinner: false,
                token: '',
            };
        },

        methods: {
            authLoginAppUser(){
                let userData = {
                    username: this.username,
                    password: this.password
                };
                this.showSpinner = true;

                if (this.username && this.password) {
                    axios.post(`http://127.0.0.1:8000/login`, userData).then(response => {
                        this.logUserInToCometChat(this.username);
                        this.showSpinner = false;
                    }).catch(error => {
                        console.log(error.response.data.message);
                        this.showSpinner = false;
                    })

                } else {
                    console.log('Por favor verifique suas credenciais');
                }
            },
            logUserInToCometChat(){
                var AUTH_KEY = "AUTH_KEY"
                CometChat.login(this.username,AUTH_KEY).then(
                    data => {
                        console.log(data)
                        window.location.href = '/home';
                    },

                    error => {
                        this.showSpinner = false;
                        alert("Ups. Algo deu errado. Isso geralmente acontece quando você insere um nome de usuário que não existe. Verifique o console para obter mais informações");
                        console.log("Erro no Login:", error.code);
                    }
                );
            }
        }
    };
</script>
