<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title>
          數數字
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-grey-1"
    >
      <q-list>
        <q-item>
          難度1
          <q-input type="number" v-model="l"/>
        </q-item>
        <q-item>
          難度2
          <q-input type="number" v-model="n"/>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view :l="l" :n="n"/>
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MainLayout',
  data () {
    return {
      leftDrawerOpen: false,
      l: 4,
      n: 4
    }
  }
}
</script>
