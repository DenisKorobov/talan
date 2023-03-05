<template>
    <main class="main">
        <h1>Пользователи</h1>
        <section class="forms">
            <div class="forms__getting-users">
                <form class="forms__form">
                    <fieldset class="forms__form-fieldset">
                        <legend>Запросить конкретное число пользователей</legend>
                        <input class="forms__form-input" v-model="count" placeholder="введите количество пользователей">
                        <button class="forms__form-button" @click="getUsers(count)">Запросить</button>
                    </fieldset>
                </form>
                <form class="forms__form">
                    <fieldset class="forms__form-fieldset">
                        <legend>Запросить случайное число пользователей</legend>
                        <button class="forms__form-button" @click="getRandomUsers()">Запросить</button>
                    </fieldset>
                </form>
            </div>
            <form class="forms__form">
                <fieldset class="forms__form-fieldset">
                    <legend>Поиск</legend>
                    <input class="forms__form-input" v-model="search" placeholder="введите ключевое слово">
                    <button class="forms__form-button" @click="filterUsers()">Поиск</button>
                </fieldset>
            </form>
        </section>
        <ul class="users">
            <UserProfile v-for="user in users" :key="user.id" :user="user" v-show="user.visible" />
        </ul>
    </main>
</template>

<script lang="ts">
import Vue from 'vue'
import UserProfile from '@/components/UserProfile.vue'

interface User {
    id: number
    first_name: string
    last_name: string
    date_of_birth: string
    phone_number: string
    visible: boolean
}

let users: User[] = []

export default Vue.extend({
    name: 'UsersView',
    components: {
        UserProfile
    },
    data() {
        return {
            count: '',
            users: users,
            search: ''
        }
    },
    methods: {
        async getUsers(count: number | string): Promise<void> {
            try {
                this.$emit('change-preloader', true)
                let response = await fetch(`https://random-data-api.com/api/v2/users?size=${count}`)
                this.users = await response.json()
                for (let user of this.users) {
                    this.$set(user, 'visible', true)
                }
                this.$emit('change-preloader', false)
            } catch (err) {
                console.log(err)
            }
        },
        getRandomUsers(): void {
            let count = Math.round(Math.random() * 30)
            this.getUsers(count)
        },
        filterUsers(): void {
            let regexp = new RegExp(this.search, "i")
            for (let user of this.users) {
                if (regexp.test(user.first_name) || regexp.test(user.last_name) || regexp.test(user.date_of_birth) || regexp.test(user.phone_number)) {
                    user.visible = true
                } else if (user.visible) {
                    user.visible = false
                }
            }
        },
    },
    created() {
        this.getRandomUsers()
    }
})
</script>

<style lang="scss" scoped>
@import '../assets/variables.scss';

.forms {
    display: flex;

    &__getting-users {
        margin-right: 20px;
    }

    &__form {
        max-width: 500px;
        margin-bottom: 30px;

        &-fieldset {
            border: 1px solid $green;
            border-radius: 5px;
            margin: 0;
        }

        &-input {
            width: 250px;
            height: 30px;
            padding: 0 10px;
            border: 1px solid $green-transparent;
            border-radius: 5px;
            margin-right: 10px;
        }

        &-input:focus {
            outline: 1px solid $green;
        }

        &-button {
            width: 80px;
            height: 30px;
            border: 1px solid $green;
            background: $green-transparent;
            border-radius: 5px;
            cursor: pointer;
        }
    }
}

.users {
    display: flex;
    flex-wrap: wrap;
}
</style>
