<template>
    <li class="users__item">
        <div class="users__item-img">
            <img :src="user.avatar" alt="avatar">
        </div>
        <p class="users__item-name">
            {{ user.first_name }} {{ user.last_name }}
        </p>
        <p class="users__item-birthsday">
            {{ formatBirthsday }}
        </p>
        <p class="users__item-phone">
            {{ user.phone_number }}
        </p>
    </li>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
    name: 'UserProfile',
    props: {
        user: {
            type: Object,
            required: true
        }
    },
    computed: {
        formatBirthsday(): string {
            return new Date(this.user.date_of_birth).toLocaleDateString('ru-RU')
        }
    }
})
</script>

<style lang="scss" scoped>
@import '../assets/variables.scss';

.users__item {
    border: 1px solid $green;
    border-radius: 10px;
    margin-right: 20px;
    margin-bottom: 20px;
    padding: 15px 15px 0;

    &-img {
        line-height: 0;
    }

    &-name {
        font-weight: bold;
    }
}
</style>
