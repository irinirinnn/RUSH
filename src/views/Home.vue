<template>
  <div class="container is-fullhd" style="height:100%;">
    <div :style="bg1"></div>
    <nav class="navbar" role="navigation" aria-label="main navigation">
      <div class="navbar-brand">
        <a class="navbar-item">
          <img src="@/assets/RUSHlogo.png" alt="logo" class="logo">
        </a>
      </div>
      <div class="navbar-menu">
        <div class="navbar-end">
          <div class="navbar-item">
            <div class="button is-rounded is-dark is-inverted is-outlined" disabled>
                Log in
            </div>
          </div>
        </div>
      </div>
    </nav>
    <div class="columns">
      <div class="column has-text-left is-offset-1 is-10">
        <br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br><br>
        <p style="margin-bottom: 3px;">select store to go :</p>
        <div :class="'dropdown is-up is-fullwidth' + (nameSuper === chooseName || nameSuper === '' ? '' : ' is-active')">
          <div class="dropdown-trigger">
            <input class="input is-rounded" type="text" placeholder="Name of the store" style="margin-bottom: 6px;" v-model="nameSuper">
          </div>
          <div class="dropdown-menu" id="dropdown-menu" role="menu">
            <div class="dropdown-content">
              <a class="dropdown-item" v-for="(store, index) in searchingStore" :key="index" @click="selectName(store)">
                {{ store }}
              </a>
            </div>
          </div>
        </div>
        <div class="columns">
          <div class="column is-8 is-offset-2">
          <button class="button is-rounded is-dark is-fullwidth" @click="$router.push('/selectMerchandises')">Next</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      nameSuper: '',
      Image: 'https://www.orcam.com/wp-content/uploads/2014/08/supermarket-960x480.jpg',
      nameOfSupermarket: ['Siam Paragon', 'ICONSIAM', 'Central Embassy', 'Central World', 'Emquatier', 'Mega Bangna', 'Central Westgate'],
      chooseName: ''
    }
  },
  computed: {
    bg1: function () {
      return {
        backgroundImage: 'url(\'' + this.Image + '\')',
        backgroundSize: 'cover',
        backgroundPosition: 'center',
        height: '100vh',
        width: '100vw',
        zIndex: '0',
        top: '0px',
        position: 'absolute',
        filter: 'grayscale(100%)',
        opacity: '0.4'
      }
    },
    searchingStore: function () {
      let output = []
      for (const key in this.nameOfSupermarket) {
        if (this.nameOfSupermarket.hasOwnProperty(key)) {
          const element = this.nameOfSupermarket[key]
          element.search(this.nameSuper)
          if (element.search(new RegExp(this.nameSuper, 'i')) >= 0) {
            output.push(element)
          }
        }
      }
      return output
    }
  },
  methods: {
    selectName: function (name) {
      this.nameSuper = name
      this.chooseName = name
    }
  }
}
</script>

<style scoped>
.dropdown.is-fullwidth {
  display: flex;
}
.dropdown.is-fullwidth > .dropdown-trigger, .dropdown.is-fullwidth > .dropdown-menu {
  width: 100%;
}

.navbar {
  background-color: #FDB849;
  height: 60px;
}
.navbar-brand {
  height: 60px;
  padding-left: 12px;
}
.logo {
  width: 35px;
  height: 35px !important;
}
.navbar-menu {
  margin-right: 0px !important;
  margin-left: 0px;
}
.navbar-end {
  padding-right: 12px;
}
</style>
