<template>
    <div>
        <h1>Привет, {{user.firstName}}!</h1>
        <p>Ты авторизовался в Vue приложении с помощью JWT-аутентификации</p>
        <h3>Список пользователей приложения:</h3>
        <em v-if="users.loading">Загрузка...</em>
        <span v-if="users.error" class="text-danger">ОШИБКА: {{users.error}}</span>
        <ul v-if="users.items">
            <li v-for="user in users.items" :key="user.id">
                {{user.firstName + ' ' + user.lastName}}
            </li>
        </ul>
        <p>
            <router-link to="/login">Выход</router-link>
        </p>
    </div>
</template>

<script>
export default {
    computed: {
        user () {
            return this.$store.state.authentication.user;
        },
        users () {
            return this.$store.state.users.all;
        }
    },
    created () {
        this.$store.dispatch('users/getAll');
    }
};
</script>