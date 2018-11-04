<template>
  <div class="v-collapse">
    <div class="c-item" :class="{open: item._open}" v-for="(item, i) of items">
      <div class="c-head" @click="select(i)">{{item.title}}</div>
      <div class="c-body" v-show="item._show">{{item.content}}</div>
    </div>
  </div>
</template>

<script>
  export default {
    name: 'v-collapse',
    data() {
      return {
        items: [
          {
            title: 'First',
            content: ''
          },
          {
            title: 'Second',
            content: ''
          },
          {
            title: 'Third',
            content: 'Third'
          }
        ],
        index: -1,
        itemIndex: -1
      }
    },
    methods: {
      select(i) {
        if (this.index === i) return

        this.close(this.index)
        this.open(i)
        this.index = i
      },
      open(i) {
        if (i < 0) return

        const item = this.items[i]
        item._show = true
        this.$forceUpdate()
        setTimeout(() => {
          item._open = true
          this.$forceUpdate()
        }, 0)
      },
      close(i) {
        if (i < 0) return

        const item = this.items[i]
        item._open = false
        this.$forceUpdate()
        setTimeout(() => {
          item._show = false
          this.$forceUpdate()
        }, 500)
      }
    }
  }
</script>