<template>
  <div class="container is-fullhd" style="background-color: #EEEEEE;">
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-menu">
        <div class="navbar-start">
          <div class="navbar-item">
            <a class="button is-text is-myBack" @click="$router.push('/')"><span class="icon"><i class="fas fa-chevron-left"></i></span></a>
            <h5 class="subtitle is-5 has-text-dark"> Select Merchandises</h5>
          </div>
        </div>
        <div class="navbar-end">
          <div class="navbar-item">
          <button class="button is-rounded is-light is-inverted badge is-badge-danger is-badge-medium" @click="openItemList"
           :data-badge="itemList.length">Item{{ itemList.length >= 2 ? 's' : '' }}</button>
          </div>
        </div>
      </div>
    </nav>
    <div class="columns">
      <div class="column columnPadding">
        <div class="control has-icons-right">
          <br><br><br>
          <input class="input is-rounded" type="text" placeholder="Search" v-model="searchItems">
          <span class="icon is-small is-right">
            <i class="fas fa-search"></i>
          </span>
        </div>
        <h6 class="subtitle marginsTop is-6 has-text-dark has-text-left">Frequently</h6>
      </div>
    </div>
    <div class="columns is-variable is-2" style="padding-left: 18px; padding-right: 18px;">
      <div class="column">
        <div class="box canClick" @click="selectItem('cheese')">
          <img src="@/assets/cheese.png" class="icon-item"><br>
          Cheese
        </div>
      </div>
      <div class="column">
        <div class="box canClick" @click="selectItem('avocado')">
          <img src="@/assets/avocado.png" class="icon-item"><br>
          Avocado
        </div>
      </div>
      <div class="column">
        <div class="box canClick" @click="selectItem('bacon')">
          <img src="@/assets/bacon.png" class="icon-item"><br>
          Bacon
        </div>
      </div>
    </div>
    <div class="columns">
      <div class="column columnPadding">
        <h6 class="subtitle marginsTop is-6 has-text-dark has-text-left">Items</h6>
      </div>
    </div>
    <div class="columns" v-for="(name, index) in categoryloop" :key="index" style="padding-left: 18px; padding-right: 18px;">
      <div class="column is-half">
        <button class="button is-fullwidth is-medium" @click="addToList(name.indexLeft)">
          {{ name.nameLeft }}
        </button>
      </div>
      <div class="column is-half" v-if="name.nameRight !== null">
        <button class="button is-fullwidth is-medium" @click="addToList(name.indexRight)">
          {{ name.nameRight }}
        </button>
      </div>
    </div>
    <modal-select-brand ref="modalSelectBrand"/>
    <modal-item-list ref="modalItemList" :category="category" :itemList="itemList" @deleteFromList="deleteMe"/>
  </div>
</template>

<script>
import modalSelectBrand from '@/components/modalSelectBrand'
import modalItemList from '@/components/modalItemList'
export default {
  components: {
    'modal-select-brand': modalSelectBrand,
    'modal-item-list': modalItemList
  },
  data () {
    return {
      // category: ['Foods', 'Drinks', 'Fruits', 'Vegetables', 'Pets', 'Babies', 'Sport&Travels'],
      category: { '1': 'Water', '2': 'Curtains', '3': 'Rug', '4': 'T-Shirt', '5': 'Skirt', '6': 'Underwear', '7': 'Pets', '8': 'Camera', '9': 'Fresh milk', '10': 'Bread', '11': 'Cheese', '12': 'Tea', '13': 'Butter', '14': 'Beef', '15': 'Pork', '16': 'Coffee', '17': 'Salt', '18': 'Pepper', '19': 'Vinegar', '20': 'Salad', '21': 'Spice', '22': 'Vegetable', '23': 'Noodle', '24': 'Jelly', '25': 'Canfood', '26': 'Seafood', '27': 'Bag', '28': 'Chocolate', '29': 'Macaroni', '30': 'Beer', '31': 'Wheat', '32': 'Cam', '33': 'Oat', '34': 'Sweets', '35': 'Snack', '36': 'Cardboard', '37': 'Pen', '38': 'Pencil', '39': 'Oil', '40': 'Sugar', '41': 'Bandage', '42': 'Sauce', '43': 'Light', '44': 'Phone', '45': 'Towel', '46': 'Book', '47': 'Toilet paper', '48': 'Glasses', '49': 'Paper', '50': 'Blotting paper', '51': 'colored paper', '52': 'Color pencil', '53': 'Marker', '54': 'Highlight', '55': 'Ballpoint pen', '56': 'Coloring pen' },
      itemList: [],
      searchItems: ''
    }
  },
  computed: {
    categoryloop: function () {
      let output = []
      let i = 1
      const search = this.searchItems.toLowerCase()
      for (const key in this.category) {
        if (this.category.hasOwnProperty(key)) {
          const element = this.category[key]
          if (this.itemList.indexOf(key) >= 0) ;
          else if (element.toLowerCase().indexOf(search) >= 0) {
            if (i % 2 === 1) {
              output.push({
                nameLeft: element,
                nameRight: null,
                indexLeft: key,
                indexRight: null
              })
            } else {
              const rowIndex = parseInt(i / 2) - 1
              output[rowIndex].nameRight = element
              output[rowIndex].indexRight = key
            }
            i++
          }
        }
      }
      return output
    }
  },
  methods: {
    selectItem: function (name) {
      console.log(name)
      this.$refs.modalSelectBrand.openModal(name)
    },
    openItemList: function () {
      this.$refs.modalItemList.openModal()
    },
    addToList: function (index) {
      console.log(index)
      if (this.itemList.indexOf(index) >= 0) return ''
      this.itemList.push(index)
    },
    deleteMe: function (value) {
      const index = this.itemList.indexOf(value)
      if (index >= 0) {
        this.itemList.splice(index, 1)
      }
    }
  }
}
</script>

<style scoped>
.navbar {
  background-color: #FDB849;
  height: 60px;
  position: fixed;
  overflow: hidden;
  width: 100%;
  top: 0;
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

.is-myBack {
  text-decoration: none !important;
  margin-right: 6px;
}
</style>
