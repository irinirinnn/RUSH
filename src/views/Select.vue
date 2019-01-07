<template>
  <div class="container is-fullhd" style="height:100%;">
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-menu">
        <div class="navbar-start">
          <div class="navbar-item">
            <h5 class="subtitle is-5 has-text-dark">Select Merchandises</h5>
          </div>
        </div>
        <div class="navbar-end">
          <div class="navbar-item">
          <button class="button is-rounded is-light is-inverted badge is-badge-danger is-badge-medium" :data-badge="itemList.length">Item{{ itemList.length >= 2 ? 's' : '' }}</button>
          </div>
        </div>
      </div>
    </nav>
    <div class="columns">
      <div class="column columnPadding">
        <input class="input is-rounded" type="text" placeholder="Search">
        <h6 class="subtitle marginsTop is-6 has-text-dark has-text-left">Frequently</h6>
      </div>
    </div>
    <div class="columns is-variable is-2" style="padding-left: 18px; padding-right: 18px;">
      <div class="column">
        <div class="box canClick" @click="selectItem('cheese')">
          <img src="@/assets/cheese.png" class="icon-item">
          Cheese
        </div>
      </div>
      <div class="column">
        <div class="box canClick" @click="selectItem('avocado')">
          <img src="@/assets/avocado.png" class="icon-item">
          Avocado
        </div>
      </div>
      <div class="column">
        <div class="box canClick" @click="selectItem('bacon')">
          <img src="@/assets/bacon.png" class="icon-item">
          Bacon
        </div>
      </div>
    </div>
    <div class="columns">
      <div class="column columnPadding">
        <h6 class="subtitle marginsTop is-6 has-text-dark has-text-left">Category</h6>
      </div>
    </div>
    <div class="columns" v-for="(name, index) in categoryloop" :key="index" style="padding-left: 18px; padding-right: 18px;">
      <div class="column is-half">
        <button class="button is-fullwidth is-medium">
          {{ name.nameLeft }}
        </button>
      </div>
      <div class="column is-half" v-if="name.nameRight !== null">
        <button class="button is-fullwidth is-medium">
          {{ name.nameRight }}
        </button>
      </div>
    </div>
    <modal-select-brand ref="modalSelectBrand"/>
  </div>
</template>

<script>
import modalSelectBrand from '@/components/modalSelectBrand'

export default {
  components: {
    'modal-select-brand': modalSelectBrand
  },
  data () {
    return {
      category: ['Foods', 'Drinks', 'Fruits', 'Vegetables', 'Pets', 'Babies', 'Sport&Travels'],
      itemList: []
    }
  },
  computed: {
    categoryloop: function () {
      let output = []
      let i = 1
      for (const key in this.category) {
        if (this.category.hasOwnProperty(key)) {
          const element = this.category[key]
          if (i % 2 === 1) {
            output.push({
              nameLeft: element,
              nameRight: null
            })
          } else {
            const rowIndex = parseInt(i / 2) - 1
            output[rowIndex].nameRight = element
          }
          i++
        }
      }
      return output
    }
  },
  methods: {
    selectItem: function (name) {
      console.log(name)
      this.$refs.modalSelectBrand.openModal(name)
    }
  }
}
</script>

<style scoped>
.navbar {
  background-color: #FDB849;
  height: 60px;
}

.navbar-menu {
  margin-right: 0px !important;
  margin-left: 0px;
}

.navbar-start {
  padding-left: 12px;
}

.navbar-end {
  padding-right: 10px;
}

.marginsTop {
  margin-top: 18px !important;
}

.columnPadding {
  padding: 18px 24px 0px 24px;
}

.canClick {
  cursor: pointer;
}

.icon-item {
  width: 40px;
  height: 40px;
}

.box {
  padding: 18px;
}
</style>
