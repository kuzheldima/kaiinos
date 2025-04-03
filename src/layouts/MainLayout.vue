<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar class="flex main-bar q-py-md">
        <strong class="text-white text-h5 q-mr-lg"><b class="text-primary">S</b>mart <b class="text-primary">U</b>tility <b class="text-primary">M</b>anager</strong>
        <q-input rounded outlined label-color="white" v-model="search" class="search-field q-ml-auto q-mr-md" dense label="Search">
          <template v-slot:append>
            <q-btn
              unelevated
              rounded
              style="min-width: 70px;"
              color="accent"
              icon="search"
            />
          </template>
        </q-input>
        <div class="btns">
          <q-btn class="q-mx-sm" outline round color="accent" no-caps icon="notifications" style="min-height: 35px; min-width: 35px;" />
          <q-btn outline round color="accent" no-caps icon="person" style="min-height: 35px; min-width: 35px;" />
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      class="main-drawer"
      :mini="miniState"
    >
      <q-btn
        flat
        dense
        round
        icon="menu"
        aria-label="Menu"
        @click="toggleLeftDrawer"
        size="lg"
        class="q-ml-xs q-mt-sm"
      />
      <q-list class="q-px-sm q-mt-md">
        <EssentialLink
          v-for="link in linksList"
          :key="link.title"
          v-bind="link"
        />
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent } from "vue";
import EssentialLink from "components/EssentialLink.vue";

const linksList = [
  {
    title: "Legal",
    caption: "See terms, policies and privacy",
    icon: "gavel",
    link: "#",
  },
  {
    title: "Help and feedback",
    caption: "Get customer support",
    icon: "help",
    link: "#",
  },
];

export default defineComponent({
  name: "MainLayout",

  components: {
    EssentialLink,
  },

  data() {
    return {
      search: "",
      linksList,
      leftDrawerOpen: true,
      miniState: true,
    };
  },

  methods: {
    toggleLeftDrawer() {
      this.miniState = !this.miniState;
    },
  },
});
</script>

<style lang="scss">
.main-bar {
  background: rgb(0,60,126);
  background: linear-gradient(90deg, rgba(0,60,126,1) 0%, rgba(0,60,126,1) 0%, rgba(48,115,167,1) 83%);
}
.main-drawer {
  background: linear-gradient(180deg, #004276, #0c1d44); /* Темно-синий градиент */
  color: white;
  border-right: 1px solid #1a5487;
}
.search-field {
  max-width: 480px;
  width: 100%;
  .q-field__control {
    padding-right: 0;
  }
}
.q-field--outlined .q-field__control:before {
  border: 1px solid #438bca;
}
</style>
