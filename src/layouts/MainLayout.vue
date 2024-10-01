<template>
  <q-layout view="lHr lpR fFf">

    <q-header bordered class="bg-white text-black"><!--Setting the Header and its color on css quasar.variables-->
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" />

        <q-toolbar-title class = "text-weight-bold">
          <span class="gt-sm">{{$route.name}}</span>
          <q-icon
            class="header-icon q-pa-md lt-md"
            name="fas fa-dove"
            size="sm"
            color="primary"
          />
        </q-toolbar-title>

      </q-toolbar>
    </q-header>

    <q-drawer show-if-above v-model="leftDrawerOpen" side="left" :width="283" bordered>   <!--left Drawer-->
      <q-icon 
      class="q-pa-md"
      name="fas fa-dove"
      size="lg"
      color="primary"
      />

      <q-list>      <!--List of items-->
        <q-item 
          exact
          clickable 
          v-ripple
          to="/"
        >
          <q-item-section avatar>
            <q-icon name="home" size="md" />
          </q-item-section>
          <q-item-section class="text-h6 text-weight-bold">Home</q-item-section>
        </q-item>

        <q-item
          exact
          clickable 
          v-ripple
          to="/about"
        >
          <q-item-section avatar>
            <q-icon name="help" size="md" />
          </q-item-section>
          <q-item-section class="text-h6 text-weight-bold">About</q-item-section>
        </q-item>

      </q-list>
    </q-drawer>

    <q-drawer show-if-above v-model="right" side="right" bordered> <!---Right side drawer--->
      <q-input outlined rounded dense clas="q-ma-md" placeholder="Search in Emitter">
        <template v-slot:prepend>
          <q-icon name="search"/>
        </template>
      </q-input>

      <q-list padding separator> <!--List of items for the right drawer--->

        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label overline class="text-grey">Education</q-item-label>
            <q-item-label class="text-weight-bold">Profe pongame 100</q-item-label>
            <q-item-label caption>Asi de paro</q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>5 min ago</q-item-label>
          </q-item-section>
        </q-item>

        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label overline class="text-grey">Pais</q-item-label>
            <q-item-label class="text-weight-bold">Se va el mejor presidente del Mexico</q-item-label>
            <q-item-label caption>Siempre con usted Obrador</q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>39 min ago</q-item-label>
          </q-item-section>
        </q-item>

        <q-item class="q-pa-md">
          <q-item-section>
            <q-item-label overline class="text-grey">Entretenimiento</q-item-label>
            <q-item-label class="text-weight-bold">Hellboy la peor pelicula</q-item-label>
            <q-item-label caption>The cookedman</q-item-label>
          </q-item-section>

          <q-item-section side top>
            <q-item-label caption>2 hours ago</q-item-label>
          </q-item-section>
        </q-item>


      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script>
import { ref } from 'vue'

export default {
  setup () {
    const leftDrawerOpen = ref(false)
    const rightDrawerOpen = ref(false)

    return {
      leftDrawerOpen,
      toggleLeftDrawer () {
        leftDrawerOpen.value = !leftDrawerOpen.value
      },

      rightDrawerOpen,
      toggleRightDrawer () {
        rightDrawerOpen.value = !rightDrawerOpen.value
      }
    }
  }
}
</script>

<style lang="sass">
.header-icon
  position: absolute
  bottom: 0
  left: 50%
  transform: translateX(-50%)
</style>