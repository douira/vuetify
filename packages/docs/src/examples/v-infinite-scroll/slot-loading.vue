<template>
  <v-infinite-scroll
    height="400"
    @load="load"
  >
    <template v-for="(item, index) in items" :key="item">
      <div :class="['pa-2', index % 2 === 0 ? 'bg-grey-lighten-2' : '']">
        Item #{{ item }}
      </div>
    </template>
    <template v-slot:loading>
      This is taking a very long time...
    </template>
  </v-infinite-scroll>
</template>

<script>
  export default {
    data: () => ({
      items: Array.from({ length: 50 }, (k, v) => v + 1),
    }),

    methods: {
      load ({ done }) {
        setTimeout(() => {
          this.items.push(...Array.from({ length: 10 }, (k, v) => v + this.items.at(-1) + 1))

          done('ok')
        }, 4000)
      },
    },
  }
</script>
