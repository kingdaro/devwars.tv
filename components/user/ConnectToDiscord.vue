<template>
    <a v-if="!hasDiscord" :href="discordUrl" class="btn btn-discord btn-icon" target="_blank">
        <i class="fab fa-discord"></i>
        <span>Connect Discord</span>
    </a>
    <a v-else class="btn btn-outline-success btn-icon" v-async-click="[removeProvider, 'DISCORD']">
        <i class="fa fa-check"></i>
        <span>Discord Connected</span>
    </a>
</template>

<script>
    import Component, {State, Action} from 'nuxt-class-component';
    import Vue from 'vue';
    import { user_has_provider } from '../../utils/linked-accounts';

    @Component({})
    export default class extends Vue {
        @State(state => state.user.user) user;

        @Action('user/disconnectLinkedAccount') removeProvider;

        discordUrl = `https://discordapp.com/api/oauth2/authorize?client_id=465280450420670484&redirect_uri=https%3A%2F%2Fapi.devwars.tv/oauth/discord&response_type=code&scope=identify`;

        get hasDiscord() {
            return user_has_provider(this.user, 'DISCORD');
        }
    }
</script>
