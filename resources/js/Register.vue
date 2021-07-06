<template>
    <div class="login-page">
        <div class="login">
            <div class="register-container auth-container">
                <div class="register-image-column">

                </div>
                <div class="register-form-column">
                    <form v-on:submit.prevent="registerAppUser">
                        <h3>Cria uma conta</h3>
                        <div class="form-wrapper">
                            <label for="username">Nome de Usuário</label>
                            <input type="text" name="username" id="username" v-model="username" placeholder="Entre com seu nome de usuário" class="form-control" required>
                        </div>

                        <div class="form-wrapper">
                            <label for="password">Password</label>
                            <input type="text" name="password" id="password" v-model="password" placeholder="Digite sua senha" class="form-control" required> 
                        </div>

                        <div class="form-wrapper">
                            <label for="password_confirmation">Confirme sua senha</label>
                        </div>
                        <button type="submit" class="mt-3">Cadastre-se &nbsp;&nbsp;<span v-if="showSpinner" class="fa fa-spin fa-spinner"></span></button>
                    </form>
                </div>
            </div>
        </div>
    </div>
</template>