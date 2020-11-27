<template>
  <div class="noticia">
    <div class="title" @click="open">
      {{ item.text }}
    </div>
    <div class="claimant">{{ item.claimant }}</div>
    <div class="rating" :class="{ falso }">
      <span class="veredicto">Veredicto: </span>
      {{ item.claimReview[0].textualRating }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    item: {
      type: Object,
    },
  },
  computed: {
    review() {
      return this.item.claimReview[0].textualRating
    },
    falso() {
      return this.review == 'Falso'
    },
  },
  methods: {
    open() {
      window.open(this.item.claimReview[0].url)
    },
  },
}
</script>

<style scoped>
.noticia {
  @apply mb-7;
}
.title {
  @apply font-bold;
}
.claimant {
  @apply text-gray-500;
  @apply font-semibold;
}
.falso {
  @apply text-red-500;
}
.veredicto {
  @apply text-gray-900;
}
</style>
