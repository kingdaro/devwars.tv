<template>
    <div class="card">
        <div class="inner">
            <h2 class="card__title" v-if="title">{{ title }}</h2>
            <slot></slot>
        </div>
    </div>
</template>

<script>
export default {
  props: [ 'title' ]
}
</script>

<style lang="scss" scoped>
@import '../assets/styles/utils';

.card {
  @extend %material;
  display: block;
  margin-bottom: 20px;
  border-top: $border-size-sm solid $brand-secondary;
  background-color: $bg-color-1;

  a {
    text-decoration: none;
  }

  &__title {
    padding: 0 0 15px;
    font-size: $h4-font-size;
    text-transform: uppercase;
    font-weight: $font-weight-bold;
  }

  &__image {
    display: block;
    margin: 0 auto 15px;
    max-width: 100px;
  }

  &.plain {
    border-top: none;
  }

  &.bezeless {
    padding: 0 !important;
  }

  &.dark {
    background-color: $bg-color-2;
  }
}

.inner {
  padding: 15px 15px 30px;

  @include breakpoint(xs) {
    padding-bottom: $s-space;
  }
}
</style>
