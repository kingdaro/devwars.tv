<template>
    <div>
        <div class="ribbon"></div>
        <div class="container">
            <div class="row-lift align-center">
                <div class="heading">
                    <h1>Welcome to DevWars!</h1>
                </div>
            </div>
        </div>

        <div class="footer-offset align-center">
            <div class="container">
                <div class="mod-card">
                    <h3 class="modpanel__subtitle">Verify your email address</h3>
                    <p class="form-group">Confirm your email by clicking the verification link we sent to your inbox.
                        Don't forget to <u>check your spam folder</u>.</p>
                    <div>
                        <button v-async-click="[resend]" class="btn btn-outline-gray">Resend Email</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>

<script>
    import Component from 'nuxt-class-component';
    import Vue from 'vue';
    import Http from "../services/Http";

    @Component
    export default class Pending extends Vue {

        async resend() {
            await Http.for('user/resend').save();

            this.$store.dispatch('toast/success', `We have sent off another email, please wait patiently.`);
        }
    }
</script>
