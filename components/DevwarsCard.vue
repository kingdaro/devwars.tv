<template>
    <div class="DevwarsCard">
        <h1 class="title" v-if="title">{{ title }}</h1>
        <p class="desc" v-if="desc">{{ desc }}</p>

        <div class="main">
            <slot></slot>
        </div>

        <div class="actions">
            <slot name="actions"></slot>
        </div>
    </div>
</template>

<script>
export default {
  props: [ 'title', 'desc' ]
}
</script>

<style lang="scss" scoped>
@import '../assets/styles/utils';

.DevwarsCard {
    max-width: 400px;
    border-width: $border-size;
    border-style: solid;
    border-image:
        linear-gradient(
            110deg,
            $brand-primary 0%,
            $brand-primary 47%,
            $bg-color-4 47%,
            $bg-color-4 53%,
            $brand-secondary 53%,
            $brand-secondary 100%
        ) 1;
    padding: $m-space $ms-space $ms-space;
    margin: 0 auto;
    text-align: center;

    .title {
        margin-bottom: $m-space;
        font-size: $h2-font-size;
    }

    .desc {
        margin-top: -$grid-gutter-width;
        margin-bottom: $m-space;
        color: $text-color-secondary;
    }

    .main {
       padding-top: $grid-gutter-part;
    }

    .actions {
        margin-top: $m-space;

        .btn + .btn {
            margin-top: $grid-gutter-part;
        }
    }
}
</style>
