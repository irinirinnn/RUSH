<template>
  <div :class="'modal' + (isOpen ? ' is-active' : '')">
    <div class="modal-background"></div>
    <div class="modal-card" style="padding: 0px 12px;">
      <header class="modal-card-head">
        <p class="modal-card-title">Select Brand</p>
        <button class="delete" aria-label="close" @click="closeModal"></button>
      </header>
      <section class="modal-card-body">
        <input class="input is-rounded" type="text" placeholder="Search">
        <div class="box" style="padding: 12px; overflow: scroll; height: 50vh; background-color: #B5DCDC;">
          <brand v-model="choosed" v-for="(namebrand, index) in brandloop" :key="index" :name="namebrand.name" :stock="namebrand.isOutOfStock"/>
        </div>
      </section>
      <footer class="modal-card-foot">
        <button class="button is-success">Save changes</button>
        <button class="button">Cancel</button>
      </footer>
    </div>
  </div>
</template>

<script>
import brand from '@/components/brand'
export default {
  components: {
    'brand': brand
  },
  data () {
    return {
      isOpen: false,
      name: '',
      choosed: '',
      brandItem: {
        cheese: [
          { name: 'cheese1', isOutOfStock: false },
          { name: 'cheese2', isOutOfStock: true },
          { name: 'cheese3', isOutOfStock: true },
          { name: 'cheese4', isOutOfStock: false },
          { name: 'cheese5', isOutOfStock: false }
        ],
        avocado: [
          { name: 'avocado1', isOutOfStock: true },
          { name: 'avocado2', isOutOfStock: false },
          { name: 'avocado3', isOutOfStock: false },
          { name: 'avocado4', isOutOfStock: false },
          { name: 'avocado5', isOutOfStock: false }
        ],
        bacon: [
          { name: 'bacon1', isOutOfStock: true },
          { name: 'bacon2', isOutOfStock: true },
          { name: 'bacon3', isOutOfStock: true },
          { name: 'bacon4', isOutOfStock: true },
          { name: 'bacon5', isOutOfStock: false }
        ]
      }
    }
  },
  methods: {
    openModal: function (name) {
      console.log('modal', name)
      this.name = name
      this.isOpen = true
    },
    closeModal: function () {
      this.isOpen = false
      this.name = ''
      this.choosed = ''
    }
  },
  computed: {
    brandloop: function () {
      return this.brandItem[this.name] || []
    }
  }
}
</script>

<style scoped>
</style>
